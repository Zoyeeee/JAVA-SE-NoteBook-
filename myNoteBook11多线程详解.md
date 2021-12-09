## 多线程详解

#### 一个进程可以有多个线程，如视频中同时听声音，看图像，看弹幕，等等

![image-20211121103715356](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211121103715356.png)

![image-20211121103755472](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211121103755472.png)

![image-20211121104003546](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211121104003546.png)

##  线程创建

![image-20211121105427638](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211121105427638.png)

![image-20211121105514927](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211121105514927.png)

```java
package test.test2.TestThread1;

//总结：注意，线程开启不一定立即执行，由cpu调度执行
public class TestThread_ extends Thread{

    @Override
    public void run() {
        //run方法线程体
        for (int i = 0; i < 20; i++) {
            System.out.println("我在跑run~~~"+i);
        }

    }

    public static void main(String[] args) {
        //main线程，主线程

        //创建一个线程对象
        TestThread_ testThread_ = new TestThread_();
        //调用start()方法开启线程
        testThread_.start();

        for (int i = 0; i < 20; i++) {
            System.out.println("我在跑main"+i);
        }


    }
}
```

> 我在跑main0
> 我在跑main1
> 我在跑main2
> 我在跑main3
> 我在跑main4
> 我在跑main5
> 我在跑run~~~0
> 我在跑main6
> 我在跑main7
> 我在跑main8
> 我在跑main9
> 我在跑main10
> 我在跑main11
> 我在跑main12
> 我在跑run~~~1
> 我在跑run~~~2
> 我在跑run~~~3
> 我在跑run~~~4
> 我在跑run~~~5
> 我在跑main13
> 我在跑main14
> 我在跑main15
> 我在跑main16
> 我在跑main17
> 我在跑main18
> 我在跑main19
> 我在跑run~~~6
> 我在跑run~~~7
> 我在跑run~~~8
> 我在跑run~~~9
> 我在跑run~~~10
> 我在跑run~~~11
> 我在跑run~~~12
> 我在跑run~~~13
> 我在跑run~~~14
> 我在跑run~~~15
> 我在跑run~~~16
> 我在跑run~~~17
> 我在跑run~~~18
> 我在跑run~~~19

## 网图下载

![image-20211121191509085](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211121191509085.png)

```java
package test.test2.TestThread1;


import org.apache.commons.io.FileUtils;

import java.io.File;
import java.io.IOException;
import java.net.MalformedURLException;
import java.net.URL;

//练习Thread, 实现多线程同步下载图片
public class TestThread_01 extends Thread{

    private String url;//网络图片地址
    private String name;//保存的文件名

    public TestThread_01(String url,String name){
        this.url=url;
        this.name=name;
    }

    @Override
    public void run() {
        WebDownLoader webDownLoader = new WebDownLoader();
        webDownLoader.downloader(url,name);
        System.out.println("下载的文件名为："+name);

    }

    public static void main(String[] args) {
        TestThread_01 t1=new TestThread_01("https://profile.csdnimg.cn/3/6/A/1_qq_33369905","C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\kuangSheng1.jpg");
        TestThread_01 t2=new TestThread_01("https://img-home.csdnimg.cn/images/20211026015909.png","C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\kuangSheng2.png");
        TestThread_01 t3=new TestThread_01("https://img-blog.csdnimg.cn/img_convert/61d590dbe8459247bac42a844814c64d.png","C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\kuangSheng3.png");
        t1.start();
        t2.start();
        t3.start();


    }
}


//下载器
class WebDownLoader{
    //下载方法
    public void downloader(String url,String name)  {
        try {
            FileUtils.copyURLToFile(new URL(url),new File(name));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}
```

> 下载的文件名为：C:\Users\admin\Desktop\JAVA路线\JAVA_FIleTest\kuangSheng2.png
> 下载的文件名为：C:\Users\admin\Desktop\JAVA路线\JAVA_FIleTest\kuangSheng3.png
> 下载的文件名为：C:\Users\admin\Desktop\JAVA路线\JAVA_FIleTest\kuangSheng1.jpg

下载的线程也是随机的

## 实现Runnable接口

![image-20211121202759899](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211121202759899.png)

