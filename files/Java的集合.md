### 关于Java集合的讨论，以及一些集合特性


List 接口是继承于 Collection接口并定义 一个允许重复项的有序集合。


List分三种：

 - ArrayList：内部是通过数组实现的，它允许对元素进行快随机访问。当从ArrayList的中间位置插入或者删除元素时，需要对数组进行复制、移动、代价比较高。因此，它适合随机查找和遍历，不适合插入和删除。

 - LinkedList: 则是链表结构存储数据的，很适合数据的动态插入和删除，随机访问和遍历速度比较慢。另外，他还提供了List接口中没有定义的方法，专门用于操作表头和表尾元素，可以当作堆栈、队列和双向队列使用。

 - Vector: 通过数组实现的，不同的是它支持线程的同步。访问速度ArrayList慢。


---------------> 代码检验三种 List 的性能
```
    private final static int count=50000;
    
    private static ArrayList arrayList = new ArrayList<>();  
    private static LinkedList linkedList = new LinkedList<>();  
    private static Vector vector = new Vector<>();  
     

    public static void main(String[] args) {
        insertList(arrayList);
        insertList(linkedList);
        insertList(vector);
        
        System.out.println("--------------------");
        
        readList(arrayList);
        readList(linkedList);
        readList(vector);
        
        System.out.println("--------------------");
        
        delList(arrayList);
        delList(linkedList);
        delList(vector);
    }

    private  static void insertList(List list){   
         long start=System.currentTimeMillis();   
         Object o = new Object();   
         for(int i=0;i<count;i++){   
             list.add(0, o);   
         }
        System.out.println(getName(list)+"插入"+count+"条数据，耗时:"+(System.currentTimeMillis()-start)+"ms");
     }   
    
    private  static void readList(List list){   
         long start=System.currentTimeMillis();   
         Object o = new Object();   
         for(int i = 0 ; i < count ; i++){  
                list.get(i);  
            }
        System.out.println(getName(list)+"查询"+count+"条数据，耗时:"+(System.currentTimeMillis()-start)+"ms");
     }  
    
    
    private  static void delList(List list){   
         long start=System.currentTimeMillis();   
         Object o = new Object();   
         for(int i = 0 ; i < count ; i++){  
             list.remove(0);   
            }
        System.out.println(getName(list)+"删除"+count+"条数据，耗时:"+(System.currentTimeMillis()-start)+"ms");
     }  
    
    private static String getName(List list) {  
        String name = "";  
        if(list instanceof ArrayList){  
            name = "ArrayList";  
        }  
        else if(list instanceof LinkedList){  
            name = "LinkedList";  
        }  
        else if(list instanceof Vector){  
            name = "Vector";  
        }  
        return name;  
    }  
```

----------------------> 输出
```
    ArrayList插入50000条数据，耗时:281ms
    LinkedList插入50000条数据，耗时:2ms
    Vector插入50000条数据，耗时:274ms
    --------------------
    ArrayList查询50000条数据，耗时:1ms
    LinkedList查询50000条数据，耗时:1060ms
    Vector查询50000条数据，耗时:2ms
    --------------------
    ArrayList删除50000条数据，耗时:143ms
    LinkedList删除50000条数据，耗时:1ms
    Vector删除50000条数据，耗时:137ms
```





 - 在集合中，我们一般用于存储数据。不过有时在有多个集合的时候，我们想将这几个集合做合集、交集、差集和并集的操作。

 - 在List中，这些方法已经封装好了，我们无需在进行编写相应的代码，直接拿来使用就行。

```
    /**
     * 合集
     * @param ls1
     * @param ls2
     * @return
     */
    private static List<String> addAll(List<String> ls1,List<String>ls2){
        ls1.addAll(ls2);
        return ls1;
    }
    
    /**
     * 交集 （retainAll 会删除 ls1在ls2中没有的元素）
     * @param ls1
     * @param ls2
     * @return
     */
    private static List<String> retainAll(List<String> ls1,List<String>ls2){
        ls1.retainAll(ls2);
        return ls1;
    }
    
    /**
     * 差集 (删除ls2中没有ls1中的元素)
     * @param ls1
     * @param ls2
     * @return
     */
    private static List<String> removeAll(List<String> ls1,List<String>ls2){
        ls1.removeAll(ls2);
        return ls1;
    }
    
    /**
     * 无重复的并集 (ls1和ls2中并集，并无重复)
     * @param ls1
     * @param ls2
     * @return
     */
    private static List<String> andAll(List<String> ls1,List<String>ls2){
        //删除在ls1中出现的元素
        ls2.removeAll(ls1);
        //将剩余的ls2中的元素添加到ls1中
        ls1.addAll(ls2);
        return ls1;
    }
```


 - List数组遍历主要有这三种方法: 普通的for循环，增强for循环(jdk1.5之后出现)，和Iterator(迭代器)。

```
     List<String> list=new ArrayList<String>();
     list.add("a");
     list.add("b");
     list.add("c");
     
     for(int i=0;i<list.size();i++){
         System.out.println(list.get(i));
     }

     for (String str : list) {  
         System.out.println(str);
     }
     
     Iterator<String> iterator=list.iterator();
     while(iterator.hasNext())
     {
         System.out.println(iterator.next());
     }
```

 - 普通的for循环和增强for循环区别不大，主要区别在于普通的for循环可以获取集合的下标，而增强for循环则不可以。
 - 至于Iterator(迭代器）这种也是无法获取数据下标。


 - 不要在 foreach 循环里进行元素的 remove / add 操作。 remove 元素请使用Iterator方式，如果并发操作，需要对 Iterator 对象加锁。


---------------------> 验证代码
```
        List<String> list = new ArrayList<String>();
        list.add("1");
        list.add("2");
        System.out.println("list遍历之前:"+list);
        for (String item : list) {
          if ("2".equals(item)) {
            list.remove(item);
            //如果这里不适用break的话，会直接报错的
            break; 
          }
        } 
        System.out.println("list遍历之后:"+list);
        
        List<String> list1 = new ArrayList<String>();
        list1.add("1");
        list1.add("2");
        System.out.println("list1遍历之前:"+list1);
        Iterator<String> iterator = list1.iterator();
        while (iterator.hasNext()) {
            String item = iterator.next();
            if ("2".equals(item)) {
                iterator.remove();
            }
        }
        System.out.println("list1遍历之后:"+list1);
```

-------------------------> 结果
```
    list遍历之前:[1, 2]
    list遍历之后:[1]
    list1遍历之前:[1, 2]
    list1遍历之后:[1]
```
 - 上述示例中，都正确的打印我们想要的数据，不过在foreach循环中，我在其中是加上了break。如果不加break，就会直接抛出ConcurrentModificationException异常！




















