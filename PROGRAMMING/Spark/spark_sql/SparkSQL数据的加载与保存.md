# SparkSQL数据的加载与保存

```
1、文件读取:
    1、spark.read
        .format() --指定文件读取格式[csv/json/text/parquet/orc]
        .option().option().. --指定读取的参数
        .load(path) --指定加载路径的数据
    在读取文件的时候,一般只有csv文件才需要配置option,csv文件常用的option:
        sep: 指定字段之间的分隔符
        header: 指定是否以文件的第一行作为列名
        inferSchema: 指定是否自动推断字段的类型
    2、spark.read[.option()].csv/json/csv/parquet/orc
2、mysql数据读取
    1、spark.read
        .format() --指定文件读取格式[jdbc]
        .option().option().. --指定读取的参数<账号、密码、driver、表、url>
        .load() --指定加载路径的数据
    2、spark.read.jdbc(url,表名,参数设置): 此种方式读取jdbc的时候分区数 = 1,只能用于数据量小的场景
       spark.read.jdbc(url,表名,分区条件参数,参数设置): 此种方式读取jdbc的时候分区数=分区条件参数数组的元素个数。<不常用>
            val arr = Array("age<20","age>=20 and age<40","age>=40")
            spark.read.jdbc("jdbc:mysql://xx:3306/test","person",arr,参数设置)
        spark.read.jdbc(url,表名,mysql字段名,lowerBound,uperBound,分区数,参数设置): <工作常用>
            此种方式读取的时候,分区数 = (uperBound-lowerBound) > 分区数 ? 分区数 : uperBound-lowerBound
2、数据保存:
    1、df/ds.write
            .mode() --指定写入模式
            .format() --指定数据写入的格式[csv/json/parquet/orc/jdbc]
            .option() --指定数据写入的时候需要的参数
                csv文件写入的时候指定的option:
                    header: 写入的时候是否将列名也写入
                    sep: 写入的时候指定字段之间的分隔符
            .save() --数据保存
    2、df/ds.write.mode(..).csv/json/parquet/orc/jdbc
    常用的写入模式:
        SaveMode.Overwrite: 如果指定的路径/表已经存在，则覆盖历史数据<数据写入HDFS的时候使用>
        SaveMode.Append: 如果指定的路径/表已经存在,则追加数据<数据写入mysql的时候使用>
            如果写入mysql的时候,主键数据已经存在,此时不能使用append,需要通过foreachPartitions对数据进行更新写入
3、hive的数据读取和保存
    1、读取数据: 
        1、在创建SparkSession的时候通过enableHiveSupport需要开启hive的支持: 
            SparkSession.builder().master(..).appName(..).enableHiveSupport().getOrCreate
        2、直接在代码中通过spark.sql("查询hive表数据")
    2、保存数据到hive表:
        df/ds.write.mode(..).saveAsTable("hive表") <不常用,一般都是将数据写入HDFS>
4、多维聚合:<对多个维度按照不同的组合进行聚合>
    grouping sets：
        语法:  select 维度1,维度2,..,聚合函数  from  表 group by 维度1,维度2,.. grouping sets( (维度1),(维度1,维度2),(..) )
            grouping sets后面的字段名必须是group by后面的字段
    案例:
        select A,B,C,count(1) from person group by A,B,C grouping sets( (A),(A,B),(B,C),(A,B,C) )
        等价于:
        select A,null B,null C,count(1) from person group by A
        union
        select A,B,null C,count(1) from person group by A,B
        union
        select null A,B,C,count(1) from person group by B,C
        union
        select A,B,C,count(1) from person group by A,B,C
```

DateFrameWriter 中 insertInto 与 saveAsTable 的比较：

|      | `insertInto`         | `saveAsTable`  |
| ---- | -------------------- | -------------- |
| 建表 | 需要提前在 hive 建表 | 不需要建表     |
| 插入 | 字段顺序匹配插入     | 字段名匹配插入 |

