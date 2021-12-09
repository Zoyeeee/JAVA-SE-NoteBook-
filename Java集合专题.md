# 集合

## 集合介绍 

![image-20211029133034713](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029133034713.png)

![image-20211029133113649](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029133113649.png)

## 集合的框架体系（重点）

![image-20211029134340052](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029134340052.png) 

1. **集合主要是两组（单列集合， 双列集合）**
2. **Collection接口有两个重要的子接口 List  Set ,他们的实现子类都是单列集合**
3. **Map接口的实现子类是双列集合，存放的K-V**

## Collections方法

![image-20211029135822960](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029135822960.png)

![image-20211029135844834](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029135844834.png)

```java
package HanSHunPin.chapter14;

import java.util.ArrayList;
import java.util.List;

public class CollectionMethod {
//    @SuppressWarnings({"all"})
    public static void main(String[] args) {
        //add:添加单个元素
        List list = new ArrayList();
        list.add("Jack");
        list.add(10);
        list.add(true);
        System.out.println("list="+list);
        //remove: 删除指定元素
        list.remove(0);//删除第一个元素
        list.remove(true);//指定删除某个元素
        System.out.println("list="+list);
        //contains: 查找元素是否存在
        System.out.println(list.contains(10));
        //size:获取元素个数
        System.out.println(list.size());
        //isEmpty: 判断是否为空
        System.out.println(list.isEmpty());
        //clear:清空
        list.clear();
        System.out.println("list="+list);
        //addAll:添加多个元素
        List list2 = new ArrayList();
        ArrayList list3 = new ArrayList();
        list3.add("123");
        list3.add(true);
        list2.add("红楼梦");
        list2.add("三国演义");
        list.addAll(list2);
        list.addAll(list3);
        System.out.println("list="+list);
        //containsAll:查找多个元素是否都存在
        System.out.println(list.containsAll(list2));
        //removeAll: 删除多个元素
        list.removeAll(list2);
        System.out.println("list="+list);

    }
}

```

> list=[Jack, 10, true]
> list=[10]
> true
> 1
> false
> list=[]
> list=[红楼梦, 三国演义, 123, true]
> true
> list=[123, true]
>
> Process finished with exit code 0

## 迭代器遍历

![image-20211029142421732](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029142421732.png)

![image-20211029142818181](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029142818181.png)

![image-20211029143220204](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029143220204.png)

```java
package HanSHunPin.chapter14;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;

public class CollectionIterator {
    public static void main(String[] args) {

        Collection col=new ArrayList();
        col.add(new Book("三国演义","罗贯中",10.1));
        col.add(new Book("小李飞刀","古龙",5.1));
        col.add(new Book("红楼梦","曹雪芹",34.6));

        System.out.println("col="+col);
        //遍历 col集合
        //1. 先得到col对应的迭代器
        Iterator iterator= col.iterator();
        //2. 使用while循环遍历
        while(iterator.hasNext()){//判断是否还有数据
//            System.out.println(iterator.next());
            //返回下一个元素，类型是Object
            Object obj = iterator.next();
            System.out.println("obj="+obj);
        }
            /*
            快捷键：while=>itit
            Ctrl+J 可显示当前所有快捷模板
             */

        //3. 当退出while循环后, 这是iterator迭代器，指向了最后的元素
//        iterator.next();

        //4. 如果希望再次遍历，需要重置迭代器
        iterator = col.iterator();
        while (iterator.hasNext()) {
            Object next =  iterator.next();
            System.out.println("第二次遍历obj="+next);
        }


    }
}

class Book{
    private String name;
    private String author;
    private double price;

    public Book(String name, String author, double price) {
        this.name = name;
        this.author = author;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public double getPrice() {
        return price;
    }

    public void setPrice(double price) {
        this.price = price;
    }

    @Override
    public String toString() {
        return "Book{" +
                "name='" + name + '\'' +
                ", author='" + author + '\'' +
                ", price=" + price +
                '}';
    }
}
```

