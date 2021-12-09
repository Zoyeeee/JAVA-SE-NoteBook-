## 面向对象

### 什么是面向对象

----

![image-20211023145906913](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023145906913.png)

![image-20211023150615982](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023150615982.png)

### 回顾

---

##### 非静态方法和静态方法的区别

![image-20211023161057451](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023161057451.png)

![image-20211023173726199](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023173726199.png)

##### static和类一起加载的，非静态方法是在类实例化之后才存在的

![image-20211023174217250](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023174217250.png)

##### Java都是值传递

![image-20211023175915428](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023175915428.png)

##### 一个类里面只能有一个public class但可以有多个class

![image-20211023181905324](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023181905324.png)

### 类与对象的创建

---

![image-20211023182445040](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023182445040.png)

![image-20211023182741730](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023182741730.png)

```java
package test.oop.demo02;

public class Student {
    //属性：字段
    String name;//null
    int age;//0


    //方法
    public void study(){
        System.out.println(this.name+"在学习");
    }
}

```





```java
package test.oop.demo02;

//一个项目应该只存一个main方法
public class Application {

    public static void main(String[] args) {

        //类：抽象的，需要实例化
        //类实例化后会返回一个自己的对象
        //student对象就是一个Student类的具体实例
        Student student=new Student();

        Student xiaoming=new Student();
        Student xiaohong=new Student();

        xiaoming.name="小明";
        xiaoming.age=3;

        xiaohong.name="小红";
        xiaohong.age=4;
        System.out.println(xiaoming.name);

    }
}

```

> 小明



### 构造器详解

---

```java
package test.oop.demo02;

//java----->class
public class Person {
    //一个类即使什么也不写，也会存在一个构造器
    //显示的定义构造器
    String name;
    int age;
    //实例化初始值
    //1.使用new关键字，本质是在调用构造器
    //2.用来初始化值
    public Person(){
        this.name="Chen Lei";
    }

    //有参构造:一旦定义了有参构造，无参就必须显示定义
    public Person(String name){
        this.name=name;
    }

    //ALT+insert 快捷键：会生成构造器

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

/*
public static void main(String[] args) {

        //new 实例化了一个对象
        Person person0 = new Person();
        System.out.println(person0.name);
        Person person1 = new Person("chenlei");
        System.out.println(person1.name);
    }

    构造器：
        1.和类名相同
        2.没有返回值
    作用：
        1.new 本质在调用构造方法
        2.初始化对象的值
    注意点：
        1.定义有参构造后，如果想使用无参构造，需显示的定义一个无参的构造
    快捷键：
        ALT+Insert
========================================
        this. =
* */
```

> Chen Lei
> chenlei

### 创建对象内存分析

---

![image-20211024113120381](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211024113120381.png)

```java
package test.oop.demo03;

public class Pet {
    public String name;
    public int age;

    //无参构造
    public void shout(){
        System.out.println("叫了一声");
    }
}

/*
    public static void main(String[] args) {
        Pet dog = new Pet();
        dog.name="旺财";
        dog.age=3;
        dog.shout();

        System.out.println(dog.name);
        System.out.println(dog.age);
    }
 */
```

### 简单小结类与对象

---

1. 类与对象

   类是一个模板:抽象，对象是一个具体的实例

2. 方法

   定义、调用

3. 对应的引用

   引用类型：

   ​				对象是通过引用来操作的：栈----->堆(地址)

4. 属性： 字段Field    成员变量

   默认初始化：

   ​					数字:	0	0.0

   ​					char:	u0000

   ​					boolean:	false

   ​					引用:	null

   修饰符	属性类型	属性名	=	属性值

5.  对象的创建和使用
   - 必须使用new关键字创造对象，构造器  Person kuangshen = new Person();
   - 对象的属性    kuangshen.name
   - 对象的方法    kuangshen.sleep()

6. 类
   - 静态的属性	属性
   - 动态的行为    方法



封装	继承	多态

### 封装详解

---

![image-20211024125446071](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211024125446071.png)

