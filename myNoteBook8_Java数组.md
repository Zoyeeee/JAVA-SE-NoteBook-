## Java数组

### 什么是数组

---

![image-20211022144328007](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211022144328007.png)

### 数组的声明和创建

---

![image-20211022144603873](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211022144603873.png)

![image-20211022145243592](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211022145243592.png)

#### int类型默认值0;string类型默认值null

```java
package test.test2.array;

public class ArrayDemo01 {
    public static void main(String[] args) {
        int[] nums;//1.定义
        int nums2[];
        nums = new int[10];//这里面可以存放10个int类型的数字  2.创建一个数组

        //3.给数组元素中幅值
        nums[0]=1;
        nums[1]=2;
        nums[2]=3;
        nums[3]=4;
        nums[4]=5;
        nums[5]=6;
        nums[6]=7;
        nums[7]=8;
        nums[8]=9;
        nums[9]=10;
        //计算所有元素的和
        int sum=0;
        
        //获取数组长度： arrays.length
        for(int i=0;i<nums.length;++i){
            sum=sum+nums[i];
        }
        System.out.println(sum);

    }
}

```

> 55

### 三种初始化及内存分析

---

#### 内存分析：

![image-20211022173529211](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211022173529211.png)

![image-20211023100253128](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023100253128.png)

#### 三种初始化：

![image-20211023100446468](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023100446468.png)

### 下标越界及小结

---

#### 数组的四个基本特点

![image-20211023101129795](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023101129795.png)

#### 数组边界

![image-20211023101344213](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023101344213.png)

### 数组的使用

---

#### 0. 普通循环使用

```java
package test.test2.array;

public class ArrayDemo03 {
    public static void main(String[] args) {
        int[] arrays={1,2,3,4,5};

        //打印全部的数组元素
        for (int i = 0; i < arrays.length; i++) {
            System.out.println(arrays[i]);
        }
        System.out.println("================");
        //计算所有元素的和
        int sum=0;
        for (int i = 0; i < arrays.length; i++) {
            sum+=arrays[i];
        }
        System.out.println(sum);
        System.out.println("================");
        //查找最大元素
        int max=arrays[0];
        for (int i = 1; i < arrays.length; i++) {
            if(max<=arrays[i]){
                max=arrays[i];
            }
        }
        System.out.println(max);
    }
}

```

> 1
> 2
> 3
> 4
> 5
---
> 15
---
> 5

#### 1. For-Each循环

快捷键arrays.for

#### 2. 数组作方法入参

#### 3. 数组作返回值

```java
package test.test2.array;

public class ArrayDemo04 {
    public static void main(String[] args) {
        int[] arrays={1,2,3,4,5};

//        //JDK1.5 没有下标
//        for (int array : arrays) {
//            System.out.println(array);
//        }

        printArray(arrays);
        System.out.println();
        printArray(reverse(arrays));


    }



    //打印数组元素
    public static void printArray(int[] arrays){
        for (int i = 0; i < arrays.length; i++) {
            System.out.print(arrays[i]+" ");
        }
    }

    //反转数组(自写)
//    public static int[] reverse(int[] arrays){
//        int[] myarrays=new int[arrays.length];
//        int count=0;
//        for (int i = arrays.length-1; i >0 ; i--) {
//            myarrays[count]=arrays[i];
//            count++;
//        }
//        return myarrays;
//    }


    //反转数组(老师)
    public static int[] reverse(int[] arrays){
        int[] result = new int[arrays.length];
        //反转的操作
        for (int i = 0,j=result.length-1; i < arrays.length; i++,j--) {
            result[i]=arrays[j];

        }


        return result;
    }
}

```

> 1 2 3 4 5 
> 5 4 3 2 1 

### 二维数组

---

![ ](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023104739451.png)

 ![image-20211023104929084](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023104929084.png)

```java
package test.test2.array;

public class ArrayDemo05 {
    public static void main(String[] args) {
        int[][] array={{1,2},{2,3},{3,4},{4,5}};
        System.out.println(array.length);
        System.out.println(array[0].length);


        System.out.println("===============");

        System.out.println(array[0]);
        printArray(array[0]);
        System.out.println();

        System.out.println("===============");

        for (int i = 0; i < array.length; i++) {
            for (int j = 0; j < array[i].length; j++) {
                System.out.println(array[i][j]);
            }
        }


    }

    
    public static void printArray(int[] arrays){
        for (int i = 0; i < arrays.length; i++) {
            System.out.print(arrays[i]+" ");
        }
    }
}

```

