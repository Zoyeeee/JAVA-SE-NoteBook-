# IO流

![image-20211113103242630](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211113103242630.png)

## 文件

### 文件流

**![image-20211113103412067](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211113103412067.png)**

## 常用的文件操作

![image-20211113103625505](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211113103625505.png)

```java
package HanSHunPin.chapter19;

import org.junit.jupiter.api.Test;

import java.io.File;
import java.io.IOException;

public class FileCreate {
    public static void main(String[] args) {

    }

    @Test
    public void create01(){
        String filePath = "C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\news1.txt";
        File file = new File(filePath);

        try {
            file.createNewFile();
            System.out.println("文件创建成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @Test
    public void create02(){
        File parentFile = new File("C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\");
        String fileName = "news2.txt";
        File file = new File(parentFile, fileName);

        try {
            file.createNewFile();
            System.out.println("创建成功");
        } catch (IOException e) {
            e.printStackTrace();
        }

    }

    @Test
    public void create03(){
        String parentPath = "C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\";
        String fileName="news3.txt";
        File file = new File(parentPath, fileName);

        try {
            file.createNewFile();
            System.out.println("文件创建成功");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }



}
```

## 获取文件的相关信息

![image-20211113110906426](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211113110906426.png)

## 目录的操作和文件删除

![image-20211113111357640](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211113111357640.png)

![image-20211113111512853](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211113111512853.png)

### 这里我们需要体会到，在java编程中，目录也被当做文件

## IO流原理及流的分类

![image-20211113113224253](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211113113224253.png)

![image-20211113113530530](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211113113530530.png)

![image-20211113114029615](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211113114029615.png)

## FileInputStream

![image-20211113114618442](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211113114618442.png)

```java
package HanSHunPin.chapter19;

import org.junit.jupiter.api.Test;

import java.io.FileInputStream;
import java.io.IOException;

public class FileInputStream_ {
    public static void main(String[] args) {




    }


    @Test
    public void readFile01(){
        String filePath = "C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\news1.txt";
        int readData =0;
        FileInputStream fileInputStream = null;

        try {
            fileInputStream = new FileInputStream(filePath);
            //从该输入流读取一个字节的数据。 如果没有输入可用。此方法将阻止。
            //如何返回-1，表示读取完毕
            while((readData = fileInputStream.read()) != -1){
                System.out.print((char) readData);
            }

        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            //关闭文件流，释放资源
            try {
                fileInputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }


    }



    @Test
    public void readFile02(){
        String filePath = "C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\news1.txt";
        int readLen =0;
        byte[] buf = new byte[8];

        FileInputStream fileInputStream = null;//一次读取8个字节

        try {
            fileInputStream = new FileInputStream(filePath);
            //从该输入流读取最多b.length字节的数据到字节数组。 此方法将阻塞，直到某些输入可用。
            //如何返回-1，表示读取完毕
            //如果读取正常，返回实际读取的字节数
            while((readLen = fileInputStream.read(buf)) != -1){
                System.out.print(new String(buf,0,readLen));
            }

        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            //关闭文件流，释放资源
            try {
                fileInputStream.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }


    }
}
```

## FileOutputStream

![image-20211114110733245](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211114110733245.png)

![image-20211114110752263](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211114110752263.png)



## 文件拷贝

完成图片/音乐的拷贝

```java
package HanSHunPin.chapter19;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class FileCopy {
    public static void main(String[] args) {
        //1.创建的文件的输入流，将文件读入到程序
        //2.创建文件的输出流，将读取到的文件数据，写入到指定的文件。
        String srcFilePath ="C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\001.jpg";
        String destFilePath ="C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\001_0.jpg";
        FileInputStream fileInputStream = null;
        FileOutputStream fileOutputStream=null;

        try {
            fileInputStream  = new FileInputStream(srcFilePath);
            fileOutputStream = new FileOutputStream(destFilePath);
            //定义一个字节数组，提高读取效果
            byte[] buf = new byte[1024];
            int readLen = 0;
            while((readLen=fileInputStream.read(buf))!=-1){
                //读取到后，就写入到文件
                //一边读，一边写
                fileOutputStream.write(buf,0,readLen);//一定要使用这个方法

            }

            System.out.println("拷贝成功");

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                //关闭输入流和输出流，释放资源
                if (fileInputStream!=null){
                    fileInputStream.close();
                }
                if (fileOutputStream!=null){
                    fileOutputStream.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }


    }
}
```