```java
package test.oop.demo04;

//类 private:私有
public class Student {
    //属性私有
    private String name;//名字
    private int id;//学号
    private char sex;//性别
    private int age;

    //提供一些可以操作这个属性的方法！
    //提供一些public的get,set方法

    //get   获得这个数据
    public String getName(){
        return this.name;
    }
    //set   给这个数据设置值
    public void setName(String name){
        this.name=name;
    }

    //ALT+Insert可自动生成get set方法


    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public char getSex() {
        return sex;
    }

    public void setSex(char sex) {
        this.sex = sex;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age<120 && age>0){
            this.age = age;
        }else {
            this.age = 3;
        }

    }
}

/*
    public static void main(String[] args) {
        Student s1 = new Student();
        String name = s1.getName();
        System.out.println(name);

        System.out.println("==============");

        s1.setName("ChenLei");
        System.out.println(s1.getName());
        System.out.println("==============");

        s1.setAge(21);//不合法的
        System.out.println(s1.getAge());
    }

null
==============
ChenLei
==============
21

    1.提高程序安全性，保护数据
    2.隐藏代码的实现细节
    3.统一接口
    4。系统的可维护增加了



 */
```

### 什么是继承

---

![image-20211025122621600](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211025122621600.png)

#### 私有的东西无法被继承

```java
package test.oop.demo05;

//在java中，所有的类，都默认直接或者间接继承Object类
//人    :父类
public class Person {

    //public
    public int money1 = 10_0000_0000;

    //private
    private int money = 9_9999_9999;

    public void say(){
        System.out.println("说了一句话");
    }

    public int getMoney() {
        return money;
    }

    public void setMoney(int money) {
        this.money = money;
    }
}

/*
优先级排序顺序
1. public
2. protected
3. default
4. private


 */
```

---

```java
package test.oop.demo05;


//学生 is 人       ：派生类，子类
//子类继承了父类，就会拥有父类的全部方法
public class Student extends Person{
    //快捷键   Ctrl + H
}


/*
    public static void main(String[] args) {
        Student student = new Student();
        student.say();
        System.out.println(student.money1);

    }


 */
```

---

```java
package test.oop.demo05;


//老师 is 人       ：派生类，子类
public class Teacher extends Person{

}

```

---

```java
package test.oop;


import test.oop.demo05.Person;
import test.oop.demo05.Student;

//一个项目应该只存一个main方法
public class Application {
    public static void main(String[] args) {
        Person person = new Person();


    }

}

```

---

### Super详解

---

**类只写了有参的构造器，父类的无参构造器就没了；**

**子类的无参构造器也写不了（除非子类无参第一行加上super(有参），不然默认调用的无参)**

```
super注意点：
    1.super调用父类的构造方法，必须在构造方法的第一个
    2.super必须只能出现在子类的方法或者构造方法中
    3.super和this不能同时调用构造方法

Vs this:
    代表的对象不同：
        this:   本身调用者这个对象
        super:  代表父类对象的引用

    前提
        this:   没有继承也可以使用
        super:  只能在继承条件下才可以使用

    构造方法
        this():   本类的构造
        super():    父类的构造
```

```java
package test.oop.demo05;

//在java中，所有的类，都默认直接或者间接继承Object类
//人    :父类
public class Person {
    public Person() {
        System.out.println("Person无参构造器执行了");
    }

    protected String name="ChenLei";


    //私有的东西无法被继承
    public void print(){
        System.out.println("Person");
    }

}

/*
优先级排序顺序
1. public
2. protected
3. default
4. private


 */
```

---

```java
package test.oop.demo05;


//学生 is 人       ：派生类，子类
//子类继承了父类，就会拥有父类的全部方法
public class Student extends Person{
    public Student() {
        //隐藏代码：调用了父类的无参构造
        super();//调用父类的构造器，必须要在子类构造器的第一行
        //this();
        System.out.println("子类的无参构造执行了");
    }

    public Student(String name) {
        this.name = name;
    }

    //快捷键   Ctrl + H
    private String name="WuDiShiDuoMeJiMo";

    public void test(String name){
        System.out.println(name);
        System.out.println(this.name);
        System.out.println(super.name);
    }

    public void print(){
        System.out.println("Student");
    }

    public void test1(){
        print();
        this.print();
        super.print();
    }



}


/*



 */
```

