### 关于Java的Integer、Int和String的转换方法，以及一些高效处理方案

#### Integer转换成int：
```
Integer i = new Integer(10); 
int k = i.intValue();

即：Integer.intValue();
```
 

#### int转换成Integer：
```
int i = 10;
Integer it = new Integer(i);
```
 

#### String转换成int：
```
String str = "10";  
Integer it = new Interger(str);  
int i = it.intValue();  

即：int i = Integer.intValue(string);
```
 

#### int转换成String
```
int i = 10;

(1)String s = String.valueOf(i);
(2)String s = Ingeger.toString(i);
(3)String s = "" + i;
```
 

#### String转换成Integer
```
String str = "10";
Integer it = Integer.valueOf(str);
```
 

#### Integer转换成String
```
Integer it = new Integer(10);
String str = it.toString();
```
 

#### String转换成BigDecimal
```
BigDecimal bd = new BigDecimal(str);
```
 

#### 日期
```
Calendar calendar = Calendar.getInstance();
int year = calendar.get(Calendar.YEAR);
int month = calendar.get(Calendar.MONTH)+1;
int day = calendar.get(Calendar.DATE);

//获取今天的日期字符串（年月日时分秒）
String today = java.text.DateFormat.getDateInstance().format(new java.util.Date());
//获取今天的日期（毫秒ms）
new java.sql.Date(System.currentTimeMillis());
```