```java
package test.test2.TestThread1;


//创建线程方式2：实现runnable接口，重写run方法，执行线程需要丢入runnable接口实现类，调用start方法
public class TestThread3 implements Runnable{
    @Override
    public void run() {
        //run方法线程体
        for (int i = 0; i < 20; i++) {
            System.out.println("我在跑run~~~"+i);
        }

    }

    public static void main(String[] args) {
        //main线程，主线程

        //创建runnable接口的实现类对象
        TestThread3 testThread3 = new TestThread3();
        //创建线程对象，通过线程对象来开启我们的线程，代理
        Thread thread = new Thread(testThread3);
        thread.start();

        for (int i = 0; i < 20; i++) {
            System.out.println("我在跑main"+i);
        }


    }
}
```

> 我在跑main0
> 我在跑main1
> 我在跑main2
> 我在跑main3
> 我在跑main4
> 我在跑main5
> 我在跑main6
> 我在跑main7
> 我在跑main8
> 我在跑main9
> 我在跑main10
> 我在跑run~~~0
> 我在跑run~~~1
> 我在跑run~~~2
> 我在跑run~~~3
> 我在跑run~~~4
> 我在跑run~~~5
> 我在跑run~~~6
> 我在跑run~~~7
> 我在跑run~~~8
> 我在跑run~~~9
> 我在跑run~~~10
> 我在跑run~~~11
> 我在跑run~~~12
> 我在跑run~~~13
> 我在跑run~~~14
> 我在跑run~~~15
> 我在跑main11
> 我在跑run~~~16
> 我在跑run~~~17
> 我在跑run~~~18
> 我在跑run~~~19
> 我在跑main12
> 我在跑main13
> 我在跑main14
> 我在跑main15
> 我在跑main16
> 我在跑main17
> 我在跑main18
> 我在跑main19

![image-20211121205851049](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211121205851049.png)

## 初识并发问题

```java
package test.test2.TestThread1;


//多个线程同时操作同一个对象
//买火车票的例子


//发现问题：多个线程操作同一个资源的情况下，线程不安全，数据紊乱
public class TestThread4 implements Runnable{

    //票数
    private  int ticketNums = 10;


    @Override
    public void run() {
        while(true){
            if (ticketNums<=0){
                break;
            }
            //模拟延时
            try {
                Thread.sleep(200);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName()+"-->拿到了第"+ticketNums--+"票");
        }

    }

    public static void main(String[] args) {
        TestThread4 testThread4 = new TestThread4();

        new Thread(testThread4,"小明").start();
        new Thread(testThread4,"老师").start();
        new Thread(testThread4,"黄牛党").start();
    }
}
```

> 老师-->拿到了第10票
> 小明-->拿到了第9票
> 黄牛党-->拿到了第8票
> 黄牛党-->拿到了第7票
> 小明-->拿到了第6票
> 老师-->拿到了第5票
> 小明-->拿到了第4票
> 老师-->拿到了第3票
> 黄牛党-->拿到了第4票
> 老师-->拿到了第2票
> 黄牛党-->拿到了第2票
> 小明-->拿到了第2票
> 小明-->拿到了第1票
> 老师-->拿到了第1票
> 黄牛党-->拿到了第1票

## 龟兔赛跑

![image-20211121214449263](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211121214449263.png)

```java
package test.test2.TestThread1;

public class Race implements Runnable{

    //胜利者
    private static String winner;


    @Override
    public void run() {
        for (int i = 0; i <= 100; i++) {

            //模拟兔子休息
//            if (Thread.currentThread().getName().equals("兔子")&& i%10==0) {
//                try {
//                    Thread.sleep(1);
//                } catch (InterruptedException e) {
//                    e.printStackTrace();
//                }
//            }

            if (gameOver(i)){
                break;
            }
            System.out.println(Thread.currentThread().getName()+"-->跑了"+i+"步");
        }
    }

    //判断是否完成比赛
    private boolean gameOver(int steps){
        if (winner!=null){
            return true;
        }
//        {
        if (steps >= 100) {
            winner = Thread.currentThread().getName();
            System.out.println("winner is " + winner);
            return true;
        }
//        }
        return false;
    }


    public static void main(String[] args) {
        Race race = new Race();
        new Thread(race,"乌龟").start();
        new Thread(race,"兔子").start();
    }
}
```