> col=[Book{name='三国演义', author='罗贯中', price=10.1}, Book{name='小李飞刀', author='古龙', price=5.1}, Book{name='红楼梦', author='曹雪芹', price=34.6}]
> obj=Book{name='三国演义', author='罗贯中', price=10.1}
> obj=Book{name='小李飞刀', author='古龙', price=5.1}
> obj=Book{name='红楼梦', author='曹雪芹', price=34.6}
> 第二次遍历obj=Book{name='三国演义', author='罗贯中', price=10.1}
> 第二次遍历obj=Book{name='小李飞刀', author='古龙', price=5.1}
> 第二次遍历obj=Book{name='红楼梦', author='曹雪芹', price=34.6}
>
> Process finished with exit code 0

## 集合增强for

![image-20211029151605688](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029151605688.png)

```java
package HanSHunPin.chapter14;

import java.util.ArrayList;
import java.util.Collection;

public class CollectionFor {
    public static void main(String[] args) {
        Collection col=new ArrayList();
        col.add(new Book("三国演义","罗贯中",10.1));
        col.add(new Book("小李飞刀","古龙",5.1));
        col.add(new Book("红楼梦","曹雪芹",34.6));

        //1.使用增强for, Collection集合使用
        //2.增强for的底层，仍然是迭代器
        //3.增强for 可以理解成就是简化版本的 迭代器
        //4.快捷方式I
        for(Object book : col){
            System.out.println("book="+book);
        }

        //增强for，也可以直接在数组使用
        int [] nums={1,8,10,90};
        for(int i :nums){
            System.out.println("i="+i);
        }




    }
}
```

## List接口方法

![image-20211029183713884](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029183713884.png)

### List接口的常用方法

![image-20211029185850985](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211029185850985.png)

```java
package HanSHunPin.list_;

import java.util.ArrayList;
import java.util.List;

public class ListMethod {
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add("张三丰");
        list.add("贾宝玉");
        // void add(int index, Object ele):在index位置插入ele元素
        //在index=1的位置插入一个对象
        list.add(1,"哇哈哈");
        System.out.println("list="+list);
        //boolean addAll(int index, Collection eles):从index位置开始将eles中的所有元素添加进来
        List list2 = new ArrayList();
        list2.add("无敌1");
        list2.add("无敌2");
        list.addAll(2,list2);
        System.out.println("list="+list);
        //Object get(int index):获取指定index位置的元素------演示略
        //int indexOf(Object obj):返回obj在集合中首次出现的位置
        System.out.println(list.indexOf("无敌2"));
        //int lastIndexOf(Object obj):返回obj在当前集合中末次出现的位置
        list.add("张三丰");
        System.out.println(list.lastIndexOf("张三丰"));
        //Object remove(int index):移出指定index位置的元素， 并返回此元素
        list.remove(0);
        System.out.println("list="+list);
        //Object set(int index, Object ele):设置指定index位置的元素为ele, 相当于替换。索引必须存在
        list.set(1,"无敌3");
        System.out.println("list="+list);
        //List subList(int fromIndex, int toIndex):返回从fromIndex到toIndex位置的子集合,包含fromIndex不包含toIndex,前闭后开
        System.out.println(list.subList(1, 2));

    }
}
```

> list=[张三丰, 哇哈哈, 贾宝玉]
> list=[张三丰, 哇哈哈, 无敌1, 无敌2, 贾宝玉]
> 3
> 5
> list=[哇哈哈, 无敌1, 无敌2, 贾宝玉, 张三丰]
> list=[哇哈哈, 无敌3, 无敌2, 贾宝玉, 张三丰]
> [无敌3]
>
> Process finished with exit code 0

---

![image-20211030111709301](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211030111709301.png)

## ArrayList注意事项

![image-20211030113041158](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211030113041158.png)



## ArrayList

![image-20211030114117685](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211030114117685.png)

### ArrayList扩容机制

![image-20211030115230409](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211030115230409.png)

### Debugger设置

![image-20211030121442347](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211030121442347.png)

## Vector注意事项

![image-20211030122445379](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211030122445379.png)

![image-20211030122653977](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211030122653977.png)

## LinkedList

![image-20211030124714524](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211030124714524.png)

![image-20211030125709778](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211030125709778.png)

## List集合选择

![image-20211031133355711](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211031133355711.png)

## set接口方法

![image-20211031133637132](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211031133637132.png)

