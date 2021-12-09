## 异常

---

### Error和Exception

---

![image-20211026142913762](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211026142913762.png)

![image-20211026144640719](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211026144640719.png)

![image-20211026144730855](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211026144730855.png)

![image-20211026144851477](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211026144851477.png)

![image-20211026144956672](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211026144956672.png)

```java
package test.exception;

public class Demo01 {

    public static void main(String[] args) {
//        new Demo01().a();
//        System.out.println(11/0);
//        System.out.println()
    }  

//    public void a(){
//        b();
//    }
//
//    public void b(){
//        a();
//    }
}

```

### 捕获和抛出异常

---

![image-20211026145654634](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211026145654634.png)

```java
package test.exception;

public class Test2 {
    public static void main(String[] args) {
        int a = 1;
        int b = 0;

        try {
            new Test2().test(1,0);
        } catch (ArithmeticException e) {
            e.printStackTrace();
        } finally {
        }

        //System.out.println(a/b);
        // 选中后Ctrl+ALT+T
        try {
            if (b==0){//主动抛出异常  throw   throws
                throw new ArithmeticException();
            }
            System.out.println(a/b);
        } catch (Exception e) {
//            System.exit(0);
            e.printStackTrace();//打印错误的栈信息
        } finally {
        }
    }


    //假设这方法中，处理不了这个异常。方法上抛出异常
    public void test(int a, int b) throws ArithmeticException{
        if (b==0){//主动抛出异常  throw   throws
            throw new ArithmeticException();//主动的爆出异常， 一般在方法中使用
        }
    }
}
```

---

```java
package test.exception;

public class Test {

    public static void main(String[] args) {
        int a = 1;
        int b = 0;

        try{//try 监控区域
            System.out.println(a/b);
        }catch(ArithmeticException e){//catch 捕获异常
            System.out.println("程序出现异常，变量b不能为0");
        }finally {//处理善后工作
            System.out.println("finally");
        }

        //finally 可以不要finally， 假设IO， 资源，关闭！




        //假设要捕获多个异常：    从小到大！
        
        try{//try 监控区域
//            new Test().a();
            System.out.println(a/b);
        }catch(Error e){//catch(想要捕获的异常类型！) 捕获异常
            System.out.println("程序出现异常，1");
        }catch(Exception e){//catch(想要捕获的异常类型！) 捕获异常
            System.out.println("程序出现异常，2");
        }catch(Throwable e){//catch(想要捕获的异常类型！) 捕获异常
            System.out.println("程序出现异常，3");
        }finally {//处理善后工作
            System.out.println("finally");
        }



    }

    public void a(){b();}
    public void b(){a();}
}
```

---

### 自定义异常及经验小结

---

![image-20211026152216269](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211026152216269.png)

![image-20211026154254621](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211026154254621.png)

```java
package test.exception.demo02;


//自定义的异常类
public class MyException extends Exception{

    //传递数字>10
    private int detail;

    public MyException(int a) {
        this.detail=a;
    }

    //toString:异常的打印信息
    @Override
    public String toString() {
        return "MyException{" +
                "detail=" + detail +
                '}';
    }
}

```

---

```java
package test.exception.demo02;

public class Test {

    //可能会存在异常的方法
    static void test(int a) throws MyException {

        System.out.println("传递的参数为:"+a);

        if (a>10){
            throw new MyException(a);//抛出
        }

        System.out.printf("OK");


    }

    public static void main(String[] args) {
        try {
            test(15);
        } catch (MyException e) {
            System.out.println("MyException=>"+e);
        }
    }

}

```