> ...
>
> 兔子-->跑了97步
> 兔子-->跑了98步
> 兔子-->跑了99步
> winner is 兔子
> 乌龟-->跑了64步

并发的问题

## 实现Callable

![image-20211122120000249](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122120000249.png)

```java
package test.test2.TestThread1;

import org.apache.commons.io.FileUtils;

import java.io.File;
import java.io.IOException;
import java.net.URL;
import java.util.concurrent.*;


/*
1.可以定义返回值
2.可以抛出异常
 */
public class TestCallable implements Callable<Boolean> {

    private String url;//网络图片地址
    private String name;//保存的文件名

    public TestCallable(String url,String name){
        this.url=url;
        this.name=name;
    }

    @Override
    public Boolean call() {
        WebDownLoader webDownLoader = new WebDownLoader();
        webDownLoader.downloader(url,name);
        System.out.println("下载的文件名为："+name);
        return true;

    }

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        TestCallable t1=new TestCallable("https://profile.csdnimg.cn/3/6/A/1_qq_33369905","C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\kuangSheng1.jpg");
        TestCallable t2=new TestCallable("https://img-home.csdnimg.cn/images/20211026015909.png","C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\kuangSheng2.png");
        TestCallable t3=new TestCallable("https://img-blog.csdnimg.cn/img_convert/61d590dbe8459247bac42a844814c64d.png","C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\kuangSheng3.png");

        //创建执行服务
        ExecutorService ser = Executors.newFixedThreadPool(3);

        //提交执行
        Future<Boolean> result1 = ser.submit(t1);
        Future<Boolean> result2 = ser.submit(t2);
        Future<Boolean> result3 = ser.submit(t3);

        //获取结果
        boolean rs1 = result1.get();
        boolean rs2 = result2.get();
        boolean rs3 = result3.get();

        //关闭服务
        ser.shutdownNow();


    }
}


//下载器
class WebDownLoader{
    //下载方法
    public void downloader(String url,String name)  {
        try {
            FileUtils.copyURLToFile(new URL(url),new File(name));
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

}
```

> 下载的文件名为：C:\Users\admin\Desktop\JAVA路线\JAVA_FIleTest\kuangSheng2.png
> 下载的文件名为：C:\Users\admin\Desktop\JAVA路线\JAVA_FIleTest\kuangSheng3.png
> 下载的文件名为：C:\Users\admin\Desktop\JAVA路线\JAVA_FIleTest\kuangSheng1.jpg

## 静态代理模式

```java
package test.test2.TestThread1;


/*
静态代理模式总结：
真实对象和代理对象都要实现同一个接口
代理对象要代理真实角色

好处：
代理对象可以做很多真实对象做不了的事情
真实对象专注做自己的事情
 */
public class StaticProxy {
    public static void main(String[] args) {
        You you = new You();
        MarryCompany marryCompany = new MarryCompany(you);
        marryCompany.HappyMarry();
    }
}

interface Marry{
    void HappyMarry();
}

class You implements Marry{
    @Override
    public void HappyMarry() {
        System.out.println("hahahahahah");
    }
}

class MarryCompany implements Marry{
    private Marry one;
    public MarryCompany(Marry marry) {
        this.one = marry;
    }

    @Override
    public void HappyMarry() {
        System.out.println("阶段1");
        this.one.HappyMarry();
        System.out.println("阶段2");
    }
}
```

> 阶段1
> hahahahahah
> 阶段2

## lamda表达式

![image-20211122133648426](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122133648426.png)

![image-20211122133903196](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122133903196.png)

```java
package test.test2.TestThread1;

public class TestLambda {

    //3.静态内部类
    static class Like2 implements ILike{
        @Override
        public void lambda() {
            System.out.println("i like lambda2");
        }
    }

    public static void main(String[] args) {
        ILike like = new Like();
        like.lambda();

        like=new Like2();
        like.lambda();

        //4.局部内部类
        class Like3 implements ILike{
            @Override
            public void lambda() {
                System.out.println("i like lambda3");
            }
        }
        like =new Like3();
        like.lambda();

        //5.匿名内部类，没有类的名称，必须借助接口或者父类
        like = new ILike() {
            @Override
            public void lambda() {
                System.out.println("i like lambda4");
            }
        };
        like.lambda();

        //6.用lambda简化
        like = ()->{
            System.out.println("i like lambda5");
        };
        like.lambda();

    }
}


//1.定义一个函数式接口
interface ILike{
    void lambda();
}

//2.实现类
class Like implements ILike{
    @Override
    public void lambda() {
        System.out.println("i like lambda");
    }
}
```

