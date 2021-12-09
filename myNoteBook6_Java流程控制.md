## Java流程控制

### 用户交互Scanner

 ![image-20211012183121434](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012183121434.png)

 ```java
 package test.test2.scanner;
 
 import java.util.Scanner;
 
 public class Demo01 {
     public static void main(String[] args) {
         //创建一个扫描器对象，用于接收键盘数据
         Scanner scanner = new Scanner(System.in);
         System.out.println("使用next方式接收:");
         //判断用户有没有输入字符串
         if (scanner.hasNext()){
             //使用next方式接收
             String str = scanner.next();
             System.out.println("输入的内容为："+str);
 
         }
         //凡是属于IO流的类如果不关闭会一直占用资源。要养成好习惯用完就关掉
         scanner.close();
 
 
     }
 }
 ```

> D:\Environment\......
> 使用next方式接收:
> hello world!
> 输入的内容为：hello

```java
package test.test2.scanner;

import java.util.Scanner;

public class Demo02 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("使用nextLine方式接收:");

        //判断是否还有输入
        if (scanner.hasNextLine()){
            String str = scanner.nextLine();
            System.out.println("输入的内容为："+str);

        }
        scanner.close();
    }
}

```

> D:\Environment\Java\...
> 使用nextLine方式接收:
> hello world!
> 输入的内容为：hello world!

![image-20211012185321075](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012185321075.png)

```java
package test.test2.scanner;

import java.util.Scanner;

public class Demo03 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入数据:");

        String str = scanner.nextLine();
        System.out.println("输出的内容为:"+str);

        scanner.close();
    }
}
```

> 请输入数据:
> hello world!
> 输出的内容为:hello world!

### scanner进阶使用

---



```java
package test.test2.scanner;

import java.util.Scanner;

public class Demo04 {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        //从键盘接收数据
        int i=0;
        float f=0.0f;

        System.out.println("请输入整数：");

        if (scanner.hasNextInt()){
            i = scanner.nextInt();
            System.out.println("整数数据:"+i);
        }else{
            System.out.println("输入的不是整数数据!");
        }

        System.out.println("请输入小数：");


        if (scanner.hasNextFloat()){
            f = scanner.nextFloat();
            System.out.println("小数数据:"+f);
        }else{
            System.out.println("输入的不是小数数据!");
        }


        scanner.close();
    }
}

```

> 请输入整数：
> 1
> 整数数据:1
> 请输入小数：
> ok
> 输入的不是小数数据!

---



```java
package test.test2.scanner;

import java.util.Scanner;

public class Demo05 {
    public static void main(String[] args) {
        //我们可以输入多个数字，并求其总和与平均数，每输入一个数字用回车确认，通过输入非数字来结束输入并输出执行结果：
        Scanner scanner = new Scanner(System.in);

        //和
        double sum = 0;
        //计算输入了多少个数字
        int m = 0;

        ////通过循环判断是否还有输入，并在里面对每一次进行求和和统计
        while(scanner.hasNextDouble()){
            m++;
            sum+=scanner.nextDouble();
        }
        scanner.close();
        System.out.println("平均数为："+(sum/m));
    }
}

```

> 1
> 2
> 3
> 4
> 5
> 6
> 7
> 8
> 9
> p
> 平均数为：5.0
>
> Process finished with exit code 0

---

### 顺序结构

---

![image-20211012193320423](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012193320423.png)

### 选择结构

---

#### if单选择结构

![image-20211012194100426](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012194100426.png)

#### if双选择结构

![image-20211012194552576](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012194552576.png)

#### if多选择结构

![image-20211012194746533](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012194746533.png)

![image-20211012195112390](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012195112390.png)

#### 嵌套的if结构

![image-20211012195211261](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012195211261.png)

#### switch多选择结构

![image-20211012195405223](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211012195405223.png)

```java
package test.test2.struct;

public class SwitchDemo01 {
    public static void main(String[] args) {
        char grade = 'B';

        switch (grade){
            case 'A':
                System.out.println("优秀");
                break;
            case 'B':
                System.out.println("良好");
            case 'C':
                System.out.println("及格");
            case 'D':
                System.out.println("再接再厉");
            case 'E':
                System.out.println("挂科");
            default:
                System.out.println("未知等级");

        }
    }
}

```

