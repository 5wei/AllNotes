# DSL(Domain Specific Language)风格语法

好文：[看完这篇彻底理解Spark SQL DSL——让那些无聊的API去死吧](https://zhuanlan.zhihu.com/p/373497278)

好处：对 Spark 的控制粒度很细，包括对并行度、checkpoint等。

通过map、flatMap..算子操作数据。常用 DSL API 对 DataFrame 进行**过滤**、**列裁剪**、**去重**

```scala
// 过滤使用 filter 、 where 函数
df = filter(" age > 25 ").show
```

```scala
// 列裁剪使用 selectExpr 、 select 函数
df.selectExpr("sum(age) sum_age").show()

import org.apache.spark.sql.functions._
df.select(sum('age)).show
```

```scala
// 去重使用 distinct 、 dropDuplicates 函数
// distinct去重: 所有列的值都相同，这两行数据才算重复
// dropDuplicates去重: 只要指定列的数据相同,这两行数据才算重复
df.distinct().show
df.dropDuplicates("name").show
```



DSL 的 operator 分两个层级：

1. DataSet

   以 `Dataset` 中的方法为主，底层使用 [`LogicalPlan` Node](hack/2021-10-25-LogicalPlan.md)

2. Column

   以 `Column` and `functions` 中的方法为主，底层使用 [`Expression` Node](hack/2021-10-18-Expression.md)

DSL 与 SQL Query 的关系：两者都转化成 Logical Plan



Join duplicated columns [How to rename duplicated columns after join?](https://newbedev.com/how-to-rename-duplicated-columns-after-join)