> i like lambda
> i like lambda2
> i like lambda3
> i like lambda4
> i like lambda5

### 带参数的情况

#### 匿名内部类

![image-20211122140944426](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122140944426.png)

#### 带参数lambda

![image-20211122141043808](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122141043808.png)

#### 简化

![image-20211122141236734](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122141236734.png)

![image-20211122141300968](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122141300968.png)

![image-20211122141616626](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122141616626.png)

## 线程停止

![image-20211122141948175](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122141948175.png)

![image-20211122142056191](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122142056191.png)

![image-20211122142239989](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122142239989.png)

![image-20211122142634332](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122142634332.png)



![image-20211122151029246](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122151029246.png)

![image-20211122150851595](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122150851595.png)

![image-20211122150938287](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122150938287.png)

```java
package test.test2.TestThread1;

public class TestStop implements Runnable{

    private boolean flag=true;
    @Override
    public void run() {
        int i=0;
        while (flag){
            System.out.println("run.....Thread"+i++);
        }
    }

    public void stop(){
        this.flag=false;
    }

    public static void main(String[] args) {
        TestStop testStop = new TestStop();
        new Thread(testStop).start();

        for (int i = 0; i < 1000; i++) {
            System.out.println("main"+i);
            if (i==900){
                testStop.stop();
                System.out.println("发出线程停止指令");
            }
        }
    }
}
```

> ![image-20211122152600003](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211122152600003.png)

## 线程休眠_sleep

![image-20211123101723816](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123101723816.png)

```java
package test.test2.TestThread1;


import java.text.SimpleDateFormat;
import java.util.Date;

public class TestSleep2 implements Runnable{
    @Override
    public void run() {
        int num=10;
        Date starTime = new Date(System.currentTimeMillis());
        for (int i = 0; i <10 ; i++) {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(new SimpleDateFormat("HH:mm:ss").format(starTime));
            starTime=new Date(System.currentTimeMillis());
        }

    }

    public static void main(String[] args) {
        TestSleep2 testSleep2 = new TestSleep2();
        new Thread(testSleep2).start();
    }
}
```

> 10:44:29
> 10:44:30
> 10:44:31
> 10:44:32
> 10:44:33
> 10:44:34
> 10:44:35
> 10:44:36
> 10:44:37
> 10:44:38
>
> Process finished with exit code 0

## 线程礼让_yield

![image-20211123104615987](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123104615987.png)

![image-20211123105039333](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123105039333.png)

## 线程强制执行_join

![image-20211123105737052](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123105737052.png)

![image-20211123110052888](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123110052888.png)

> main执行到199后，开始VIP线程，只有VIP线程全都执行完了，继续main

## 观测线程状态

![image-20211123110242469](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123110242469.png)

```java
package test.test2.TestThread1;

public class TestState {
    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(()->{
            for (int i = 0; i < 5; i++) {
                try {
                    Thread.sleep(200);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println("///////");
        });

        //观察状态
        Thread.State state=thread.getState();
        System.out.println(state);
        //观察启动后
        thread.start();
        state=thread.getState();
        System.out.println(state);

        while (state!=Thread.State.TERMINATED){//只要线程不终止。就一直输出状态
            Thread.sleep(100);
            state=thread.getState();
            System.out.println(state);


        }
    }
}
```

> NEW
> RUNNABLE
> TIMED_WAITING
> TIMED_WAITING
> TIMED_WAITING
> TIMED_WAITING
> TIMED_WAITING
> TIMED_WAITING
> TIMED_WAITING
> TIMED_WAITING
> TIMED_WAITING
> ///////
> TERMINATED

## 线程的优先级

![image-20211123113813284](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123113813284.png)