---

```java
package test.oop;


import test.oop.demo05.Student;

//一个项目应该只存一个main方法
public class Application {
    public static void main(String[] args) {
        Student student = new Student();
        student.test("haha");
        student.test1();
    }

}

```

> Person无参构造器执行了
> 子类的无参构造执行了
> haha
> WuDiShiDuoMeJiMo
> ChenLei
> Student
> Student
> Person

### 方法重写

---

#### 例子1

```java
package test.oop.demo05;

public class A extends B{
    public static void test(){
        System.out.println("A=>test()");
    }
}

```

---

```java
package test.oop.demo05;

//重写都是方法的重写，和属性无关
public class B {
    public static void test(){
        System.out.println("B=>test()");
    }
}

```

---

```java
package test.oop;


import test.oop.demo05.A;
import test.oop.demo05.B;

//一个项目应该只存一个main方法
public class Application {
    public static void main(String[] args) {

        //方法的调用只和左边，定义的数据类型有关
        A a = new A();
        a.test();

        //父类的引用指向了子类
        B b = new A();
        b.test();
    }

}


```

> A=>test()
> B=>test()

---

---

#### **重写快捷键：ALT+Insert;	override**

```
重写：需要有继承关系，子类重写父类的方法！
    1.方法名必须相同
    2.参数列表必须相同
    3.修饰符：范围可以扩大但不能缩小： public>Protected>Default>private
    4.抛出的异常：范围，可以被缩小，但不能扩大；

为什么需要重写：
    1.父类的功能，子类不一定需要，或者不一定满足
    Alt + Insert  ----->    override
```

#### 例子2

---

```java
package test.oop.demo05;

public class A extends B{

    //Override: 重写
    @Override//注解：有功能的注释
    public void test() {
        System.out.println("A=>test()");
    }
}

```

---

```java
package test.oop.demo05;

//重写都是方法的重写，和属性无关
public class B {
    public void test(){
        System.out.println("B=>test()");
    }
}

```

---

```java
package test.oop;


import test.oop.demo05.A;
import test.oop.demo05.B;

//一个项目应该只存一个main方法
public class Application {
    //静态的方法和非静态的方法区别很大
        //静态方法： 方法的调用只和左边，定义的数据类型有关
        //非静态方法：子类重写了父类的方法；只有非静态的才算重写,private也不行,只能public
    public static void main(String[] args) {

        //方法的调用只和左边，定义的数据类型有关
        A a = new A();
        a.test();

        //父类的引用指向了子类
        B b = new A();
        b.test();
    }

}

```

> A=>test()
> A=>test()

### 什么是多态（重点）

---

![image-20211025132238043](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211025132238043.png)

```java
package test.oop.demo06;

public class Person {

    public void run(){
        System.out.println("run");
    }
}

/*
多态注意事项：
1.  多态是方法的多态，属性没有多态
2.  父类和子类，有联系    否则，类型转换异常！
3.  存在条件： 继承关系， 方法需要重写，父类引用指向子类对象


不能重写的
    1.static方法，属于类，它不属于实例
    2.final常量
    3.private方法；
 */
```

---

```java
package test.oop.demo06;

public class Student extends Person{

    @Override
    public void run() {
        System.out.println("son");
    }

    public void eat(){
        System.out.println("eat");
    }
}

```

---

```java
package test.oop;


import test.oop.demo06.Person;
import test.oop.demo06.Student;

//一个项目应该只存一个main方法
public class Application {
    //静态的方法和非静态的方法区别很大
        //静态方法： 方法的调用只和左边，定义的数据类型有关
        //非静态方法：子类重写了父类的方法；只有非静态的才算重写,private也不行,只能public
    public static void main(String[] args) {

        //一个对象的实际类型是确定的
        //new Student();
        //new Person();

        //可以指向的引用类型就不确定了: 父类的引用指向子类

        //Student 能调用的方法都是自己的或者继承父类的
        Student s1 = new Student();
        //Person 能调用的方法都是自己的或者继承父类的
        Person s2 = new Student();
        Object s3 = new Student();

        s1.run();
        s2.run();//子类重写了父类的方法，执行子类的方法
        //s3.run(); 报错

        //对象能执行哪些方法，主要看对象左边的类型，和右边关系不大
        s1.eat();
        //报错 s2.eat();
    }
}

```