> 良好
> 及格
> 再接再厉
> 挂科
> 未知等级

##### 勘误：JDK7的新特性，表达式结果可以是字符串！！

### 字符的本质还是数字

##### 反编译 java---class(字节码文件)---反编译（IDEA）

点击项目结构（Ctrl+Alt+Shift+s）

![image-20211013140228527](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013140228527.png)

![image-20211013140103629](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013140103629.png)

![image-20211013140627552](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013140627552.png)

打开后

![image-20211013140641185](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013140641185.png)

![image-20211013140827211](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013140827211.png)

打开后将.class拖进去

![image-20211013140905507](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013140905507.png)

![image-20211013140942955](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013140942955.png)

![image-20211013141519590](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013141519590.png)

### while循环详解

---

> while循环
>
> do...while循环
>
> for循环
>
> 在java5中引入了一种主要用于数组的增强型for循环

![image-20211013142748663](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013142748663.png)

### Dowhile循环

---

![image-20211013145301041](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013145301041.png)

### for循环详解

---

![image-20211013145944980](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013145944980.png)

#### 快捷键 100.for

#### 输出换行方法：

> ```java
> System.out.println();
> //System.out.print("\n");
> ```

#### 打印九九乘法表(重要的是学会拆分的思想)

![image-20211013151926988](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013151926988.png)

```java
package test.test2.struct;

public class ForDemo01 {
    public static void main(String[] args) {
        for (int i = 1; i <= 9; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.print(j+"*"+i+"="+(j*i)+"\t");
            }
            System.out.println();
        }
    }
}

```

> 1\*1=1	
> 1\*2=2	2\*2=4	
> 1\*3=3	2\*3=6	3\*3=9	
> 1\*4=4	2\*4=8	3\*4=12	4\*4=16	
> 1\*5=5	2\*5=10	3\*5=15	4\*5=20	5\*5=25	
> 1\*6=6	2\*6=12	3\*6=18	4\*6=24	5\*6=30	6\*6=36	
> 1\*7=7	2\*7=14	3\*7=21	4\*7=28	5\*7=35	6\*7=42	7\*7=49	
> 1\*8=8	2\*8=16	3\*8=24	4\*8=32	5\*8=40	6\*8=48	7\*8=56	8\*8=64	
> 1\*9=9	2\*9=18	3\*9=27	4\*9=36	5\*9=45	6\*9=54	7\*9=63	8\*9=72	9\*9=81	

### 增强for循环

---



![image-20211013152053950](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013152053950.png)

```java
package test.test2.struct;

public class ForDemo02 {
    public static void main(String[] args) {
        int[] numbers={10,20,30,40,50};

        //遍历数组的元素
        for (int x:numbers){
            System.out.println(x);
        }
        
    }
}

```

> 10
> 20
> 30
> 40
> 50

### break\continue

---

![image-20211013152631453](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013152631453.png)

![image-20211013153758831](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013153758831.png)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        

```java
package test.test2.struct;

public class LabelDemo {
    public static void main(String[] args) {
        //打印101-150之间所有的质数
        //质数是指在大于1的自然数中，除了1和它本身以外不再有其他因素的自然数

        int count = 0;
        outer:for (int i=101;i<150;i++){
            for (int j=2;j<i/2;j++){
                if (i%j==0){
                    continue outer;
                }
            }
            System.out.print(i+" ");
        }
    }
}
```

> 101 103 107 109 113 127 131 137 139 149 

### 打印三角形及Debug

```java
package test.test2.struct;

public class TestDemo {
    public static void main(String[] args) {
        //打印三角形 5行
        for (int i = 1; i <=5; i++) {
            for (int j=5;j>=i;j--){
                System.out.print(" ");
            }
            for (int j=1;j<=i;j++){
                System.out.print("*");
            }
            for (int j=1;j<i;j++){
                System.out.print("*");
            }
            System.out.println();
        }
    }
}

```

>       ![image-20211013161028532](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211013161028532.png)

