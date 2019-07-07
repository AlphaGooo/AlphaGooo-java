### 关于获取 Java int数组的最后一个元素的讨论，以及解决方案

```
        // 产生随机数组
        int[] arr = new int[s_len];
        for (int i = 0; i < s_len; i++) {
            arr[i] = (int) Math.round(Math.random() * max);
        }

        // 排序
        java.util.Arrays.sort(arr);
        
        // 拿到数组最后一个元素
        int target = array10[array10.length-1];
```
        
        
        