![image-20211031133826619](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211031133826619.png)

```java
package HanSHunPin.set_;

import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

public class SetMethod {
    public static void main(String[] args) {


        //1. 以Set 接口的实现类 HashSet 来讲解Set接口的方法
        //2. set接口的实现类的对象（Set接口对象），不能存放重复的元素
        //3. set接口对象存放数据是无序（即添加的顺序和取出的顺序不一致）
        //4. 注意：取出的顺序的顺序虽然不是添加的顺序，但是他是固定的

        Set set = new HashSet();
        set.add("john");
        set.add("lucy");
        set.add("john");
        set.add("jack");
        set.add(null);
        set.add(null);

        System.out.println("set="+set);

        //遍历
        //方式1： 使用迭代器
        System.out.println("=======使用迭代器====");
        Iterator iterator = set.iterator();
        while (iterator.hasNext()) {
            Object obj =  iterator.next();
            System.out.println("obj="+obj);

        }

        //方式2：增强for
        System.out.println("=======使用增强for====");
        for (Object o : set) {
            System.out.println("o="+o);
        }

        //set 接口对象。不能通过索引获取

    }
}
```

## HashSet全面说明

![image-20211031135431274](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211031135431274.png)

```java
package HanSHunPin.set_;

import java.util.HashSet;

public class HashSet01 {
    public static void main(String[] args) {
        HashSet set = new HashSet();
        //1.在执行add方法后， 会返回一个boolean值
        //2. 如果添加成功， 返回true, 否则返回false
        //3. 可以通过 remove 指定删除哪个对象
        System.out.println(set.add("1"));
        System.out.println(set.add("2"));
        System.out.println(set.add("1"));//false
        System.out.println(set.add("4"));
        System.out.println(set.add("5"));

        set.remove("1");
        System.out.println("set="+set);//不保证输出顺序为输入顺序

        //4.Hashset 不能添加相同的元素/数据
        set = new HashSet();
        set.add("1");
        set.add("1");
        set.add(new Dog("Tom"));//OK
        set.add(new Dog("Tom"));//OK
        System.out.println("set="+set);

        //在加深以下， 非常经典的面试题
        set.add(new String("Chen"));//OK
        set.add(new String("Chen"));//False
        System.out.println("set="+set);
    }
}


class Dog{
    private String name;

    public Dog(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Dog{" +
                "name='" + name + '\'' +
                '}';
    }
}
```

> true
> true
> false
> true
> true
> set=[2, 4, 5]
> set=[1, Dog{name='Tom'}, Dog{name='Tom'}]
> set=[1, Dog{name='Tom'}, Dog{name='Tom'}, Chen]
>
> Process finished with exit code 0

## 数组链表模拟

![image-20211031142513618](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211031142513618.png)

```java
package HanSHunPin.set_;

public class HashSetStructure {
    public static void main(String[] args) {
        //模拟一个 HashSet的底层(HashMap 的底层结构)

        //1. 创建一个数组，数组的类型是 Node[]
        //2. 有些人，直接把 Node[] 数组称为 table
        Node[] table = new Node[16];
        //3. 创建结点
        Node john = new Node("john", null);

        table[2]=john;
        Node jack = new Node("jack", null);
        john.next=jack;//将jack结点挂载到john
        Node rose = new Node("Rose",null);
        jack.next = rose;

        Node luck = new Node("luck", null);
        table[3] = luck;
        System.out.println("table="+table);

    }
}

class Node{//结点， 存储数据， 可以指向下一个结点， 从而形成链表
    Object item;//存放数据
    Node   next;//指向下一个结点

    public Node(Object item, Node next) {
        this.item = item;
        this.next = next;
    }
}
```

## HashSet扩容机制

![image-20211031145807964](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211031145807964.png)

## HashSet源码

```ja
package HanSHunPin.set_;

import java.util.HashSet;

public class HashSetSource {
    public static void main(String[] args) {
        HashSet hashSet = new HashSet();
        hashSet.add("1");
        hashSet.add("2");
        hashSet.add("1");
        System.out.println("set="+ hashSet);

        
    }
}
```

自己加断点去跑

![image-20211101131932010](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101131932010.png)

