# UserDefinedFunction

- 为什么 udf 会自动将输入参数 Column 类型转成 String ？ udf 输出参数 case class 转成 struct StructType ？hack udf

  https://sparkbyexamples.com/spark/convert-case-class-to-spark-schema/

  因为创建 udf 的时候传了一个函数的对象，在 udf 方法里面会将 scala TypeTag 转成 DataType

```scala
// org.apache.spark.sql.functions

/**
 * Defines a Scala closure of 1 arguments as user-defined function (UDF).
 * The data types are automatically inferred based on the Scala closure's
 * signature. By default the returned UDF is deterministic. To change it to
 * nondeterministic, call the API `UserDefinedFunction.asNondeterministic()`.
 *
 * @group udf_funcs
 * @since 1.3.0
 */
def udf[RT: TypeTag, A1: TypeTag](f: Function1[A1, RT]): UserDefinedFunction = {
  val ScalaReflection.Schema(dataType, nullable) = ScalaReflection.schemaFor[RT] // 返回值的 scala TypeTag 转成 DataType
  val inputEncoders = Try(ExpressionEncoder[A1]()).toOption :: Nil
  val udf = SparkUserDefinedFunction(f, dataType, inputEncoders) // 参数的 scala TypeTag 转成 DataType
  if (nullable) udf else udf.asNonNullable()
}
```

以一个参数的 udf 为例



```
change log
2021-11-12 10:06 ADD 研究 udf 的参数以及返回值
```