```java
package test.test2.TestThread1;

public class TestPriority {
    public static void main(String[] args) {
        System.out.println(Thread.currentThread().getName()+"-->"+Thread.currentThread().getPriority());
        MyPriority myPriority=new MyPriority();
        Thread t1 = new Thread(myPriority);
        Thread t2 = new Thread(myPriority);
        Thread t3 = new Thread(myPriority);
        Thread t4 = new Thread(myPriority);
        Thread t5 = new Thread(myPriority);
        Thread t6 = new Thread(myPriority);

        //先设置优先级，再启动
        t1.start();

        t2.setPriority(1);
        t2.start();

        t3.setPriority(4);
        t3.start();

        t4.setPriority(Thread.MAX_PRIORITY);
        t4.start();

//        t5.setPriority(-1);
//        t5.start();
//
//        t6.setPriority(11);
//        t6.start();


    }

}


class MyPriority implements Runnable{
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName()+"-->"+Thread.currentThread().getPriority());
    }
}
```

> main-->5
> Thread-0-->5
> Thread-1-->1
> Thread-2-->4
> Thread-3-->10

## 守护线程

![image-20211123113951161](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123113951161.png)

```java
package test.test2.TestThread1;

public class TestDaemon {


    public static void main(String[] args) {
        God god = new God();
        Wangfansghu wangfansghu = new Wangfansghu();

        Thread thread = new Thread(god);
        thread.setDaemon(true);
        thread.start();

        new Thread(wangfansghu).start();
    }
}

class God implements Runnable{
    @Override
    public void run() {
        while (true){
            System.out.println("上帝保佑你");
        }
    }
}




class Wangfansghu implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("王方舒好惨");
        }
        System.out.println("-===GG===-");
    }

}
```

> ![image-20211123120331420](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123120331420.png)

## 线程同步机制

> 多个线程操作同一个资源

### 并发：同一个对象被多个线程同时操作

![image-20211123122040799](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123122040799.png)

![image-20211123123036134](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211123123036134.png)

## 三大不安全案例

```java
package test.test2.syn;

import test.oop.demo05.B;

public class UnsafeBuyTicket {
    public static void main(String[] args) {
        BuyTicket station=new BuyTicket();

        new Thread(station,"陈1").start();
        new Thread(station,"陈2").start();
        new Thread(station,"黄牛党").start();
    }

}

class BuyTicket implements Runnable{
    private int ticketNums=10;
    boolean flag=true;//外部停止方式

    @Override
    public void run() {
        //买票
        while (flag){
            try {
                buy();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }

    private void buy() throws InterruptedException {
        if (ticketNums<=0){
            flag=false;
            return;
        }
        //模拟延时
        Thread.sleep(100);
        //买票
        System.out.println(Thread.currentThread().getName()+"拿到"+ticketNums--);
    }
}
```

> 陈2拿到10
> 黄牛党拿到8
> 陈1拿到9
> 黄牛党拿到7
> 陈1拿到7
> 陈2拿到7
> 陈2拿到6
> 黄牛党拿到5
> 陈1拿到5
> 黄牛党拿到4
> 陈1拿到3
> 陈2拿到4
> 陈2拿到2
> 陈1拿到2
> 黄牛党拿到2
> 黄牛党拿到1
> 陈1拿到1
> 陈2拿到1

```java
package test.test2.syn;

public class UnsafeBank {
    public static void main(String[] args) {
        Account account = new Account(100, "结婚基金");
        Drawing you = new Drawing(account, 50, "you");
        Drawing girlFriend = new Drawing(account, 100, "girlFriend");

        you.start();
        girlFriend.start();

    }
}

class Account{
    int money;//余额
    String name;//卡名

    public Account(int money, String name) {
        this.money = money;
        this.name = name;
    }
}

//银行：模拟取款
class Drawing extends Thread{
    Account account;
    int drawingMoney;
    int nowMoney;

    public Drawing(Account account, int drawingMoney, String name){
        super(name);
        this.account=account;
        this.drawingMoney=drawingMoney;


    }

    @Override
    public void run(){
        if (account.money-drawingMoney<0){
            System.out.println(Thread.currentThread().getName()+"钱不够，取不了");
            return;
        }
        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        account.money=account.money-drawingMoney;
        nowMoney=nowMoney+drawingMoney;

        System.out.println(account.name+"余额为："+account.money);

        //此处this.getName()与Thread.currentThread().getName()等价
        System.out.println(this.getName()+"手里的钱:"+nowMoney);
    }


}
```