![image-20211101141011987](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101141011987.png)

![image-20211101141031981](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101141031981.png)

```java
package HanSHunPin.set_;

import java.util.HashSet;
import java.util.Objects;

public class HashSetExercise {
    public static void main(String[] args) {
        HashSet set = new HashSet();
        set.add(new Employee("C1",1));
        set.add(new Employee("C2",2));
        set.add(new Employee("C3",3));
        System.out.println("set="+set);

        System.out.println("================");

        set.add(new Employee("C3",3));
        System.out.println("set="+set);

        System.out.println("================");


    }
}

class Employee{
    private String name;
    public int age;

    public Employee(String name, int age) {
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

    @Override
    public String toString() {
        return "Employee{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    //如果name 和 age 值相同，则返回相同的hash值

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Employee employee = (Employee) o;
        return age == employee.age && Objects.equals(name, employee.name);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
}
```

> set=[Employee{name='C1', age=1}, Employee{name='C2', age=2}, Employee{name='C3', age=3}]
> \================
> set=[Employee{name='C1', age=1}, Employee{name='C2', age=2}, Employee{name='C3', age=3}]
> \================

---

```java
package HanSHunPin.set_;

import java.util.HashSet;
import java.util.Objects;

public class HashSetExercise2 {
    public static void main(String[] args) {
        HashSet set = new HashSet();
        set.add(new Employee("C1",'男', new MyDate(1997,1,1)));
        set.add(new Employee("C2",'男', new MyDate(1997,1,1)));
        set.add(new Employee("C1",'女', new MyDate(1997,1,1)));
        System.out.println("set="+set);
    }
}

class Employee{
    private String name;
    private char sal;
    private MyDate birthday;

    public Employee(String name, char sal, MyDate birthday) {
        this.name = name;
        this.sal = sal;
        this.birthday = birthday;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public char getSal() {
        return sal;
    }

    public void setSal(char sal) {
        this.sal = sal;
    }

    public MyDate getBirthday() {
        return birthday;
    }

    public void setBirthday(MyDate birthday) {
        this.birthday = birthday;
    }

    @Override
    public String toString() {
        return "Employee{" +
                "name='" + name + '\'' +
                ", sal=" + sal +
                ", birthday=" + birthday +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Employee employee = (Employee) o;
        return Objects.equals(name, employee.name) && Objects.equals(birthday, employee.birthday);
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, birthday);
    }
}


class MyDate{
    private int year;
    private int month;
    private int day;

    public MyDate(int year, int month, int day) {
        this.year = year;
        this.month = month;
        this.day = day;
    }

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public int getMonth() {
        return month;
    }

    public void setMonth(int month) {
        this.month = month;
    }

    public int getDay() {
        return day;
    }

    public void setDay(int day) {
        this.day = day;
    }

    @Override
    public String toString() {
        return "MyDate{" +
                "year=" + year +
                ", month=" + month +
                ", day=" + day +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        MyDate myDate = (MyDate) o;
        return year == myDate.year && month == myDate.month && day == myDate.day;
    }

    @Override
    public int hashCode() {
        return Objects.hash(year, month, day);
    }
}
```

> set=[Employee{name='C2', sal=男, birthday=MyDate{year=1997, month=1, day=1}}, Employee{name='C1', sal=男, birthday=MyDate{year=1997, month=1, day=1}}]

---

## LinkedHashSet介绍

![image-20211101152433317](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101152433317.png)

![image-20211101152558252](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101152558252.png)

### 1.  LinkedHashSet 加入顺序和取出元素/数据的顺序一致

### 2.  LinkedHashSet 底层维护的是一个LinkedHashMap(是HashMap的子类)

### 3.  LinkedHashSet 底层结构（数组table+双向链表）

### 4.  添加第一次时， 直接将 数组table扩容到16， 存放的结点类型是 LinkedHashMap$Entry

### 5.  数组是HashMap$Node[]  存放的元素/数据是 LinkedHashMap$Entry



## Map接口特点

![image-20211101160052326](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101160052326.png)

