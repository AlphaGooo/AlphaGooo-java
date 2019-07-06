### 关于Java的哈希数组的讨论，以及它的一些特性

-----------------> https://www.jianshu.com/p/a17b4717a721

 - HashMap是Java程序员使用频率最高的用于映射(键值对)处理的数据类型。。。

 - Map 提供了一个通用的元素存储方法，Map集合类用于存储元素对（称作“键”和“值”），其中每个键映射到一个值。

 - Java为数据结构中的映射定义了一个接口java.util.Map，此接口主要有四个常用的实现类，分别是HashMap、Hashtable、LinkedHashMap和TreeMap。

 - HashMap 根据键的hashCode值存储数据，大多数情况下可以直接定位到它的值，因而具有很快的访问速度，但遍历顺序却是不确定的。

 - HashMap 最多只允许一条记录的键为null，允许多条记录的值为null。

 - HashMap非线程安全，即任一时刻可以有多个线程同时写HashMap，可能会导致数据的不一致。
 - 如果需要满足线程安全，可以用 Collections 的 synchronizedMap 方法使 HashMap 具有线程安全的能力，或者使用 ConcurrentHashMap。

 - 从结构实现来讲，HashMap是数组+链表+红黑树（JDK1.8增加了红黑树部分）实现的。
 - HashMap就是使用哈希表来存储的，为解决冲突可以采用开放地址法和链地址法等来解决问题，Java中HashMap采用了链地址法。



-----------> 示例代码
```
        // 初始化 hashMap 数组
        HashMap<String, String> result = new HashMap<>();

        // 给数组填充数据 ---> 普通字段
        result.put("test", "test");
        result.put("demo", "demo");
        // put 方法会直接覆盖已存在的 value
        result.put("name", "alphaGooo");
        result.put("name", null);
        // putIfAbsent 方法会判断，如果 key 不存在 或者 value 为null，才会覆盖
        result.putIfAbsent("name", "");
        result.put("name", "alphaGooo");
        result.putIfAbsent("name", "alphaGoooNew");
        // remove 方法可以移除指定的元素
        result.remove("test");
        // replace 方法可以替换指定元素
        // 对于存在的key，调用replace方法，会替换原来的value，并返回旧value，这和put的效果是一样的
        // 对于不存在的key，replace方法什么都不做
        // put在key不存在时将新key-value加入map
        result.replace("name", "alphaGoooNewNew");

        // 给数组填充数据 ---> 一维数组 Array
        int[] array10 = randomArray10();
        result.put("array", Arrays.toString(array10));

        // 给数组填充数据 ---> 一维数组 ArrayList
        List<String> arrayList = DemoBusiness.randomArrayList();
        result.put("arrayList", arrayList.toString());

        // 给数组填充数据 ---> 一维数组 hashMap
        HashMap<String, String> hashMap = randomHashMap();
        result.put("hashMap", hashMap.toString());
        HashMap<String, String> hashMap1 = randomHashMap();
        result.put("hashMap1", hashMap1.toString());

        // 获取数组元素
        String name = result.get("name");
        System.out.println(name);
        String test = result.getOrDefault("test", "test is deleted");
        System.out.println(test);

        // 打印数组
        System.out.println(result);

        // 判断数组元素key/value 是否存在
        if (result.containsKey("test") == false) {
            System.out.println("key is test was not exits");
        } else {
            System.out.println("key is test was exits");
        }
        if (result.containsValue("demo") == false) {
            System.out.println("value is demo was not exits");
        } else {
            System.out.println("value is demo was exits");
        }
```

-----------> Map接口，常用方法
```
public interface Map<K,V> {

    //返回Map中的key--value的数目
    int size();

    //如果Map不包含任何key--value，则返回 true
    boolean isEmpty();

    //如果Map中包含指定key的映射，则返回true
    boolean containsKey(Object key);

    //如果此Map将一个或多个键映射到指定值，则返回 true
    boolean containsValue(Object value);

    //返回与指定键关联的值
    V get(Object key);

    //将指定值与指定键相关联
    V put(K key, V value);

    //从Map中删除键和关联的值
    V remove(Object key);

    //将指定Map中的所有映射复制到此map
    void putAll(java.util.Map<? extends K, ? extends V> m);

    //从Map中删除所有映射
    void clear();

    //返回Map中所包含键的Set集合
    Set<K> keySet();

    //返回 map 中所包含值的 Collection集合。
    Collection<V> values();

    //返回Map中所包含映射的Set视图。Set中的每个元素都是一个 Map.Entry 对象
    Set<java.util.Map.Entry<K, V>> entrySet();

    //比较指定对象与此 Map 的等价性
    boolean equals(Object o);

    //返回此 Map 的哈希码
    int hashCode();

    //Map集合中存储key--value的对象Entry，在Map集合内形成数组结构
    interface Entry<K,V> {

        V getValue();

        V setValue(V value);

        boolean equals(Object o);

        int hashCode();
    }
}
```



