### 关于Java数组的讨论，以及如何打印数组

 - 随机生成一个整数
```
Random random = new Random();
/** 随机产生一个整数，包括正负数*/
for (int i = 0; i < 100; i++) {
 int r = random.nextInt();
 System.out.println(r);
}
```



 - 随机生成一定范围内的整数
```
Random提供的nextInt方法，可生成一个大于等于0 小于指定值的随机数。
/** 随机产生一个正整数，大于等于0 小于指定值*/
for (int i = 0; i < 100; i++) {
 int r = random.nextInt(100);
 System.out.println(r);
}

如果要生成一个范围值比如，100~200之间随机，采用100加上0到100的随机值就能实现。
for (int i = 0; i < 100; i++) {
 int r = 100 + random.nextInt(100);
 System.out.println(r);
}
```



 - 随机从数组中取一个值
```
原理是通过nextInt生成一个随机的索引，然后从数组中获取指定的索引。
/** 随机从数组中取一个值*/
/** 初始化数组*/
int[] arr = new int[100];
for (int i = 0; i < arr.length; i++) {
    arr[i] = i + 1000;
}

/** 随机索引*/
int index = random.nextInt(arr.length);
/** 随机值*/
int randomValue = arr[index];
System.out.println(" randomValue " + randomValue);
```


 - 随机生成不重复的值
```
随机生成指定个数和范围不重复的值，最简单的方法是随机生成一个值，放入HashSet中，利用Set自带的去重功能，实现去重。数量不到就一直随机值，并且放入HashSet，直到数量满足条件。
/** 随机生成指定个数不重复的值*/
HashSet<Integer> set = new HashSet<>();
while (set.size() < 10) {
 set.add(random.nextInt(100));
}
for (Integer i : set) {
 System.out.println("i " + i);
}
```



 - 案例 ！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！
```
    /*** 
     * @Todo: 测试
     * @Params: [] 
     * @Return: java.lang.String 
     */ 
    @RequestMapping(value = "/demo", method = RequestMethod.GET)
    public String demo()
    {
        /** todo 产生随机数组，并且排序 **/
        // 产生随机数
        int min = 100;
        int max = 10000;
        int randomNumber1 = (int) Math.round(Math.random()*min);
        int randomNumber2 = (int) Math.round(Math.random()*max);

        // 产生随机数组
        int[] result = new int[10];
        for (int i = 0; i < 10; i++) {
            result[i] = (int) Math.round(Math.random()*randomNumber1+randomNumber2);
        }

        // 排序
        java.util.Arrays.sort(result);

        System.out.println(Arrays.toString(result));// todo 打印数组

        return "测试随机数组范围：" + randomNumber1 + "----->" + randomNumber2 + " \n";
    }
```



