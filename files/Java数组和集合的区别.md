### 关于Java数组和集合的讨论，区分两者的差别

---------------------------> http://blog.qianlicao.cn/translate/2016/03/09/array-vs-arraylist

---------------------------> https://blog.csdn.net/seabreezesuper/article/details/52471087

####【定义】
 - Array 和 ArrayList 两者都是 Java 中重要的数据结构, 在Java程序中运用非常频繁。
 - 尽管ArrayList 内部是由一个 Array 实现的, 但是知道 Array 和 ArrayList 之间的区别是成为一个优秀的java 开发者的关键。


####【差异】
- Array 是本地的程序设计组件或者数据结构。但是ArrayList是一个来自Java集合类的类,一个接口 。

- 在性能上，ArrayList 所需要的内存要比 Array 大。（一个int[] 的数组会比ArrayList节省20个int 变量的大小,因为对象的基本数据在ArrayList和包装类上需要开销）

- 在时间复杂度上，ArrayList 要比 Array 要高一些。（ArrayList 包含了创建一个新的array 和将老的array的数据拷贝到新的array里，操作复杂度会高一些）

- ArrayList 是类型安全的,因为它支持泛型(Generics) 允许编译器检查 ArrayList 里所包含的对象是否是正确的类型。
- Array 并不支持泛型，这代表在编译时期检查array 所保存对象的类型是不可能的。

- ArrayList比简单的Array要灵活的多,因为 ArrayList 是动态的,它可以在需要的时候扩大自己的内存,这是一个 array 不可能做到的。

- int[]数组是合法的,但是一个int型的ArrayList是不合法的。（从Java5开始，不能保存基本类型到ArrayList里）

- ArrayList 提供比array更多的方式来迭代一个接一个的访问所有的元素。

- Array 仅仅提供一个length 属性来告诉你array里有多少个插槽。
- ArrayList提供一个size()方法来告诉你当前时间点ArrayList存储了多少个元素。（size() 总是和length不同的,它也是ArrayList的容量）

- ArrayList和array的另外一个重要的区别，就是Array可以使多维度的，ArrayList并不支持允许你指定维度。


####【概述】
- Array 是静态的,所以一个数据一旦创建就无法更改他的大小。
- ArrayList 是Java集合框架类的一员,可以称它为一个动态数组。


####【结论】
- 所以, 如果需要一个数组可以重新定义他的大小。你应该使用 ArrayList。 
- 这是array 和ArrayList 的基本的不同。


####【ArrayList和Array的常用场景】

1. Array数组一般不能直接追加新元素，因为Java中的数组是固定长度的。

```
// todo 定义一个数组，长度是固定的
int[] intArray = { 1, 2, 3, 4, 5 };
 
// 一般不能直接打印
System.out.println(intArray);  // [I@7150bd4d

// todo 需要转义字符才能打印
String intArrayString = Arrays.toString(intArray);
System.out.println(intArrayString);  // [1, 2, 3, 4, 5]
```




2. ArrayList集合是比较方便地进行增删改的动态数组，而且长度也不是固定的。

```
// todo 检查数组中是否包含某个值
String[] stringArray = { "a", "b", "c", "d", "e" };
boolean b = Arrays.asList(stringArray).contains("a");
System.out.println(b);  // true


// todo 连接两个数组
int[] intArray = { 1, 2, 3, 4, 5 };
int[] intArray2 = { 6, 7, 8, 9, 10 };
int[] combinedIntArray = ArrayUtils.addAll(intArray, intArray2);


// todo 将数组中的元素以字符串的形式输出
String j = StringUtils.join(new String[] { "a", "b", "c" }, ", ");
System.out.println(j);
// a, b, c


// todo 将Array转化成Set集合
Set<String> set = new HashSet<String>(Arrays.asList(stringArray));
System.out.println(set);  //[d, e, b, c, a]


// todo 数组翻转
int[] intArray = { 1, 2, 3, 4, 5 };
ArrayUtils.reverse(intArray);
System.out.println(Arrays.toString(intArray));   //[5, 4, 3, 2, 1]


// todo 从数组中移除一个元素
int[] intArray = { 1, 2, 3, 4, 5 };
int[] removed = ArrayUtils.removeElement(intArray, 3);//create a new array
System.out.println(Arrays.toString(removed));


// todo 将一个int值转化成byte数组
byte[] bytes = ByteBuffer.allocate(4).putInt(8).array();
 
for (byte t : bytes) {
  System.out.format("0x%x ", t);
}
```





