> 4
> 2
>
> [I@1b6d3586
> 1 2 
> 
> 1
> 2
> 2
> 3
> 3
> 4
> 4
> 5
>
> Process finished with exit code 0

### Arrays类讲解

---

![image-20211023130246278](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023130246278.png)

![image-20211023133513693](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023133513693.png)

### 冒泡排序

---

![image-20211023133621906](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023133621906.png)

```java
package test.test2.array;

public class ArrayDemo07 {
    public static void main(String[] args) {
        int[] arrays={5,4,3,2,1};
        int[] sort = sort(arrays);
        printArray(sort);

    }

    //冒泡排序
    //1.比较数组中，两个相邻的元素。如果第一个数比第二个数大，我们就交换他们的位置
    //2.每一次比较，都会产生出一个最大，或者最小的数字
    //3.下一轮则，可以少一次排序
    //4.依次循环，直到结束
    public static int[] sort(int[] array){
        int temp=array[0];
        //外层循环，判断我们这个要走多少次；
        for (int i = 0; i < array.length-1; i++) {
            boolean flag=false;//通过flag标识位减少没有意义的比较


            //内层循环，比较判断两个数，如果第一个数，比第二个数大，则交换位置
            for (int j = 0; j < array.length-1-i; j++) {
                if (array[j]>array[j+1]) {
                    temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;
                    flag=true;
                }
            }

            if (flag==false){
                break;
            }
        }
        return array;

    }


    public static void printArray(int[] arrays){
        for (int i = 0; i < arrays.length; i++) {
            System.out.print(arrays[i]+" ");
        }
    }
}

```

> 1 2 3 4 5 

### 稀疏数组(数据结构)

---

![image-20211023141007968](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023141007968.png)

![image-20211023141144380](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20211023141144380.png)

```java
package test.test2.array;

public class ArrayDemo08 {
    public static void main(String[] args) {
        //1.创建一个二维数组11*11   0:没有棋子   1:黑棋  2:白棋
        int[][] array1=new int[11][11];
        array1[1][2]=1;
        array1[2][3]=2;
        //输出原始数组
        System.out.println("输出原始数组");
        for (int[] ints : array1) {
            for (int anInt : ints) {
                System.out.print(anInt+"\t");
            }
            System.out.println();
        }

        System.out.println("===========================");
        //转换为稀疏数组来保存
        //获取有效值的个数
        int sum=0;
        for (int i = 0; i < array1.length; i++) {
            for (int j = 0; j < array1[0].length; j++) {
                if(array1[i][j]!=0){
                    sum++;
                }

            }

        }
        System.out.println("有效值的个数:"+sum);

        //2.创建一个稀疏数组的数组
        int[][] array2 = new int[sum+1][3];
        array2[0][0]=11;
        array2[0][1]=11;
        array2[0][2]=sum;

        //遍历二维数组，将非零的值，存放稀疏数组中
        int count=0;
        for (int i = 0; i < array1.length; i++) {
            for (int j = 0; j < array1[i].length; j++) {
                if (array1[i][j]!=0){
                    count++;
                    array2[count][0]=i;
                    array2[count][1]=j;
                    array2[count][2]=array1[i][j];

                }
            }

        }

        //输出稀疏数组
        System.out.println("稀疏数组");

        for (int i = 0; i < array2.length; i++) {
            for (int j = 0; j < array2[i].length; j++) {
                System.out.print(array2[i][j]+" ");
            }
            System.out.println();
        }
        System.out.printf("======================");

        //稀疏数组还原
        System.out.println();
        System.out.println("还原");
        //1.读取稀疏数组
        int[][] array3=new int[array2[0][0]][array2[0][1]];

        //2.给其中的元素还原它的值
        for (int i = 1; i < array2.length; i++) {
            array3[array2[i][0]][array2[i][1]]=array2[i][2];
        }

        //3.输出还原数组
        for (int i = 0; i < array3.length; i++) {
            for (int j = 0; j < array3[i].length; j++) {
                System.out.print(array3[i][j]+" ");
            }
            System.out.println();
        }
    }
}

```

> 输出原始数组
> 0	0	0	0	0	0	0	0	0	0	0	
> 0	0	1	0	0	0	0	0	0	0	0	
> 0	0	0	2	0	0	0	0	0	0	0	
> 0	0	0	0	0	0	0	0	0	0	0	
> 0	0	0	0	0	0	0	0	0	0	0	
> 0	0	0	0	0	0	0	0	0	0	0	
> 0	0	0	0	0	0	0	0	0	0	0	
> 0	0	0	0	0	0	0	0	0	0	0	
> 0	0	0	0	0	0	0	0	0	0	0	
> 0	0	0	0	0	0	0	0	0	0	0	
> 0	0	0	0	0	0	0	0	0	0	0	
>  \===========================
> 有效值的个数:2
> 稀疏数组
> 11 11 2 
> 1 2 1 
> 2 3 2 
>   \======================
> 还原
> 0 0 0 0 0 0 0 0 0 0 0 
> 0 0 1 0 0 0 0 0 0 0 0 
> 0 0 0 2 0 0 0 0 0 0 0 
> 0 0 0 0 0 0 0 0 0 0 0 
> 0 0 0 0 0 0 0 0 0 0 0 
> 0 0 0 0 0 0 0 0 0 0 0 
> 0 0 0 0 0 0 0 0 0 0 0 
> 0 0 0 0 0 0 0 0 0 0 0 
> 0 0 0 0 0 0 0 0 0 0 0 
> 0 0 0 0 0 0 0 0 0 0 0 
> 0 0 0 0 0 0 0 0 0 0 0 
>
> Process finished with exit code 0

