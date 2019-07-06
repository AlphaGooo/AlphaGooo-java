### 关于如何给Java数组添加元素，以及一些高效的解决方案


在 java 的世界里，一般数组是不能添加元素的，因为他们在初始化时就已定好长度了，不能改变长度。


方案1: 创建一个比原来数组长度大1的临时数组，复制并添加元素
```
        // 静态定义一维数组
        int[] scores={90,70,50,80,60,85};

		//向一维数组scores末尾中添加一个学生的成绩 75.
		/*
		思路:
			1. 先创建一个比原来scores数组长度大1的临时数组 tempArray
			2. 将scores数组的每一个值复制到 tempArray
			3. 然后将 成绩为 75 赋值到 tempArray的新增最后的索引位置
			4. 最后将tempArray地址指针引用赋值给 scores;
		*/
        
        // 创建一个比原来数组长度大1的临时数组
        int[] tempArray=new int[scores.length+1];
        
        // 把原来数组的元素复制到临时数组
        for(int i=0;i<scores.length;i++){
			tempArray[i]=scores[i];
		}
		
		// 再把需要添加的元素补充上
		tempArray[scores.length]=75;
		
		// 临时数组覆盖原来的数组，达到数组添加元素的效果
		scores=tempArray;
		
		
		// 打印输出，看结果
		for(int i=0;i<scores.length;i++)
		{
			System.out.print(scores[i]+",");
		}
```

方案2: 可以使用Arrays.copyOf(array, size)从现有阵列构建新阵列。
```
    // 创建数组
    int[] array = new int[] {1, 2, 3};
    
    // 打印
    System.out.println(Arrays.toString(array));
    
    // copy数组，并且构建一个比原来大1的数组
    array = Arrays.copyOf(array, array.length + 1); //create new array from old array and allocate one more element
    
    // 往 copy数组 添加元素
    array[array.length - 1] = 4;
    
    // 打印
    System.out.println(Arrays.toString(array));
```


案例 ！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！
```
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


        /** todo 调用其他类的方法，自定义排序 **/
        // 数组另外赋值
        int[] resultSort = result;
        java.util.Arrays.sort(resultSort);

        // 获取数组长度
        int length = resultSort.length;

        // 调用其他类方法，获取返回值
        DemoBusiness demo = new DemoBusiness();
        int demoResult = demo.hello();

        // 给数组添加元素
        resultSort = Arrays.copyOf(resultSort, resultSort.length + 1);
        resultSort[resultSort.length - 1] = demoResult;

        System.out.println(Arrays.toString(resultSort));// todo 打印数组

        return "测试随机数组范围：" + randomNumber1 + "----->" + randomNumber2 + " \n";
    }
```



