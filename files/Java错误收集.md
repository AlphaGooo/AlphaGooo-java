### 关于一些Java错误，已经相应的解决方案

#### java.lang.IndexOutOfBoundsException 错误解决

 - 示例
```
java.lang.IndexOutOfBoundsException : Invalid array range: 10 to 10
```

 - 原因

什么意思呢？就是有个数组要取出10位置的值，程序发现那个位置也就是10位置那里并没有值，就会报这个错。

也有人说是越界错误，也是可以理解的，数组越界了，那里当然也没有值可以给你取得的。

所以归根到底是要取的值是空的。


 - 解决！！！！！！！！！！！！！！！！！！
```
// 确定10位置有值，采取进行操作
if (array.size > 10) {
    // todo sometiong
}
```

#### not functional interface

 - 原因

函数式接口(Functional Interface)是Java 8对一类特殊类型的接口的称呼。 

java.util.function中定义了几组类型的函数式接口以及针对基本数据类型的子接口:

 - Predicate -- 传入一个参数，返回一个bool结果， 方法为boolean test(T t)
 - Consumer -- 传入一个参数，无返回值，纯消费。 方法为void accept(T t)
 - Function -- 传入一个参数，返回一个结果，方法为R apply(T t)
 - Supplier -- 无参数传入，返回一个结果，方法为T get()
 - UnaryOperator -- 一元操作符， 继承Function,传入参数的类型和返回类型相同。
 - BinaryOperator -- 二元操作符， 传入的两个参数的类型和返回类型相同， 继承BiFunction

 - 解决！！！！！！！！！！！！！！！！！！
 
--------> https://colobu.com/2014/10/28/secrets-of-java-8-functional-interface/