> 结婚基金余额为：0
> you手里的钱:50
> 结婚基金余额为：0
> girlFriend手里的钱:100

```java
package test.test2.syn;

import java.util.ArrayList;
import java.util.List;

public class UnsafeList {
    public static void main(String[] args) {
        List<String> list=new ArrayList<>();
        for (int i = 0; i < 10000; i++) {
            new Thread(()->{
                list.add(Thread.currentThread().getName());
            }).start();
        }
//        try {
//            Thread.sleep(3000);
//        } catch (InterruptedException e) {
//            e.printStackTrace();
//        }
        System.out.println(list.size());
    }
}
```

> 9997

## 同步方法及同步块

![image-20211203150120051](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211203150120051.png)

![image-20211203150153828](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211203150153828.png)

![image-20211203153627801](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211203153627801.png)

## CopyOnWriteArrayList

```java
package test.test2.syn;

import java.util.concurrent.CopyOnWriteArrayList;

//测试JUC安全类型的集合
public class TestJUC {
    public static void main(String[] args) {
        CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<String>();
        for (int i = 0; i < 10000; i++) {
            new Thread(()->{
                list.add(Thread.currentThread().getName());
            }).start();
        }

        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(list.size());
    }
}
```

> 10000

## 死锁

![image-20211208190741190](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211208190741190.png)

![image-20211208200951320](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211208200951320.png)

```java
package test.test2.syn;


//死锁：多个线程互相抱着对方需要的资源，然后形成僵持.
public class DeadLock {
    public static void main(String[] args) {
        MakeUp g1 = new MakeUp(0,"g1");
        MakeUp g2 = new MakeUp(1,"g2");

        g1.start();
        g2.start();
    }
}

//口红
class Lipstick{

}
//镜子
class Mirror{

}

class MakeUp extends Thread {

    //需要的资源只有一份，用static来保证只有一份
    static Lipstick lipstick = new Lipstick();
    static Mirror mirror = new Mirror();

    int choice;
    String girlName;

    MakeUp(int choice, String girlName) {
        this.choice = choice;
        this.girlName = girlName;
    }


    @Override
    public void run() {
        try {
            makeup();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    private void makeup() throws InterruptedException {
        if (choice == 0) {
            synchronized (lipstick) {
                System.out.println(this.getName() + "获得口红的锁");
                Thread.sleep(1000);
                synchronized (mirror) {//一秒钟后想获得镜子
                    System.out.println(this.getName() + "获得镜子的锁");

                }
            }


        } else {
            synchronized (mirror) {
                System.out.println(this.getName() + "获得镜子的锁");
                Thread.sleep(2000);
                synchronized (lipstick) {//一秒钟后想获得口红
                    System.out.println(this.getName() + "获得口红的锁");

                }
            }



        }
    }
}
```

> Thread-0获得口红的锁
> Thread-1获得镜子的锁

运行ing  死锁了

## Lock锁

![image-20211208201351424](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211208201351424.png)

```java
package test.test2.syn;


import java.util.concurrent.locks.ReentrantLock;

//测试Lock锁
public class TestLock {
    public static void main(String[] args) {
        TestLock2 testLock2=new TestLock2();
        new Thread(testLock2).start();
        new Thread(testLock2).start();
        new Thread(testLock2).start();

    }

}

class TestLock2 implements Runnable{
    int ticketNums = 10;

    //定义Lock锁
    private final ReentrantLock lock=new ReentrantLock();

    @Override
    public void run() {
        while (true){
            try {
                lock.lock();//加锁
                if (ticketNums>0){
                    try {
                        Thread.sleep(1000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(ticketNums--);

                }else {
                    break;
                }
            }finally {
                //解锁
                lock.unlock();

            }

        }
    }
}
```

> 10
> 9
> 8
> 7
> 6
> 5
> 4
> 3
> 2
> 1
>
> Process finished with exit code 0

![image-20211208210815562](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211208210815562.png)

![image-20211208210833437](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211208210833437.png)

## 线程协作-生产者消费者

![image-20211208211310616](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211208211310616.png)

![image-20211208211433497](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211208211433497.png)

![image-20211208211548209](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211208211548209.png)