```java
package HanSHunPin.map_;

import java.util.HashMap;
import java.util.Map;

public class Map_ {
    public static void main(String[] args) {
        //Map 接口实现类的特点。 使用实现类 HashMap
        //1. Map与Collection并列存在。用于保存具有映射关系的数据：Key-Value(双列元素)
        //2. Map中的key 和 value 可以是任何引用类型的数据，会封装到 HashMap$Node 对象中
        //3. 常用 String 类 作为 Map 的 key
        //4. key 和 value 之间存在单向一对一关系， 即通过指定的 key 总能找到对应的 value
        Map map = new HashMap();
        map.put("3","-3");
        map.put("1","-1");
        map.put("2","-2");
        map.put("1","-99");//当有相同的Key时，就等价于替换
        map.put("4","-2");//value 可以重复
        map.put(null,null);
        map.put(null,"999");
        map.put("4",null);

        System.out.println("map="+map);

        //通过 get 方法，传入 key, 会返回对应的 value
        System.out.println(map.get(null));
    }
}
```

> map={null=999, 1=-99, 2=-2, 3=-3, 4=null}
> 999

![image-20211101164939628](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101164939628.png)

```java
package HanSHunPin.map_;

import java.util.Collection;
import java.util.HashMap;
import java.util.Map;
import java.util.Set;

public class MapSource {
    public static void main(String[] args) {

        Map map = new HashMap();
        map.put("no1","C1");
        map.put("no2","张无忌");

        //1. k-v 最后是 HashMap$Node node = newNode(hash, key, value, null)
        //2. k-v 为了方便程序员的遍历，还会创建 EntrySet集合， 该集合存放的元素的类型 Entry ，而一个Entry
        //   对象就有k,v EntrySet<Entry<K,V>> 即： transient Set<Map.Entry<K,V>> entrySet;
        //3. entrySet 中，定义的类型是 Map.Entry， 但是实际上存放的还是 HashMap$Node
        //   这是因为 static class Node<K,V>  implements Map.Entry<K,V>
        //4. 当把 HashMap$Nod 对象存放到 entrySet 就方便我们的遍历， 因为 Map.Entry 提供了重要方法
        //   K getKey();   V getValue();

        Set set = map.entrySet();
        System.out.println(set.getClass());
        for (Object obj : set) {

            Map.Entry entry = (Map.Entry) obj;
            System.out.println(entry.getKey()+"-"+entry.getValue());

        }

        Set set1 = map.keySet();
        System.out.println(set1.getClass());
        Collection values = map.values();
        System.out.println(values.getClass());

    }
}
```

> class java.util.HashMap$EntrySet
> no2-张无忌
> no1-C1
> class java.util.HashMap$KeySet
> class java.util.HashMap$Values

### Map接口方法

![image-20211101173726445](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101173726445.png)

![image-20211101173822577](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101173822577.png)

### Map的六大遍历方式

![image-20211101194529651](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101194529651.png)

```java
package HanSHunPin.map_;

import java.util.*;

public class MapFor {
    public static void main(String[] args) {
        Map map = new HashMap();
        map.put("3", "-3");
        map.put("2", "-2");
        map.put("1", "-99");//当有相同的Key时，就等价于替换
        map.put("4", "-2");//value 可以重复
        map.put(null, "999");
        map.put("4", null);
        System.out.println("map="+map);

        System.out.println("==========================");

        //第一组：先取出所有的key ,通过key 取出对应的Value
        Set keyset = map.keySet();
        //(1) 增强for
        for (Object key : keyset) {
            System.out.println(key+"-"+map.get(key));
        }

        System.out.println("==========================");

        //（2） 迭代器
        Iterator iterator = keyset.iterator();
        while (iterator.hasNext()) {
            Object next =  iterator.next();
            System.out.println(next+"-"+map.get(next));

        }

        System.out.println("==========================");

        //第二组： 把所有的values取出
        Collection values = map.values();
        //这里可以使用所有的Collections使用的遍历方法
        //（1）增强for
        System.out.println("=============（1）增强for=============");
        for (Object o : values) {
            System.out.println(o);
        }

        //(2)迭代器
        System.out.println("=============(2)迭代器=============");
        Iterator iterator1 = values.iterator();
        while (iterator1.hasNext()) {
            Object next =  iterator1.next();
            System.out.println(next);
        }

        //第三组： 通过EntrySet 来获取 k-v
        Set entrySet = map.entrySet();
        //(1)增强for
        System.out.println("=============第三组(1)增强for=============");
        for (Object entry : entrySet) {
            //将entry 转成 Map.Entry
            Map.Entry m = (Map.Entry) entry;
            System.out.println(m.getKey()+"-"+m.getValue());
        }

        //(2)迭代器
        System.out.println("=============第三组(2)迭代器=============");
        Iterator iterator2 = entrySet.iterator();
        while (iterator2.hasNext()) {
            Object next =  iterator2.next();
            Map.Entry m = (Map.Entry) next;
            System.out.println(m.getKey()+"-"+m.getValue());
        }


    }
}
```

