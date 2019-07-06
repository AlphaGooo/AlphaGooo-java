### 关于Java的方法调用，和一些注意事项


#### 非静态方法：没有 static 修饰的方法，是通过对象来调用的：对象名.方法（）

eg：
```
public class UnstaticMethod {
    
    public static void main(String[] args) {
        UnstaticMethod obj = new UnstaticMethod();
        obj.unstaticFunc();
    }
    
    public void unstaticFunc() {
        System.out.printfln("unstatic function");
    }
}
```


#### 静态方法：用 static 修饰的方法，是通过类名来调用的：类名.方法()

eg：
```
public class InvokeMethod {
    
    public static void main (String[] args)
    {
        InvokeMethod.t2();
    }
    
    public static void t2()
    {
        System.out.println("static t2....");
    }
}
```


#### 静态方法内部调用其他方法：
 - 如果在本类中，可以直接调用静态方法，main方法除外。
 - 如果在本类中，非静态方法只能用对象来调用：类名.静态方法()
 - 如果不在本类中，想要调用静态方法，必须通过：类名.静态方法()
 - 如果不在本类中，想要调用非静态方法，必须导入类包创建对象：对象名.非静态方法()



#### 非静态方法的内部调用：
如果在本类中，非静态方法可以直接调用静态方法和非静态方法。
如果不在本类中，非静态方法调用其他类的静态方法，需要导入类包：类名.静态方法()
如果不在本类中，非静态方法调用其他类的非静态方法，需要导入类包创建对象：对象名.非静态方法。



eg：
```
public class InvokeMethod
{
    public static void main (String[] args){
        t2();
    }
    
    public static void t2(){
        System.out.println("static t2...");
    }
    
    public static void t1(){
        //静态方法调用非静态方法需通过对象来调用
        //InvokeMethod in =new InvokeMethod();
        //in.t2();
        
        t2();
        System.out.println("static t1");
    }
}
```
