> 拷贝成功

## 文件字符流说明

![image-20211116200812726](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211116200812726.png)

![image-20211116201210575](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211116201210575.png)

## FileReader

```java
package HanSHunPin.chapter19;

import org.junit.jupiter.api.Test;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class FileReader_ {
    public static void main(String[] args) {

    }

    @Test
    public void readFile01() {
        String filePath = "C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\news3.txt";
        int data = 0;


        //1.创建FileReader对象
        FileReader fileReader = null;

        try {
            fileReader = new FileReader(filePath);
            while ((data = fileReader.read()) != -1) {
                System.out.print((char) data);
            }

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (fileReader != null) {
                    fileReader.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    @Test
    public void readFile02(){
        String filePath = "C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\news3.txt";
        int readLen=0;
        char[] buf = new char[8];
        //1.创建FileReader对象
        FileReader fileReader = null;

        try {
            fileReader = new FileReader(filePath);
            while ((readLen = fileReader.read(buf)) != -1) {
                System.out.print(new String(buf,0,readLen));
            }

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (fileReader != null) {
                    fileReader.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

    }


}
```

## FIleWriter

```java
char[] chars ={'a','b','c'};
fileWriter.writer('H');
fileWriter.write("陈磊hahahahha".toCharArray(),0,2);
fileWriter.write("你好北京~");
fileWriter.write("陈磊hahahahha",0,2);
```

## 节点流和处理流

![image-20211117122742192](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211117122742192.png)

![image-20211117122849721](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211117122849721.png)

## 处理流设计模式

![image-20211118145653702](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211118145653702.png)

 

![image-20211118215442778](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211118215442778.png)

![image-20211118215506992](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211118215506992.png)

![image-20211118215527210](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211118215527210.png)

![image-20211118215603489](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211118215603489.png)

![image-20211118215622611](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211118215622611.png)

![image-20211118215650488](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211118215650488.png)

![image-20211118221517590](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211118221517590.png)

## BufferedReader

![image-20211118221758258](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211118221758258.png)

![image-20211118222205849](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211118222205849.png)

## BufferedWriter

![image-20211119150154098](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119150154098.png)

## BufferedCopy

![image-20211119150659478](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119150659478.png)

## Buffered字节处理流

![image-20211119151306338](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119151306338.png)

![image-20211119151330573](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119151330573.png)

## 字节处理流Copy文件

![image-20211119153723340](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119153723340.png)

![image-20211119153735449](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119153735449.png)

![image-20211119153908232](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119153908232.png)

## 对象处理流

![image-20211119154240708](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119154240708.png)

![image-20211119164015208](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119164015208.png)

![image-20211119164105700](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211119164105700.png)

## ObjectOutputStream

```java
package HanSHunPin.chapter19;

import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;

public class ObjectOutStream_ {
    public static void main(String[] args) throws Exception {
        //序列化后，保存的文件格式，不是存文本，而是按照他的格式来保存
        String filePath = "C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\data.dat";

        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(filePath));
        //序列化数据到文件中
        oos.write(100);//int -> Integer(实现了 Serializable)
        oos.writeBoolean(true);//boolean ->Boolean(实现了 Serializable)
        oos.writeChar('a');//char->Character(实现了 Serializable)
        oos.writeDouble(9.5);//double->Double(实现了 Serializable)
        oos.writeUTF("哈嘿哈嘿哈嘿哈黑");//String(实现了 Serializable)
        //保存一个Dog对象
        oos.writeObject(new Dog("旺财",10));

        oos.close();
        System.out.println("数据保存完毕（序列化形式）");

    }
}

//如果需要序列化某个类的对象，实现 Serializable
class Dog implements Serializable {
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

    @Override
    public String toString() {
        return "Dog{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

## ObjectInputStream

```java
package HanSHunPin.chapter19;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.ObjectInputStream;