> map={null=999, 1=-99, 2=-2, 3=-3, 4=null}
> ==========================
> null-999
> 1--99
> 2--2
> 3--3
> 4-null
> ==========================
> null-999
> 1--99
> 2--2
> 3--3
> 4-null
> ==========================
> =============（1）增强for=============
> 999
> -99
> -2
> -3
> null
> =============(2)迭代器=============
> 999
> -99
> -2
> -3
> null
> =============第三组(1)增强for=============
> null-999
> 1--99
> 2--2
> 3--3
> 4-null
> =============第三组(2)迭代器=============
> null-999
> 1--99
> 2--2
> 3--3
> 4-null
>
> Process finished with exit code 0

### 题目

![image-20211101204431117](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101204431117.png)

```Java
package HanSHunPin.map_;

import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Set;

public class MapExercise {
    public static void main(String[] args) {

        Map map = new HashMap();
        map.put(1,new Emp("C1",17999,1));
        map.put(2,new Emp("C2",27999,2));
        map.put(3,new Emp("C3",37999,3));

        //方式1   keySet  itit
        Set keySet = map.keySet();
        Iterator iterator = keySet.iterator();
        while (iterator.hasNext()) {
            Object obj =  iterator.next();
            Emp temp= (Emp) map.get(obj);
            if (temp.getSale()>18000){
                System.out.println(temp.getId());
            }
        }

        //方式2   entrySet    增强for
        System.out.println("=====================");
        Set entryset = map.entrySet();
        for (Object o : entryset) {
            Map.Entry m = (Map.Entry) o;
            Emp temp=(Emp)m.getValue();
            if (temp.getSale()>18000){
                System.out.println(temp.getId());
            }
        }




    }
}



class Emp{
    private String name;
    private int sale;
    private int id;

    public Emp(String name, int sale, int id) {
        this.name = name;
        this.sale = sale;
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getSale() {
        return sale;
    }

    public void setSale(int sale) {
        this.sale = sale;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    @Override
    public String toString() {
        return "Emp{" +
                "name='" + name + '\'' +
                ", sale=" + sale +
                ", id=" + id +
                '}';
    }
}
```

> 2
> 3
> \=====================
> 2
> 3

## HMap阶段小结

![image-20211101212012661](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211101212012661.png)

## HMap底层机制

![image-20211105131619035](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211105131619035.png)

![image-20211105131926594](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211105131926594.png)

## HMap扩容树化触发

## Hashtable的使用

![image-20211105145349195](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211105145349195.png)

1. 底层有数组 Hashtable$Entry[] 初始化大小为11

2. threshold   8=11*0.75

3. 扩容：

   ​	11-》23

   ```java
   int newCapacity = (oldCapacity << 1) + 1;
   ```

   

   执行 方法addEntry(hash, key, value, index); 添加k_v 封装到Entry

   当 if(count>=threshold)满足时，就进行扩容

   ![image-20211105155353209](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211105155353209.png)

## Properties

![image-20211105155452363](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211105155452363.png)

```java
package HanSHunPin.map_;

import java.util.Properties;

public class Properties_ {
    public static void main(String[] args) {

        //1. Properties 继承 Hashtable
        //2. 可以通过 K-V 存放数据， 当然 key 和 value 不能为 null
        Properties properties = new Properties();
        properties.put("c1",100);
        properties.put("c2",100);
        properties.put("c3",100);
        properties.put("c3",99);

        System.out.println("properties=" + properties);

        //通过 k 获取对应值
        System.out.println(properties.get("c3"));

        //删除
        properties.remove("c3");
        System.out.println("properties=" + properties);

        //修改
        properties.put("c2",999);
        System.out.println("properties=" + properties);
        

    }
}
```