---

> son
> son
> eat

### instanceof和类型转换

---

#### instanceof	(类型转换)引用类型，判断一个对象是什么类型

```java
package test.oop.demo06;

public class Person {

    public void run(){
        System.out.println("run");
    }
}

/*
多态注意事项：
1.  多态是方法的多态，属性没有多态
2.  父类和子类，有联系    否则，类型转换异常！
3.  存在条件： 继承关系， 方法需要重写，父类引用指向子类对象


不能重写的
    1.static方法，属于类，它不属于实例
    2.final常量
    3.private方法；
 */
```

---

```java
package test.oop.demo06;

public class Student extends Person{

    @Override
    public void run() {
        System.out.println("son");
    }

    public void eat(){
        System.out.println("eat");
    }

    public void go(){
        System.out.println("go");
    }
}

/*
    public static void main(String[] args) {

        //Object > String
        //Object > Person > Teacher
        //Object > Person > Student
        //System.out.println(X instanceof Y);//能不能编译通过，看X，Y之间是否有关系
        Object object = new Student();

        System.out.println(object instanceof Student);//true
        System.out.println(object instanceof Person);//true
        System.out.println(object instanceof Object);//true
        System.out.println(object instanceof Teacher);//false
        System.out.println(object instanceof String);//false

        System.out.println("================");

        Person person = new Student();
        System.out.println(person instanceof Student);//true
        System.out.println(person instanceof Person);//true
        System.out.println(person instanceof Object);//true
        System.out.println(person instanceof Teacher);//false
        //System.out.println(person instanceof String);//编译就报错

        System.out.println("================");

        Student student = new Student();
        System.out.println(student instanceof Student);//true
        System.out.println(student instanceof Person);//true
        System.out.println(student instanceof Object);//true
        //System.out.println(student instanceof Teacher);//编译报错


    }

 */
```

---

```java
package test.oop;


import test.oop.demo06.Person;
import test.oop.demo06.Student;
import test.oop.demo06.Teacher;

//一个项目应该只存一个main方法
public class Application {
    //静态的方法和非静态的方法区别很大
        //静态方法： 方法的调用只和左边，定义的数据类型有关
        //非静态方法：子类重写了父类的方法；只有非静态的才算重写,private也不行,只能public
    public static void main(String[] args) {

        //类型之间的转化：  基本类型转换 高低64 32 16 8   同样的  父（高）  子（低）

        //高                     低
        Person student = new Student();
        //student.go();报错

        //将student这个对象转换为Student类，我们就可以使用Student类型的方法了！

        ((Student)student).go();
//        Student student1 = (Student) student;
//        student1.go();

        //子类转换为父类，可能丢失自己的本来的一些方法
    }
}

/*
1.父类引用指向子类的对象
2.把子类转换为父类，向上转型； 可能丢失自己的本来的一些方法
3.把父类转换为子类，向下转型；强制转换
4.方便方法的调用，减少重复的代码

抽象： 封装、继承、多态！   抽象类，接口

 */
```

---

### static关键字详解

---

```java
package test.oop.demo07;


//static
public class Student {

    private static int age;//静态的变量  多线程
    private double score;//非静态的变量

    public void run(){

    }

    public static void go(){

    }

    public static void main(String[] args) {
        Student s1 = new Student();

        System.out.println(Student.age);
        //System.out.println(Student.score);非静态不能.
        System.out.println(s1.age);
        System.out.println(s1.score);

        s1.run();
        Student.go();
        go();

    }
}

```

> 0
> 0
> 0.0

---

```java
package test.oop.demo07;

public class Person {

    {
        //代码块（匿名代码块），构造器之前,可用于赋初始值//    2
        System.out.println("匿名代码块");
    }

    static {
        //静态代码块,最早执行和类一块加载,且只执行一次//    1
        System.out.println("静态代码块");
    }

    public Person(){
        //                               3
        System.out.println("构造方法");
    }

    public static void main(String[] args) {
        Person person1 = new Person();
        System.out.println("=================");
        Person person2= new Person();
    }

}

```

