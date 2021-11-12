# SparkSQL优化

## 内存优化-堆内内存调优-Spark RDD缓存

对表进行 rdd catch 缓存时出现内存不够的情况：

**Kryo serialization** 可以减少（压缩）缓存内存

注意具体使用需要 register 这一步

- [ ] RDD 的 catch persist 等算子的总结比较

## 内存优化-堆内内存调优-Spark DF、DS 缓存

Dataset 的 **catch** 可以减少（压缩）缓存内存

注意具体使用需要了解 Encoder

结论：调优需要反复测试；相比较 RDD 推荐使用 DF DS 开发。

## 内存优化-堆外内存使用

## 合理控制 shuffle 分区个数

### 场景

> `spark.sql.shuffle.partitions` 默认为 200 ，而我的 application vcore 数为 12 （远远小于 200）

存在 vcore 空闲的情况， Partitioner 有可能分不了那么多的 partition 。

### 场景分析

提交命令

```shell
spark-submit \
# spark 基本参数
--master yarn \
--deploy-mode client \
# 资源参数 memory, cpu
--driver-memory 1g \
--num-executors 3 \
--executor-cores 4 \
--executor-memory 2g \
# 
--queue spark \
# 执行 jar 包
--class com.atguigu.sparksqltuning.PartitionTuning spark-sql-tuning-1.0-SNAPSHOT-jar-with-dependencies.jar 
```

去向yarn申请的executor vcore资源个数为12个（num-executors*executor-cores）,如果不修改spark sql分区个数，那么就会像上图所展示存在cpu空转的情况，而且 shuffle 小文件个数也很多。

这样往往读取文件的调度时间大于读取文件本身，而且会频繁打开关闭文件句柄，浪费较为宝贵的io资源，执行效率也大大降低。——来自：[spark partition 理解 / coalesce 与 repartition的区别](https://www.cnblogs.com/jiangxiaoxian/p/9539760.html)

### 优化

通过修改 `spark.sql.shuffle.partitions` 参数为 36 合理控制 shuffle 分区个数

Job 执行时间变短了

小文件过多问题也解决了（也可以通过 coalesce 算子缩小分区）

### 结论

离线计算最好设置分区数为 vcore 数的 2~3 倍，实时计算则设置分区数为 vcore 数为 1:1 ，以便合理利用 CPU 资源

## 解决小文件过多问题

### 场景

### 场景分析

### 优化

解决小文件过多问题也非常简单，在spark当中一个分区最终落盘形成一个文件，那么解决小文件过多问题只需将分区缩小即可。在插入表前，添加coalesce算子指定缩小后的分区个数。那么使用此算子需要注意,coalesce算子缩小分区后那么实际处理插入数据的任务只有一个，<u>可能会导致oom</u>，所以需要适当控制，并且coalesce算子里的参数只能填写比原有数据分区小的值，比如当前表的分区是200，那么填写参数必须小于200，否则无效。当然<u>缩小分区后任务的耗时肯定会变久</u>。

### 结论

合理使用 coalesce 算子

## 数据倾斜-无用的解决方案

面试宝典上数据倾斜无用的解决方案：

使用 Hive ETL 预处理数据。会过滤数据，不推荐

过滤少数导致倾斜的 key 。会过滤数据，不推荐

提高 shuffle 操作并行度 。错误的方案

## 数据倾斜-广播join

Spark join策略中，如果当一张小表足够小并且可以先缓存到内存中，那么可以使用Broadcast Hash Join,其原理就是先将小表聚合到driver端，再广播到各个大表分区中，那么再次进行join的时候，就相当于大表的各自分区的数据与小表进行本地join，从而规避了shuffle。

广播join默认值为10MB，由 `spark.sql.autoBroadcastJoinThreshold` 参数控制

## 数据倾斜-打散大表扩容小表

## SMB JOIN

## Spark 3.0 参数优化-AQE

重要参考：[Adaptive Query Execution Demo](https://docs.databricks.com/_static/notebooks/aqe-demo.html)

- 动态合并shuffle partitions（Dynamically coalescing shuffle partitions）
- 动态切换join策略（Dynamically switching join strategies）
- 动态优化数据倾斜（Dynamically optimizing skew joins）

## Spark 3.0 参数优化-DPP

- [ ] TODO

## Spark 3.0 参数优化-Hint增强

- [ ] TODO