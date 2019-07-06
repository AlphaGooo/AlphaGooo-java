### 关于Java的HashMap字符串转换恢复成HashMap数组的讨论，以及一些高效的解决方案

```
    /*** 
     * @Todo: hashMap数组字符串，恢复hashMap
     * @Params: [str] 期望字符串格式为 [0=123,1=224423,2=3423]
     * @Return: java.util.HashMap<java.lang.String,java.lang.String> 
     */ 
    public HashMap<String,String> mapStringToMap(String str)
    {
        // 切割字符串，去掉首尾字符
        str = str.substring(1, str.length()-1);

        // 以逗号 "," 为分割，把字符串转为数组
        String[] strs = str.split(",");

        // 初始化一个全新的 hashMap 数组
        HashMap<String,String> map = new HashMap<String, String>();

        // 遍历字符数组，填充 hashMap 数组
        for (String string : strs) {
            String key = string.split("=")[0];
            String value = string.split("=")[1];
            map.put(key, value);
        }
        
        return map;
    }
```