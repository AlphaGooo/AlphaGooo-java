### 关于Java单例模式的讨论，以及一些高效的应用案例

---> https://www.runoob.com/design-pattern/singleton-pattern.html

单例模式（Singleton Pattern）是 Java 中最简单的设计模式之一。

 - 这种模式涉及到一个单一的类，该类负责创建自己的对象，同时确保只有单个对象被创建。（最佳的状态是，一个单例只完成一件事）

 - 小小的单例模式可以牵扯到很多东西，比如 多线程是否安全，是否懒加载，性能等等。

 - 写单例模式，需要注意的问题：线程安全、延迟加载、序列化与反序列化安全。

 - 一般来说，单例模式有五种写法：懒汉、饿汉、双重检验锁、静态内部类、枚举。


#### 饿汉模式
```
public class SingletonHungry
{
    private SingletonHungry() {}

    private final static SingletonHungry singletonHungry = new SingletonHungry();

    public static SingletonHungry getInstance()
    {
        return singletonHungry;
    }
    /* 在Hungry类中，定义了四个byte数组，当代码一运行，这四个数组就被初始化，并且放入内存了，如果长时间没有用到getInstance方法，不需要Hungry类的对象，这会是一种浪费 */

    private byte[] data1 = new byte[1024];
    private byte[] data2 = new byte[1024];
    private byte[] data3 = new byte[1024];

    public String hungryName = "hungry_1";


}
```


#### 懒汉模式
```
public class SingletonLazyman
{
    private static boolean flag = false;

    private SingletonLazyman()
    {
        // 处理有人利用 反射 破坏单例模式
        synchronized (SingletonLazyman.class) {
            if (flag == false) {
                flag = true;
            } else {
                throw new RuntimeException("不要试图用反射破坏单例模式！");
            }
        }
        /* flag 并不能完全避免单例模式被反射破坏，因为可以利用反射修改flag的值 */
    }

    // 懒汉式单例的极端情况可能出线指令重排，增加一个 volatile 关键字，可以避免这个问题
    private volatile static SingletonLazyman singletonLazyman;

    public static SingletonLazyman getInstance()
    {
        if (singletonLazyman == null) {
            synchronized (SingletonLazyman.class) {
                if (singletonLazyman == null) {
                    singletonLazyman = new SingletonLazyman();
                }
            }
        }

        return singletonLazyman;
    }

    /* DCL懒汉式的单例，保证了线程的安全性，又符合了懒加载，只有在用到的时候，才会去初始化，调用效率也比较高 */

    // 私有变量
    private String word1 = "SingletonLazyman type ";
    private String word2 = "is DCL + Volatile ";
    // 公共函数
    public String getName()
    {
        return word1 + word2;
    }



}
```


#### 静态内部类 （推荐使用）
```
public class SingletonHolder
{
    private SingletonHolder() {}

    public static SingletonHolder getInstance()
    {
        return InnerClass.singletonHolder;
    }

    private static class InnerClass
    {
        private static final SingletonHolder singletonHolder = new SingletonHolder();
    }

    /* Holder 是饿汉式（DCL）的改进版本，同样也是在类中定义static变量的对象，并且直接初始化。不过是移到了静态内部类中，十分巧妙。既保证了线程的安全性，同时又满足了懒加载。 */

    private String word1 = "my name is ";
    private String word2 = "class lazyman - holder ";

    public String getDesc()
    {
        return word1 + word2;
    }



}
```


#### 枚举模式（推荐使用）
```
public enum SingletonEnum
{
    instance;
    public SingletonEnum getInstance()
    {
        return instance;
    }

    // 获取/更新 - 名字
    private String name = "my name is singleton(enum)";
    public String getName()
    {
        return name;
    }
    public void setName(String name)
    {
        this.name = name;
    }
}
```


 - 考虑到线程安全、反射强行调用构造器和反序列化创造新对象等问题，单例模式最佳方案是 枚举模式，但最常见的是 静态内部类。

 - 枚举模式在 Android 平台是不受推荐的。