public class ObjectInputStream_ {
    public static void main(String[] args) throws Exception {
        //指定反序列化的文件
        String filePath = "C:\\Users\\admin\\Desktop\\JAVA路线\\JAVA_FIleTest\\data.dat";

        ObjectInputStream ois = new ObjectInputStream(new FileInputStream(filePath));

        //读取
        //1.读取（反序列化）的顺序需要和你保存数据（序列化）的顺序一致
        //2.否则会出现异常
        System.out.println(ois.readInt());
        System.out.println(ois.readBoolean());
        System.out.println(ois.readChar());
        System.out.println(ois.readDouble());
        System.out.println(ois.readUTF());
        Object o=ois.readObject();
        System.out.println("运行类型="+o.getClass());
        System.out.println("dog信息="+o);

        //这里是特别重要的细节：

        //1.如果我们希望调用DOg的方法，需要向下转型
        //2.需要我们将Dog类的定义，拷贝到可以引用的位置
        Dog dog2=(Dog)o;
        System.out.println(dog2.getName());

        //关闭流，关闭外层流即可，底层会关闭FIleInputStream
        ois.close();



    }
}
```

> 100
> true
> a
> 9.5
> 哈嘿哈嘿哈嘿哈黑
> 运行类型=class HanSHunPin.chapter19.Dog
> dog信息=Dog{name='旺财', age=10}
> 旺财

## 对象处理流使用细节

![image-20211120111103566](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120111103566.png)

```java
//serialVersionUID 序列化的版本号，可以提高兼容性
private static final long serialVersionUID=1L
```

## 标准输入输出流

![image-20211120120058356](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120120058356.png)

### 编译类型不等于运行类型

## 乱码引出转换流

![image-20211120121843734](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120121843734.png)

默认情况下，读取文件是按照 utf-8 编码,变了会乱码(根本问题是没有指定读取文件的编码方式)，为了解决这个问题，提出了转换流

## InputStreamReader

![image-20211120122506103](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120122506103.png)

![image-20211120122653396](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120122653396.png)

![image-20211120124902931](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120124902931.png)

![image-20211120125115903](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120125115903.png)

## OutputStreamWriter

![image-20211120125731148](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120125731148.png)

## PrintStream

### 打印流只有输出流，没有输入流

![image-20211120140804024](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120140804024.png)

![image-20211120140818971](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120140818971.png)

![image-20211120140908959](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120140908959.png)

 ![image-20211120141054438](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120141054438.png)

![image-20211120141222521](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120141222521.png)

![image-20211120141439700](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120141439700.png)

## PrintWriter

![image-20211120142836902](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120142836902.png)

![image-20211120142931590](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120142931590.png)

## 配置文件引出Properties

![image-20211120143531519](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120143531519.png)

![image-20211120143714769](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120143714769.png)

## Properties读文件

![image-20211120171247509](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120171247509.png)

![image-20211120171311904](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211120171311904.png)

```java
package HanSHunPin.chapter19;

import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.Properties;

public class Properties02 {
    public static void main(String[] args) throws IOException {
        //使用 Properties 类来读取 mysql.properties 文件

        //1.创建 Properties 对象
        Properties properties = new Properties();
        //2.加载指定配置文件
        properties.load(new FileReader("E:\\JAVAtest\\JavaSE\\BaseGrammar\\src\\mysql.properties"));
        //3.把 k-v 显示控制台
        properties.list(System.out);
        //4.根据 key 获取对应的值
        String user = properties.getProperty("user");
        String pwd = properties.getProperty("pwd");
        System.out.println("用户名=:"+user);
        System.out.println("密码=:"+pwd);


    }
}
```

> -- listing properties --
> user=root
> pwd=12345
> ip=192.168.100.100
> 用户名=:root
> 密码=:12345

## Properties修改文件

```java
package HanSHunPin.chapter19;


import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Properties;

public class Properties03 {
    public static void main(String[] args) throws IOException {
        //使用 Properties 类来创建 配置文件， 修改配置文件内容
        Properties properties = new Properties();
        //创建
        //1.如果该文件没有key 就是创建
        //2.如果该文件有key, 就是修改
        /*
        Properties父类是 Hashtable , 底层就是Hashtable 核心方法
         */
        properties.setProperty("charset","utf8");
        properties.setProperty("user","汤姆");//注意保存时， 是中文的 unicode码值
        properties.setProperty("pwd","abc111");

        //将 k-v 存储文件中即可
        properties.store(new FileOutputStream("E:\\JAVAtest\\JavaSE\\BaseGrammar\\src\\mysql2.properties"),"hello world");
        System.out.println("保存配置文件成功~");


    }
}
```

