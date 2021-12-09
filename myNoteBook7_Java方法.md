## Java方法

![image-20211013161351894](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013161351894.png)

```java
package test.test2.Method;

public class Demo01 {
    public static void main(String[] args) {
        int sum=add(1,2);
        System.out.println(sum);
    }

    public static int add(int a,int b){
        return a+b;
    }
}

```

> 3

### 方法的定义和调用

---


![image-20211013162059350](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013162059350.png)

> 实参：实际调用传递给他的参数
>
> 形参：用来定义作用的

![image-20211013162644566](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013162644566.png)

```java
package test.test2.Method;

public class Demo02 {
    public static void main(String[] args) {
        int max = max(5, 6);
        System.out.println(max);
    }

    //比大小
    public static int max(int a,int b){
        int result=0;

        if (a==b) {
            System.out.println("num1==num2");
            return 0;//终止方法
        }

        if (a>b){
            result=a;
        }else {
            result=b;
        }

        return result;
    }
}

```

> 6

#### 拓展：值传递（Java）和引用传递

### 方法的重载

---

![image-20211013164056258](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013164056258.png)

#### 注：方法重载的规则要考

```java
package test.test2.Method;

public class Demo02 {
    public static void main(String[] args) {
        double max = max(20.0, 20.0);
        System.out.println(max);
    }


    public static double max(double a,double b){
        double result=0;

        if (a==b) {
            System.out.println("num1==num2");
            return 0;//终止方法
        }

        if (a>b){
            result=a;
        }else {
            result=b;
        }

        return result;
    }
    //比大小
    public static int max(int a,int b){
        int result=0;

        if (a==b) {
            System.out.println("num1==num2");
            return 0;//终止方法
        }

        if (a>b){
            result=a;
        }else {
            result=b;
        }

        return result;
    }
}

```

> num1==num2
> 0.0

### 命令行传递参数

---

![image-20211013165851429](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013165851429.png)

```java
package test.test2.Method;

public class Demo03 {
    public static void main(String[] args) {
        //args.Length 数组长度
        for (int i = 0; i < args.length; i++) {
            System.out.println("arg["+i+"]:"+args[i]);
        }
    }
}

```

#### 具体操作

![image-20211013172738077](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013172738077.png)

### 可变参数

---

![image-20211013172931137](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013172931137.png)

```java
package test.test2.Method;

public class Demo04 {
    public static void main(String[] args) {
        Demo04 demo04 = new Demo04();
        demo04.test(1,2,3,4,5,6,7,8,9);
    }


    public void test(int... i){
        System.out.println(i[0]);
        System.out.println(i[1]);
        System.out.println(i[3]);
        System.out.println(i[4]);
    }
}

```

> 1
> 2
> 4
> 5

### 递归讲解（重点）

---

![image-20211013180325976](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013180325976.png)

![image-20211013180559374](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013180559374.png)

```java
package test.test2.Method;

public class Demo06 {
    public static void main(String[] args) {
        System.out.println(f(5));
    }


    //1!    1
    //2!    2*1
    //5!    5*4*3*2*1

    //2     2*f(1)
    //3     3*f(2)
    public static int f(int n){
        if (n==1){
            return 1;
        }else {
            return n*f(n-1);
        }
    }
}
```

> 120