![image-20211208212019298](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211208212019298.png)

## ![image-20211208212109891](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211208212109891.png)管程法

```java
package test.test2.syn;

//测试：生产者消费者模型-->利用缓冲区解决：管程法
public class TestPC {
    public static void main(String[] args) {
        SynContainer container = new SynContainer();

        new Productor(container).start();
        new Consumer(container).start();
    }
}

//生产者
class Productor extends Thread {
    SynContainer container;

    public Productor(SynContainer container) {
        this.container = container;
    }

    //生产
    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            container.push(new Chicken(i));
        }
    }
}

//消费者
class Consumer extends Thread {
    SynContainer container;

    public Consumer(SynContainer container) {
        this.container = container;
    }

    @Override
    public void run() {
        for (int i = 0; i < 100; i++) {
            container.pop();
        }
    }
}

//产品
class Chicken {
    int id;

    public Chicken(int id) {
        this.id = id;
    }
}

//缓冲区
class SynContainer {
    //需要一个容器大小
    Chicken[] chickens = new Chicken[10];
    //容器计数器
    int count = 0;

    //生产者放入产品
    public synchronized void push(Chicken chicken) {
        //如果容器满了，就需要等待消费者消费
        if (count == chickens.length) {
            //通知消费者消费，生产等待
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        //如果没有满，我们就需要丢入产品
        chickens[count] = chicken;
        count++;

        System.out.println("生产了" + count + "只鸡");
        //可以通知消费者消费了
        this.notifyAll();


    }

    //消费者消费产品
    public synchronized Chicken pop() {
        //判断能够消费
        if (count == 0) {
            //等待生产者和生产，消费者等待
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        //如果可以消费
        count--;
        Chicken chicken = chickens[count];
        System.out.println("消费了-->" + count + "只鸡");


        //吃完了，通知生产者生产
        this.notifyAll();

        return chicken;


    }

}
```

> 部分截取
>
> 生产了1只鸡
> 生产了2只鸡
> 生产了3只鸡
> 生产了4只鸡
> 生产了5只鸡
> 生产了6只鸡
> 生产了7只鸡
> 生产了8只鸡
> 生产了9只鸡
> 生产了10只鸡
> 消费了-->9只鸡
> 消费了-->8只鸡
> 消费了-->7只鸡
> 消费了-->6只鸡
> 消费了-->5只鸡
> 消费了-->4只鸡
> 消费了-->3只鸡
> 消费了-->2只鸡
> 消费了-->1只鸡
> 消费了-->0只鸡
> 生产了1只鸡
> 生产了2只鸡

## 信号灯法

```java
package test.test2.syn;

//测试生产者消费者问题2：信号灯法，标志位解决
public class TestPC2 {
    public static void main(String[] args) {
        TV tv = new TV();
        new Player(tv).start();
        new Watcher(tv).start();
    }
}

//生产者-->演员
class Player extends Thread{
    TV tv;
    public Player(TV tv){
        this.tv=tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            if (i%2==0){
                this.tv.play("快乐大本营播放中");
            }else {
                this.tv.play("广告");
            }
        }
    }
}
//消费者-->观众
class Watcher extends Thread{
    TV tv;
    public Watcher(TV tv){
        this.tv=tv;
    }

    @Override
    public void run() {
        for (int i = 0; i < 20; i++) {
            tv.watch();
        }
    }
}
//产品-->节目
class TV{
    //演员表演，观众等待 T
    //观众观看，演员等待 F
    String voice;
    boolean flag =true;

    //表演
    public synchronized void play(String voice){
        if (!flag){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("演员表演了:"+voice);
        //通知观众观看
        this.notifyAll();
        this.voice=voice;
        this.flag=!this.flag;
    }
    //观看
    public synchronized void watch(){
        if (flag){
            try {
                this.wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        System.out.println("观看了"+voice);
        //通知演员表演
        this.notifyAll();
        this.flag=!this.flag;

    }


}
```

> 演员表演了:快乐大本营播放中
> 观看了快乐大本营播放中
> 演员表演了:广告
> 观看了广告
> 演员表演了:快乐大本营播放中
> 观看了快乐大本营播

## 线程池

![image-20211209233719867](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211209233719867.png)

![image-20211209233846573](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211209233846573.png)

