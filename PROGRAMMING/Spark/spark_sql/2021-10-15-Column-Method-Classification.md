# Column 类的方法整理

> `Column` represents a column in a [Dataset](https://jaceklaskowski.gitbooks.io/mastering-spark-sql/content/spark-sql-Dataset.html) that holds a Catalyst [Expression](https://jaceklaskowski.gitbooks.io/mastering-spark-sql/content/spark-sql-Expression.html) that produces a value per row.
>
> Ref. https://jaceklaskowski.gitbooks.io/mastering-spark-sql/content/spark-sql-Column.html

这里整理的都是以 Column 对象作为输入（包含 `self` `this` 情况）并且以 Column 对象最为输出的方法。

## 获得列 get column

| Method | Package Class                  | Description |
| ------ | ------------------------------ | ----------- |
| col    | org.apache.spark.sql.functions |             |
| column | org.apache.spark.sql.functions |             |
| lit    | org.apache.spark.sql.functions |             |

## 新增列 add column

## ~~Column as complex expression~~

一个 Column 实例要和包裹它的方法配合，

`org.apache.spark.sql.Column`

`org.apache.spark.sql.functions`

## 修改列的元数据 modify column metadata

| Method | Package Class | Description |
| ------ | ------------- | ----------- |
| as     |               |             |
| cast   |               |             |



## 列作为判断（true or false） get if value

| Method | Package Class | Description |
| ------ | ------------- | ----------- |
|        |               |             |
|        |               |             |
|        |               |             |
|        |               |             |
|        |               |             |
|        |               |             |
|        |               |             |

## 对列排序 order column

| Method | Package Class | Description |
| ------ | ------------- | ----------- |
| asc    |               |             |
| desc   |               |             |

## 一对一映射 column value function

| Method | Package Class | Description |
| ------ | ------------- | ----------- |
|        |               |             |
|        |               |             |

## 多对一映射（聚合） column value aggregation function

| Method | Package Class | Description |
| ------ | ------------- | ----------- |
| avg    |               |             |
| max    |               |             |
| min    |               |             |
| sum    |               |             |
| first  |               |             |
| last   |               |             |





类 SQL

| Method                                                  | Description |
| ------------------------------------------------------- | ----------- |
| `def === (other: Any): Column`                          |             |
| `def =!= (other: Any): Column `                         |             |
| `def !== (other: Any): Column`                          |             |
| `def > (other: Any): Column`                            |             |
| `def < (other: Any): Column`                            |             |
| `def <= (other: Any): Column`                           |             |
| `def >= (other: Any): Column`                           |             |
| `def <=> (other: Any): Column`                          |             |
| `def || (other: Any): Column`                           |             |
| `def && (other: Any): Column`                           |             |
| `def as[U : Encoder]: TypedColumn[Any, U]`              | 起别名      |
| `def between(lowerBound: Any, upperBound: Any): Column` |             |
|                                                         |             |
| `def notEqual(other: Any): Column`                      |             |