> 静态代码块
> 匿名代码块
> 构造方法
> \=================
> 匿名代码块
> 构造方法
>
> Process finished with exit code 0

----

```java
package test.oop.demo07;


//静态导入包
import static java.lang.Math.random;
import static java.lang.Math.PI;


public class Test {

    public static void main(String[] args) {
        System.out.println(random());
        System.out.println(PI);


    }

}

```

> 0.8308907457475745
> 3.141592653589793

---

### 抽象类

---

![image-20211025204754472](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211025204754472.png) 

```java
package test.oop.demo08;


//abstract  抽象类：类 extend:单继承        (接口可以多继承)
public abstract class Action {

    //约束~有人帮我们实现~
    //abstract, 抽象方法， 只有方法名字， 没有方法的实现
    public abstract void doSomething();

    //1. 不能new这个抽象类，只能靠子类去实现它；是一个约束
    //2. 抽象类中可以写普通方法~
    //3. 抽象方法必须在抽象类中~

}

```

---

```java
package test.oop.demo08;


//抽象类的所有方法，继承了它的子类，都必须要实现它的方法~除非继承了的子类也是抽象类
public class A extends  Action{
    @Override
    public void doSomething() {

    }
}

```

---

### 接口的定义与实现

---

![image-20211025211254504](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211025211254504.png)

```java
package test.oop.demo09;


//interface 定义的关键字,接口都需要有实现类
public interface UserService {


    //常量~所有定义的常量都是  public  static final，一般不会在接口中定义常量
    public  static final int age=99;
    //接口中的所有定义的方法其实都是抽象的   public abstract;前面这个可以不写
    public abstract void add(String name);
    public abstract void delete(String name);
    public abstract void update(String name);
    public abstract void query(String name);


}

```

---

```java
package test.oop.demo09;

public interface TimeService {
    void timer();
}

```

---

```java
package test.oop.demo09;

// 抽象类： extends~
// 类 可以实现接口 implements 接口
// 实现了接口的类， 就需要重写接口中的方法~

// 多继承~利用接口实现多继承~
public class UserServiceImpl implements UserService, TimeService{
    @Override
    public void add(String name) {

    }

    @Override
    public void delete(String name) {

    }

    @Override
    public void update(String name) {

    }

    @Override
    public void query(String name) {

    }

    @Override
    public void timer() {

    }
}

```

---

```java
作用：
    1.约束
    2.定义一些方法，让不同的人实现
    3.public abstract
    4.public static final
    5.接口不能被实例化~，接口中没有构造方法~
    6.implements可以实现多个接口
    7.必须要重写接口中的方法~

```

---

### N种内部类

---

![image-20211026114243565](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211026114243565.png)

```java
package test.oop.demo10;

public class Outer {

    private int id;

    //局部内部类
    public void method(){

        class Inner1{
            public void in(){


            }
        }


    }

    public void out(){
        System.out.println("这是外部类的方法");
    }

    public class Inner{
        public void in(){
            System.out.println("这是内部类的方法");
        }

        //获得外部类的私有属性~
        public void getID(){
            System.out.println(id);
        }
    }

}


//一个java类中可以有多个class类，但是只能有一个public class类
class A{


}
```

---

```java
package test.oop.demo10;

public class Test {
    public static void main(String[] args) {
        //没有名字初始化类,不用将实例保存到变量中~
        new Apple().eat();

        UserService userService = new UserService() {
            @Override
            public void hello() {

            }
        };
    }

}

class Apple{
    public void eat(){
        System.out.println("1");
    }
}

interface UserService{
    void hello();
}
```

---

```java
package test.oop;

import test.oop.demo10.Outer;

//一个项目应该只存一个main方法
public class Application {
    public static void main(String[] args) {
        Outer outer = new Outer();

        //通过这个外部类来实例化内部类
        Outer.Inner inner = outer.new Inner();
        inner.in();
        inner.getID();
    }
}


```

---

> 这是内部类的方法
> 0

