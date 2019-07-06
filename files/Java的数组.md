### 关于Java数组的讨论，作为容器它的一些特性


-----------------> https://zhuanlan.zhihu.com/p/40969337


 - 所谓数组，就是相同数据类型的元素按一定顺序排列的集合，把有限个类型相同的变量用一个名字命名，然后用编号区分他们的变量的集合。

 - 这个名字称为数组名，编号称为下标，组成数组的各个变量称为数组的元素，也称为数组的分量，有时也称为下标变量。

 - 数组是一种非常重要的数据类型，属于引用类型，数组是我们接触的第一个容器，数组是长度固定的容器。

 - 由于Java中的数据类型分为两种：基本类型和引用类型。所以数组也有两种类型的：基本类型的数组和引用类型的数组。

```
    /*** 
     * @Todo: 随机一个二维数组
     * @Params: [] 
     * @Return: int[][] 
     */ 
    public static int[][] randomTwoDimensionArray()
    {
        // 可以在定义时不指定第二维的长度
        int[][] result = new int[3][];

        // 第二维的长度可以不固定，就不规则二维数组
        result[0] = new int[1];
        result[1] = new int[2];
        result[2] = new int[3];

        // 给二维数组赋值
        int value = 1;
        for (int i=0; i<result.length; i++) {
            for (int j=0; j<i+1; j++) {
                result[i][j] = value;
                value++;
            }
        }
        
        return result;
    }
```


 - 数组按下标个数分类有一维数组，二维数组等，二维以上数组通常称为多维数组。

```
    /*** 
     * @Todo: 随机一个多维数组
     * @Params: [] 
     * @Return: int[][][] 
     */ 
    public static int[][][] randomManyDimensionArray()
    {
        // 指定多维数组各节点长度
        int result[][][] = new int [3][4][5];

        // 给数组赋值
        int i, j, k;

        for (i=0; i<3; i++) {
            for (j=0; j<4; j++) {
                for (k=0; k<5; k++) {
                    result[i][j][k] = randomNumber();
                }
            }
        }

        return result;
    }
```


 - 在Java中，数组是固定长度不能扩展的。但是在现实情况中，动态地扩展数组以适应程序的要求是非常常见的。

```
    /*** 
     * @Todo: 给数组添加新元素
     * @Params: [array, column] 
     * @Return: int[]
     */
    public int[] formatArrayAddColumn(int[] array, int column)
    {
        // 获取数组长度
        int length = array.length;


        // 给数组添加元素
        array = Arrays.copyOf(array, array.length + 1);
        array[array.length - 1] = column;

        java.util.Arrays.sort(array);

        return array;
    }
```


 - 由于Java中数组的一些固有特性，限制了我们对数组的灵活运用。所以在Java中，我们可以使用ArrayList来代替数组的使用。

```
    /*** 
     * @Todo: 随机一个一维列表
     * @Params: [] 
     * @Return: java.util.List<java.lang.String> 
     */ 
    public static List<String> randomArrayList()
    {
        // 定义列表对象，长度不限，其保存的数据类型为字符串，注意声明方式
        // 之所以使用List来定义ArrayList，是因为List统一了接口
        List<String> result = new ArrayList<String>();

        // 调用列表对象的add方法，往列表中添加数据
        result.add("id");
        result.add("name");
        result.add("sex");
        result.add("age");
        result.add("from");

        // 删除第3条数据
        result.remove(2);
        // remove的重载方法，删除 age 这条数据
        result.remove("age");

        // 使用contains来判断是否仍然包含数据 age
        if (result.contains("age") == false) {
            result.add("ageAfterAdd");
        }

        return result;
    }


    /*** 
     * @Todo: 获取一个指定的固定长度多维数组
     * @Params: [s_len] 
     * @Return: java.util.List<java.lang.String>[][] 
     */ 
    public List<String>[][] getArrayList(int s_len)
    {
        // 定义多维数组，按照输入的长度建立
        List<String>[][] result = new ArrayList[s_len][s_len];

        // 给数组赋值
        for (int i = 0; i < s_len; i++) {
            for (int j = 0; j < s_len; j++) {
                result[i][j] = new ArrayList<>();
            }
        }

        return result;
    }
```






























