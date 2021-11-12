# RDD、DataFrame、DataSet比较

---

- 什么是DataFrame

  DataFrame可以当做一个二维表格,有schema信息<有列名、列类型>
  
  DataFrame只关注列不关注行的类型,不管每个元素<每行>是什么类型，表现出来都是Row类型
  
- 什么是DataSet

  DataSet可以当做一个二维表格,有schema信息<有列名、列类型>
  
  DataSet即关注列也关注行的类型,每个的数据类型是啥,表现出来就是啥

---

RDD、DataFrame、DataSet的联系

1、RDD、DataFrame、DataSet都是弹性分布式数据集
2、RDD、DataFrame、DataSet都是惰性执行的，都需要调用action算子之后才会真正执行
3、RDD、DataFrame、DataSet都有分区
4、RDD、DataFrame、DataSet有很多共同的函数: map、flatMap、filter..
5、RDD、DataFrame、DataSet都是数据在内存与磁盘中动态存储

---

DataFrame与DataSet的区别

- DataFrame是弱类型（Row类型）,DataSet是强类型（一行数据的实际类型）

- DataFrame是运行期安全,编译器不安全。DataSet是编译器安全,运行期也安全

- DataFrame与DataSet的使用时机

  - 如果是将rdd转成sparksql编程，
  
    此时如果rdd里面的元素类型是样例类,转成DataSet或者DataFrame都可以
    
    此时如果rdd里面的元素类型元组,推荐转成DataFrame,可以通过toDF指定列名
    
  - 如果想要使用map、flatMap这种写函数的强类型算子,推荐使用DataSet

---

为什么 DataFrame 底层实现是 RDD，却比 RDD 更快

> 其实是这样的，因为 df 是由 spark 自己转换成 RDD 的，那么 spark 自然会用最合适的、最优化的方式转换成 RDD，因为它比任何人都清楚怎么才能更高效，
>
> 对比我们自己操作 RDD 去实现各种功能，大部分情况下我们的作法可能不是最优，自己玩不如作者玩，所以说 df 性能高于 RDD
>
> 举个简单例子：
>
> ...
>
> ——[spark教程(九)-sparkSQL 和 RDD-DF-DS 关系](http://www.manongjc.com/detail/12-kejjjjlwsnfjxuh.html)

---



```
change log

```

