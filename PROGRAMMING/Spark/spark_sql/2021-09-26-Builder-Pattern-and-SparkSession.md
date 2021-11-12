# SparkSession 和建造者模式

> 建造者模式（Builder Pattern）使用多个简单的对象一步一步构建成一个复杂的对象。这种类型的设计模式属于创建型模式，它提供了一种创建对象的最佳方式。
>
> 一个 Builder 类会一步一步构造最终的对象。该 Builder 类是独立于其他对象的。
>
> Ref. [建造者模式 | 菜鸟教程](https://www.runoob.com/design-pattern/builder-pattern.html)

## SparkSession 类图

```puml
@startuml

'' define
class SparkDemo {
  +main(): void
}
class Builder as "SparkSession.Builder" {
  -options: HashMap[String, String]
  +config(key, value): Builder
  +getOrCreate(): SparkSession
}
class SparkSession {
  -sparkContext: SparkContext
  -sessionState: SessionState
  ...
  +udf(): UDFRegistration
  +createDataFrame(...): DataFrame
  +sql(sqlText: String): DataFrame
  +read(): DataFrameReader
  ...()
}

class SparkContext {

}

class SessionState {
  +conf: SQLConf
}

class DataFrame
class DataFrameReader {
  +option(key: String, value: String): DataFrameReader
  ...()
  +csv(path: String): DataFrame
  ...()
  +textFile(path: String): Dataset[String]
}

class Dataset<T>

'' Association
SparkDemo ..> Builder: asks
Builder ..> Builder: 迭代生成更新后的 Builder
Builder ..> SparkSession: getOrCreate 创建
SparkSession --> SparkContext: 由...组成
SparkSession --> SessionState
SparkSession ..> DataFrame: 使用
SparkSession ..> DataFrameReader: 使用
DataFrameReader ..> DataFrameReader: 迭代生成更新后的 DataFrameReader
DataFrameReader ..> DataFrame
DataFrameReader ..> Dataset
DataFrame -- Dataset: type DataFrame = Dataset[Row]

@enduml
```

![](http://www.plantuml.com/plantuml/png/VPAzRXD14CVxVOfHcbn4V0zmWYWGow808UnGHIbMlh6pydqSktk62D6bI8LIM1IaeA2XGGA92WlbPM8VZy7iVPmdric5PStyVtF_cPqvDbPgcyUH4Flx4E949IZ6aJG6HfdKipx6ANmG08zYgHBl881vgaBniMQUvIeAKOCqi5Vo8pH6fObV2tjbRI_DB2LD0C-bkNWfixEHrIgP7aBrV-w-FqwJYPfwCxmyXBcCSYIl-YjEdg9zfKyqIekk2sxMTiEJbR5ncPCqiVZUKX6BIhL2HrPQ99L5fFg-xtppSEBytlG7GvmgOxLqevGDbytqfPK3BMFqg830DdQ8UHjvz3jrxlMisuX66NeyEQG4wge1xu1cOyCrpTDmJ61zar0_9VczVa7uf0MPRnjpowgsMfLRGzDnlOuctD6hipPpBvFseelcd9jYe2BiWWtQi-OmUFDEU7nwL5xgKsFIiQfsiJbKtpzgRYO0QMP6rD53vT_TZ_lbjsBnTNrzixxzlVxyStNpgVXorH2y2lXH1S3E45RNjwlb7y41wFLS1J-wOl6BfYwMLsJMmVAZuwhptZnT0FT_xuh5zqw4xw85j_8TxAw7s29tVwrRhVQrqMZS9Xc0lSmGDjAJTk_3zDsv4CUOX7aS_GS0)

UML 画图参考：[UML类图与类的关系详解](https://www.cnblogs.com/pangjianxin/p/7877868.html) 

源码参考：spark-sql v2.1.1

## SparkSession 的建造者模式思想

- **意图**

  将一个复杂的 SparkSession 构建与其表示相分离，使得同样的构建过程可以创建不同的表示。

- **主要解决**

  复杂 SparkSession 的构建要考虑到 Thread 的 SparkSession 以及 SparkContext 以及 conf ，

- **何时使用**

- **如何解决**

- **关键代码**

  建造者：`Builder.getOrCreate()` ；导演： `SparkDemo.main()`

- **应用实例**

  SparkSession 的建造者模式

- **优点**

- **缺点**

- **使用场景**

- **注意事项**
