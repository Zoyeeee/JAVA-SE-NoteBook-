# 泛型

P554

## 泛型引入

![image-20211107113902511](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211107113902511.png)

![image-20211107115009828](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211107115009828.png)

```java
package HanSHunPin.generic_;

import java.util.ArrayList;

public class Generic01 {
    public static void main(String[] args) {
        ArrayList arrayList = new ArrayList();
        arrayList.add(new Dog("W1",1));
        arrayList.add(new Dog("W2",2));
        arrayList.add(new Dog("W3",3));

        for (Object o : arrayList) {
            Dog dog = (Dog)o;
            System.out.println(dog.getName()+"-"+dog.getAge());
        }

        //假如不小心加入了一只猫
        /*
        arrayList.add(new Cat("WC1",1));
        System.out.println("-------------------");
        for (Object o : arrayList) {
            Dog dog = (Dog)o;
            System.out.println(dog.getName()+"-"+dog.getAge());
        }

        //Exception in thread "main" java.lang.ClassCastException: HanSHunPin.generic_.Cat cannot be cast to HanSHunPin.generic_.Dog
        // at HanSHunPin.generic_.Generic01.main(Generic01.java:21)
         */

    }
}

class Dog{
    private String name;
    private int age;

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

class Cat{
    private String name;
    private int age;

    public Cat(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

> W1-1
> W2-2
> W3-3
> \-------------------
> W1-1
> W2-2
> W3-3





## 泛型入门

![image-20211107120251020](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211107120251020.png)

```java
package HanSHunPin.generic_;

import java.util.ArrayList;

public class Generic02 {
    public static void main(String[] args) {
        //使用泛型
        //1. 当我们 ArrayList<Dog> 表示存放到 ArrayList 集合中的元素是Dog类型
        //2. 如果编译器发现添加的类型， 不满足要求， 就会报错
        //3. 在遍历的时候， 可以直接取出 Dog 类型而不是 Object
        ArrayList<Dog> arrayList = new ArrayList<Dog>();
        arrayList.add(new Dog("W1",1));
        arrayList.add(new Dog("W2",2));
        arrayList.add(new Dog("W3",3));
//        arrayList.add(new Cat("WC1",1));


        for (Object o : arrayList) {
            Dog dog = (Dog)o;
            System.out.println(dog.getName()+"-"+dog.getAge());
        }
        System.out.println("----------使用泛型---------");
        for (Dog dog : arrayList) {
            System.out.println(dog.getName()+"-"+dog.getAge());
        }

    }
}


class Dog{
    private String name;
    private int age;

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}

class Cat{
    private String name;
    private int age;

    public Cat(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

> W1-1
> W2-2
> W3-3
> \-------------------
> W1-1
> W2-2
> W3-3



## 泛型说明

![image-20211107120420605](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211107120420605.png)



## 泛型应用实例

![image-20211107160330076](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211107160330076.png)

![image-20211107160537012](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211107160537012.png)







## 泛型使用细节

![image-20211107163529844](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211107163529844.png)





## 自定义泛型类

![image-20211108113204951](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211108113204951.png)

**静态是和类相关的，在类加载时，对象还没创建；所以，如果静态方法和静态属性使用了泛型，JVM就无法完成初始化**

![image-20211108161725843](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211108161725843.png)

 







## 自定义泛型接口

![image-20211108162503038](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211108162503038.png)

![image-20211108164227715](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211108164227715.png)

**在接口中，成员都是静态性质的**







## 自定义泛型方法

![image-20211108165028384](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211108165028384.png)









## 泛型方法练习

![image-20211108165834635](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211108165834635.png)

>  U u有误；Integer Dog



## 泛型继承和通配

![image-20211108210849797](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211108210849797.png)

> 1)不对，泛型没有继承性







## JUnit使用

![image-20211108211650176](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211108211650176.png)

![image-20211108215035480](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211108215035480.png)

![image-20211108215135387](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211108215135387.png)

```java
package HanSHunPin.junit_;

import org.junit.jupiter.api.Test;

public class JUnit_ {
    public static void main(String[] args) {
        //传统方式
//        JUnit_ jUnit_ = new JUnit_();
//        jUnit_.m1();
//        jUnit_.m2();
    }


    @Test
    public void m1(){
        System.out.println("m1方法被调用");
    }

    @Test
    public void m2(){
        System.out.println("m2方法被调用");
    }
}
```

junit4 was not loaded
         解决方案：File ---> Settings ---> Build,Execution,Deployment --->Build Tools ---> Maven ---> Running Tests -->勾掉argLine ---> Apply ---> OK







```java
package HanSHunPin.generic_;


import org.junit.jupiter.api.Test;

import java.util.*;

public class Homework01 {
    public static void main(String[] args) {
//        User user1 = new User(1,1,"c1");
//        User user2 = new User(2,2,"c2");
//        User user3 = new User(3,3,"c3");
//        DAO<User> userDAO = new DAO<>();
//        userDAO.save("ID1",user1);
//        userDAO.save("ID2",user2);
//        userDAO.save("ID3",user3);
//        System.out.println(userDAO.list());


    }

    @Test
    public void testList(){
        DAO<User> userDAO = new DAO<>();
        User user1 = new User(1,1,"c1");
        User user2 = new User(2,2,"c2");
        User user3 = new User(3,3,"c3");
        userDAO.save("ID1",user1);
        userDAO.save("ID2",user2);
        userDAO.save("ID3",user3);

        List<User> list = userDAO.list();
        System.out.println("list="+list);
    }

}

class DAO<T>{

    private Map<String,T> map=new HashMap<>();

    public void save(String id, T entity){
        map.put(id,entity);
    }

    public T get(String id){
        return map.get(id);
    }

    public  void updata(String id,T entity){
        map.put(id,entity);
    }

    public List<T> list(){
        Set<String> keySet =map.keySet();
        List<T> ts = new ArrayList<>();
        for (String o : keySet) {
            ts.add(map.get(o));
        }
        return ts;
    }

    public void delete(String id){
        map.remove(id);
    }


}

class User{
    private int id;
    private int age;
    private String name;

    public User(int id, int age, String name) {
        this.id = id;
        this.age = age;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

> list=[User{id=2, age=2, name='c2'}, User{id=1, age=1, name='c1'}, User{id=3, age=3, name='c3'}]