> properties={c3=99, c2=100, c1=100}
> 99
> properties={c2=100, c1=100}
> properties={c2=999, c1=100}

## 集合选型规则

![image-20211105161007124](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211105161007124.png)

## TreeSet源码解读

```java
package HanSHunPin.set_;

import java.util.Comparator;
import java.util.TreeSet;

public class TreeSet_ {
    public static void main(String[] args) {

        //1. 当我们使用无参构造器，创建TreeSet时， 任然时无序的
        //2. 希望添加的元素，按照字符串大小来排序
        //3. 使用TreeSet 提供的一个构造器，可以传入一个比较器（匿名内部类）
        //   并指定排序规则

        TreeSet treeSet = new TreeSet();
        //添加数据
        treeSet.add("jack");
        treeSet.add("tom");
        treeSet.add("sp");
        treeSet.add("a");

        System.out.println("treeSet="+treeSet);
        System.out.println("===========传入一个比较器============");

        TreeSet treeSet1 = new TreeSet(new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                //下面 调用 String 的 compateTo 方法进行字符串大小比较
//                return ((String)o2).compareTo(((String)o1));
                //如果要求加入的元素，按照长度大小排序
                return ((String)o1).length()-((String)o2).length();
                //会发现相同长度的加不进去， 可看下面的代码知道原因
            }
        });

        treeSet1.add("jack");
        treeSet1.add("tom");
        treeSet1.add("sp");
        treeSet1.add("a");
        treeSet1.add("abc");

        System.out.println("treeSet1="+treeSet1);

        //1. 构造器把传入的比较器对象， 赋给了 TreeSet的底层的 TreeMap的属性 this.comparator
        /*

        public TreeMap(Comparator<? super K> comparator) {
            this.comparator = comparator;
            }

        2. 在调用treeSet.add("tom"), 在底层会执行到

            if (cpr != null) {
            do {
                parent = t;
                cmp = cpr.compare(key, t.key);//动态绑定到我们的匿名内部类（对象的compare方法）
                if (cmp < 0)
                    t = t.left;
                else if (cmp > 0)
                    t = t.right;
                else                          //如果相等， 即返回0，这个Key就没有加入, 执行替换(只替换双列的												  //value)
                    return t.setValue(value);
            } while (t != null);
        }


         */
    }
}
```

> treeSet=[a, jack, sp, tom]
> ===========传入一个比较器============
> treeSet1=[a, sp, tom, jack]

## TreeMap源码解读

```java
package HanSHunPin.map_;

import java.util.Comparator;
import java.util.TreeMap;

public class TreeMap_ {
    public static void main(String[] args) {

        //使用默认的构造器， 创建 TreeMap, 是无序的(也没有排序)
        TreeMap treeMap = new TreeMap();
        treeMap.put("jack","杰克");
        treeMap.put("tom","汤姆");
        treeMap.put("kristina","克瑞斯提诺");
        treeMap.put("smith","斯密斯");

        System.out.println("treeMap="+treeMap);
        System.out.println("===============");

        /*
            按照传入的k(String)的大小进行排序
         */

        TreeMap treeMap1 = new TreeMap(new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                return ((String)o2).compareTo((String) o1);
            }
        });

        treeMap1.put("jack","杰克");
        treeMap1.put("tom","汤姆");
        treeMap1.put("kristina","克瑞斯提诺");
        treeMap1.put("smith","斯密斯");

        System.out.println("treeMap1="+treeMap1);
        System.out.println("===============");

    }
}
```

> treeMap={jack=杰克, kristina=克瑞斯提诺, smith=斯密斯, tom=汤姆}
> \===============
> treeMap1={tom=汤姆, smith=斯密斯, kristina=克瑞斯提诺, jack=杰克}
> \===============

## collections工具类

![image-20211106200126958](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211106200126958.png)

![image-20211106201336381](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211106201336381.png)

