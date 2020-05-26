
- 课程源：[p350](https://www.bilibili.com/video/av55246614/?p=350) ~[p393](https://www.bilibili.com/video/av55246614?p=393)

<!-- TOC -->

- [流（黑马）](#流黑马)
    - [字节输出流 （OutputStream）](#字节输出流-outputstream)
        - [文件字节输出流（FileOutputStream）](#文件字节输出流fileoutputstream)
        - [数据的追加写和换行写](#数据的追加写和换行写)
    - [字节输入流（InputStream）](#字节输入流inputstream)
        - [文件字节输入流 （FileInputStream）](#文件字节输入流-fileinputstream)
        - [练习：文件复制](#练习文件复制)
    - [字符流](#字符流)
        - [字符输入流（Reader）](#字符输入流reader)
        - [字符输出流 (Writer)](#字符输出流-writer)
        - [续写和换行写](#续写和换行写)
    - [属性集](#属性集)
    - [缓冲](#缓冲)
        - [字节缓冲流](#字节缓冲流)
        - [字符缓冲流](#字符缓冲流)
        - [练习：文本排序](#练习文本排序)
    - [转换流](#转换流)
        - [OutputStreamWriter](#outputstreamwriter)
        - [InputStreamReader](#inputstreamreader)
        - [练习：文件转码](#练习文件转码)
    - [对象流](#对象流)
        - [对象序列化](#对象序列化)
        - [对象反序列化](#对象反序列化)
    - [transient 关键字](#transient-关键字)
        - [InvalidClassException](#invalidclassexception)
        - [练习：序列化集合](#练习序列化集合)
    - [打印流](#打印流)
- [流（mooc）](#流mooc)
    - [数据流](#数据流)
    - [节点流](#节点流)
    - [过滤器流](#过滤器流)
        - [带缓冲的过滤器流](#带缓冲的过滤器流)
        - [数据输入输出流](#数据输入输出流)
    - [文件流](#文件流)
    - [字符流](#字符流)
    - [随机读写](#随机读写)
    - [对象I/O](#对象io)
    - [拷贝](#拷贝)
    - [移动和重命名](#移动和重命名)

<!-- /TOC -->

---

# 流（黑马）

## 字节输出流 （OutputStream）
    java.io.OutputStream
    最顶层的抽象类，定义了所有字节流的所有方法。
    定义了子类共性的方法。 close(),flush(),write(**)*3

### 文件字节输出流（FileOutputStream）

    继承了 OutputStream
    将内容写入到硬盘中

- 构造方法：  
  - FileOutputStream(String name): 创建一个具有指定名称的文件中写入输出文件流。
  - FileOutputStream(File file): 创建一个像指定File 对象表示文件中写入数据的文件输出流
- 参数：
  - name：目的地是文件的路径
  - file：目的地是一个文件
- 作用：
  1. 创建一个FileOutputStream 对象
  2. 根据传递的参数，创建一个空文件
  3. 会把输出流对象指向创建好的文件

写入数据的原理：
    由内存到硬盘： java程序 --> JVM --> OS --> 调用写数据的方法（OS） --> 写入文件

字节输出流写入步骤：

    1. 创建一个对象（传递写入数据的路径）  
    2. 调用对象中的write 方法，写入到文件中  
    3. 释放资源 （提高程序的效率）

```java
    // 1. 创建一个对象（传递写入数据的路径）  (相对路径)
    FileOutputStream fos = new FileOutputStream("09\\a.txt");
    //2. 调用对象中的write 方法，写入到文件中  
    fos.write(97);  //十进制 -> 二进制 （1100001）
    //3. 释放资源 （提高程序的效率）
    fos.close();
```

写入：
1. public void write(int a):
   
    记事本打开文件时查询编码表 字节 -> 字符
    0 - 127 ： ASCII 表
    其他：系统默认编码表（中文系统GBK表）

2. public void write(byte[] b):
   1. 如果写入第一个字节是整数（0-127） ，那么查询 ASCII表。
   2. 如果写入的是负数 ，第一个字节会和第二个字节组成一个中文显示，查询系统默认表。

3. public void write(byte [] b,int off, int len):
   1. 部分写入
   2. off 开始，len：长度

### 数据的追加写和换行写

追加/续写：

    FileOutputStream(String name ,boolean append)
    FileOutputStream(File file ,boolean append)

- append : 追加写开关 false:创建新文件，覆盖源文件

换行：

    windows ： \r\n
    linux : \n
    mac:: \r

## 字节输入流（InputStream）

    也是抽象类，定义了输入流子类共性的方法。
    read() * 2 , close()

### 文件字节输入流 （FileInputStream）

- 构造方法：
  - FileInputStream(String name)
  - FileInputStream(File file)
- 作用：
  - 创建一个FileInputStream 对象
  - 把对象指向要读取的文件
- 读取数据的原理： 硬盘 -> 内存

java程序 -> JVM -> OS -> 读取方法 ->读取文件

- 步骤：
  - 创建一个FileInputStream 对象，绑定数据源
  - 调用read方法读取文件
  - 释放资源

```java
    FileInputStream fin = new FileInputStream("src/liu/a.txt");
    int x;
    //读取一个字节
    x = fin.read();
    System.out.println(x);
    //文件结束 返回 -1 
    x = fin.read();
    System.out.println(x);
    
    /**
     * 1. fin.read() : 读取一个字符
     * 2. x = fin.read() 赋值
     * 3. 判断 x 是否等于 -1
     */
    while((x = fin.read()) != -1){
        System.out.println((char)x);
    }

    fin.close();
```

多字节读取

- int read(byte [] b)
  - 参数：byte[]  存放的数组（字节） 一般大小为 $\color{red}{1024(1KB)}$或者1024的整数倍
  - 返回值：int 返回读取的字节数
- String 构造方法
  - String（byte [] b）: 字符数组转换成 字符串
  - String (byte [] b,int off,int len): 一部分转化

```java

    /**
     * 多字节读取
     * byte 有时恰好汉字没有乱码
     */
    byte []  b = new byte[4];
    fin = new FileInputStream("src/liu/b.txt");
    while ((x = fin.read(b))!= -1){
        System.out.println(new String(b,0,x));
    }
```

### 练习：文件复制

1. 创建一个输入流对象，绑定读取数据源
2. 创建一个输出流对象，绑定目的地
3. 使用文件输入流 ，读取文件
4. 使用文件输出流 ，写入文件
5. 释放资源（先关闭写的，后关闭读的）
   
```java
package liu;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

/**
 * @author LiYang
 * @Project Name: bilibili
 * @Package Name: liu
 * Created by MacBook Air on 2020/02/25.
 * Copyright © 2020 LiYang. All rights reserved.
 * 字节流练习
 */
public class CopyFile {
    public static void main(String[] args) {
        try{
            FileInputStream fin = new FileInputStream("src/liu/2.jpeg");
            FileOutputStream fout = new FileOutputStream("src/1.jpeg",true);
            byte [] b = new byte[1024];
            while (fin.read(b) != -1){
                fout.write(b);
            }
            fout.close();
            fin.close();
        } catch (IOException e){
            System.out.println(e.getMessage());
        }
    }
}
```

## 字符流 

    java.io.Reader
    解决中文读取可能乱码的问题

    1个中文：
        GBK： 占2个字节
        UTF-8 ：占3个字节

### 字符输入流（Reader）

    抽象类
    共性成员的方法： close(),read()
> 层次：
- Reader
  -   InputStreamReader
        - FileReader
  
  FileReader FileInputStream 读取字节 -> FileReader转换成字符

> InputStream:文件字符输入流

- 构造方法：
  - FileReader(String filename)
  - FileReader(File file) 
- 参数： 
  - filename：文件路径
  - file：一个文件
- 作用：
  1. 创建一个FileReader对象
  2. 会把FileReader对象指向文件
- 使用步骤：
  - 创建一个对象，并绑定数据源
  - 使用对象读取文件
  - 释放资源
  
### 字符输出流 (Writer)

    java.io.Writer;
    flush ():刷新
    所有字符输出流的顶层类，是一个抽象类

> 层次
- java.io.Writer
  - java.io.OutputStreamWriter
    - java.io.FileWriter
  
```java
java.io.FileWriter extends OutputStreamWriter extends Writer
```

FileWriter： 文件字符输出流

作用：  将内存中的内容输入到磁盘中

- 构造方法：
  - FileWriter(String fielname)
  - FileWriter(File file)
- 参数
  - ...
- 作用
  - 创建一个对象
  - 根据传递的参数，创建一个文件
  - 对象指向创建的文件
- 使用步骤
  1. 创建一个对象，构造方法中绑定要写入的数据目的地
  2. 使用FileWriter中的Write，把数据写入到缓冲区中（字符转换成字节的过程）
  3. 使用FileWriter的方法，flush() ，把内存中数据刷新，刷新到文件中
  4. 释放资源（先将内存缓冲区中的数据刷新到文件中）
   
flush 与 close 的区别：
  - flush：刷新缓冲区，流对象可以继续使用
  - close：先刷新缓冲区，关闭流对象

### 续写和换行写

  FileWriter(String filename , boolean append);  
  FileWriter(File file , boolean append);
  
## 属性集

- java.lang.Object  
    - java.util.Dictionary<K,​V>  
      - java.util.Hashtable<Object,​Object>  
        - java.util.Properties

  是一个持久的属性集。Properties可以保存在流或从流中加载
  是唯一一个与IO流相结合的集合

- store() ： 把集合中的临时数据，持久化写入到硬盘中存储
  - public void store​(OutputStream out,String comments)
    - 不能写入中文
  - public void store​(Writer writer,String comments)
    - 可以写入中文
  - comments ： 注释文件的作用，不能使用中文，Unicode编码，通常为空字符串
- 使用步骤
  1. 创建Properties集合对象，添加数据
  2. 创建字节/字符输出流，构造方法绑定文件
  3. 使用Properties集合的方法 store，持久化写入硬盘
  4. 释放资源 

---

- load(): 把硬盘中保存的键值对，读取到内存中       
   -  public void load​(InputStream inStream)  
      -  字节输入流  不能读取含有中文的键值对
   -  public void load​(Reader reader)
      -  字符输入流  能读中文 
- 步骤
  1. 创建Properties 集合对象
  2. 使用Properties 集合对象中的方法Load读取文件的键值对
  3. 遍历Properties 集合
- 注意：
    1. 键值对文件中，键与值之间默认连接方式为 = 或者 空格 或者其他符号
    2. 键值对文件中，可以使用 # 进行注释
    3. 键值对文件中，键与值默认都是字符串


  是双列结合，Key和Value默认都是字符串

## 缓冲

### 字节缓冲流

  BufferedOutputStream ：字节缓冲输出流
- 构造方法：
  - public BufferedOutputStream​(OutputStream out)
  - public BufferedOutputStream​(OutputStream out,int size)
- 参数：
  - out：字节输出流
  - size： 自定缓冲流内部缓冲区的大小
- 作用：
  - 给OutputStream 创建一个缓冲区，提高写入效率
- 步骤
  1. 创建一个字节缓冲流，在构造方法中绑定目的地
  2. 创建缓冲流对象，构造方法中传递字节缓冲流，提高效率
  3. 使用write方法，把数据写入到内部缓冲区
  4. 使用flush方法，把数据刷新到文件中
  5. 释放资源

  BufferedInputStream : 字节缓冲输入流
- 构造方法：
  - public BufferedInputStream​(InputStream in)
  - public BufferedInputStream​(InputStream in,int size)
- 参数
  - in ： 字节输出流
  - size : 缓冲区大小
- 使用步骤
  1. 创建FileInputStream对象
  2. 创建BufferedInputStream对象，构造方法传递 FileInputStream对象
  3. 使用Buffered的read，读取文件
  4. 释放资源

### 字符缓冲流

- 字符缓冲输出流
  - BufferedWriter extends Writer
- 构造方法：
  - public BufferedWriter​(Writer out)
  - public BufferedWriter​(Writer out,int sz)
- 参数
  - out ： 字符输出流
  - sz ： 指定缓冲区的大小
- 方法
  - public void newLine() ： 写一个行分隔符
- 步骤
  1. 创建字符缓冲输出流对象，构造方法中传递字符输出流
  2. 调用缓冲流中的write方法啊，写入缓冲区
  3. 调用flush方法，刷新到磁盘文件
  4. 释放资源

- 字符缓冲输入流
  - BufferedReader
- 构造函数
  - BufferedReader​(Reader in)	
  - BufferedReader​(Reader in, int sz)
- 参数 
  - in ： 字符输入流
  - sz ： 大小
- 方法 
  - readLine() : 读一行

### 练习：文本排序

  分析：  
  1. 创建一个HashMap 集合对象，可以存储每行的文本序号（1，2，3...);value 存储每行的内容
  2. 创建字符缓冲输入流对象，构造方法绑定字符输入流
  3. 创建字符缓冲输出流对象，构造方法绑定字符输出流
  4. 使用字符缓冲输入流中的readline()方法，逐行读取文本内容
  5. 对读取到的文本进行切割，获取行号和文本内容，并存储到HashMap集合中（kay 自动排序）
  6. 遍历HashMap 获取键值
  7. 使用字符缓冲输出流中的writeLine() 方法，吸入文本
  8. 释放资源

## 转换流

- 编码： 字符 -> 字节
- 解码： 字节 -> 字符
- 字符集(编码表) Charset   
  - ASCII  
  - GBK （国标） 双字节编码
  - Unicode 万国码 (UTF8,16,32)

### OutputStreamWriter

- 继承了 Writer
- 是字符流通向字节流的桥梁，可是指定 charset 将要写入流中的字符编码成字节 (编码的过程)
- 构造方法
  - public OutputStreamWriter​(OutputStream out)
  - public OutputStreamWriter​(OutputStream out,String charsetName)
- 参数 
  - out : 字节输出流，可以用来写转换之后的字节到文件中
  - charsetName ： 编码表的名称 ，不区分大小写 utf-8 默认使用 utf-8
- 步骤
  1. 创建OutputStreamWriter​ 对象，构造方法中传递字节输出流，指定编码表名称
  2. 使用OutputStreamWriter ​对象中的 **Writer** 方法，把字符组转换成自己储存到缓冲区
  3. 使用OutputStreamWriter ​对象中的 **flush** 方法，把内存缓冲区中的字节刷新到文件中去
  4. 释放资源

### InputStreamReader

- 继承了 reader
- 构造方法
  - public InputStreamReader​(InputStream in)
  -  public InputStreamReader​(InputStream in,String charsetName)
- 参数 
  - in : 字节输入流，可以用来读文件中字节
  - charsetName ： 编码表的名称 ，不区分大小写 utf-8 默认使用 utf-8
- 步骤
  1. 创建对象，传参
  2. 使用read() 方法读取文件
  3. 释放资源
- 注意
  - 指定编码与文件的编码相同，否则会发生乱码
  
### 练习：文件转码

  1. 创建InputStreamReader对象，传递字节输入流
  2. 创建OutputStreamWriter对象，传递字节输出流
  3. 使用InputStreamReader 对象方法啊read 读文件
  4. 使用OutputStreamWriter 方法Write 写文件
  5. 释放资源

## 对象流

### 对象序列化

- 对象中不仅仅包含字符，使用字节流
- ObjectOutputStream
- 方法：
  - public final void writeObject​(Object obj)
    - throws IOException
- 步骤
  1. 创建ObjectOutputStream对象，传递输出流
  2. 使用ObjectOutputStream的 writeObject方法，把对象写入
  3. 释放资源
   
### 对象反序列化
- ObjectInputStream
  - public final Object readObject() 
    - throws IOException,ClassNotFoundException
- NotSerializableException 没有序列化异常
  - $\color{red}{Serializable}$ ：是一个接口，须有实该接口才能使用序列化功能。
  - 标记性接口，要进行序列化和反序列化的类必须实现该接口
  - 当序列化时需要检查该标记，没有抛出异常
- 步骤
  1. 创建ObjectInputStream对象，传递输入流
  2. 使用ObjectInputStream的 readObject方法，把对象读出
  3. 释放资源

## transient 关键字

- 瞬态关键字
- static： 静态关键字
  - 静态优先于非静态加载到内存中 (静态优先于对象进入到内存)
  - 被static 修饰的成员变量不能被序列化

```java
/**
 * 序列化标记型接口
 */
class Point implements Serializable{
    private int x;
    private static int y;
    transient int z;

    public Point(int x, int y,int z) {
        this.x = x;
        Point.y = y;
        this.z = z;
    }

    public void print(){
        System.out.println("(" +x+","+y+","+z+")");
    }
}
```

1. 对于y 是静态成员，需要用类名直接调用，不能够序列化写入到文件中
2. 对于z 是瞬态成员，需要用this直接调用，属于单个对象，也不能被序列化写入到文件中

### InvalidClassException

- 当类文件被修改时，.class 文件的序列号(serialVersionUID)会被修改，当直接进行反序列化时，文件中的序列号会找 .class 文件
  找不到：会抛出 __InvalidClassException__ 异常
- 解决方法：
  - 手动给类添加 序列号
  - The serialization runtime associates with each serializable class a version number, called a serialVersionUID, which is used during deserialization to verify that the sender and receiver of a serialized object have loaded classes for that object that are compatible with respect to serialization. If the receiver has loaded a class for the object that has a different serialVersionUID than that of the corresponding sender's class, then deserialization will result in an InvalidClassException. A serializable class can declare its own serialVersionUID explicitly by declaring a field named "serialVersionUID" $\color{red}{ that must be static, final, and of type long:}$
  
> ANY-ACCESS-MODIFIER static final long serialVersionUID = 42L;

### 练习：序列化集合

> ArrayListTest.java  
> ArrayListTest1.java

- 当我们想在文件中保存多个对象的时候  
  可以把多个对象储存到一个集合中  
  对集合进行序列化和反序列化
- 分析：
  1. 定义一个存储Point对象的ArrayList集合
  2. 往List中进行存储Point对象
  3. 创建一个序列化流 ObjectOutputStream 对象
  4. 写入（WriteObject）
  5. 创建反序列化对象
  6. 读出来 （ReadObject）
  7. 把Object类型的集合转化成 ArrayList集合
  8. 遍历
  9. 释放资源

## 打印流

- PrintStream​
  1. 只负责输出，不负责输入
  2. 永远不抛出 IOException
  3. 特有方法print(),println()
- 构造方法
  - public PrintStream​(File file)
  - public PrintStream​(OutputStream out)
  - public PrintStream​(String fileName)
- extends OutpuStream
- 注意
  - 使用父类的 write方法，会查询自己编码表 97 -> a
  - 使用自己特有的 print/println ，会输出原样 97 -> 97
- 可以改变打印的方向
  - System.setOut(PrintStream out)
- 示例:

```java
    System.out.println("我是控制台输出！");
    //PrintStream ps = new PrintStream("src/liu/c.txt");
    PrintStream ps = new PrintStream(new FileOutputStream("src/liu/d.txt"));
    //修改打印的位置
    System.setOut(ps);
    System.out.println("文件打印！");
```

FileOutputStream 会创建文件，但是依然需要抛出 **FileNotFoundException**


---

# 流（mooc）

## 数据流

    数据流是指应用程序与对象进行数据交换时的数据传输过程。
    字节流是按照字节读/写二进制数据。
    InputStream和OutputStream类是处理以8字节为基本单位的字节流，读写以字节为单位进行。
    Object：InputStream、OutputStream（字节流）；File（文件）；Reader、Writer（字符流）；RandomAccessFile（随机处理文件）

## 节点流

    节点流是直接与特定数据源相连的流，提供了访问该数据源的基本操作。

## 过滤器流

    1. 为了提高数据的处理速度
    2. 能对如：int、double之类的数据直接进行操作
    会联合使用被称为过滤器(Filter)流，提高留的处理效率。
    过滤器流不能够单独使用，必须与相应的节点流进行一起使用。

### 带缓冲的过滤器流

1. 计算机在读取或写入内存中数据时速度很快，而在读取或写入外部设备（键盘、显示器、文件等）时速度却慢得多。
2. 在IO操作中，为了提高数据的传输效率，通常使用带缓冲（ Buffered ）过滤器流。当向一个缓冲过滤器流写入数据时，系统将数据发送到缓冲区，而不是直接发送到外部设备。
3. BufferedInuputStream类和BufferedOutputStream就是两个常用的带缓冲的过滤器流。

### 数据输入输出流

当处理的数据为int等类型时，需要专门的数据输入输出流来处理。
DateInputStream 类和DateOutputStream类 能够直接读写Java基本类型的数据和Unicode编码格式的字符串。

## 文件流

1. FileInputStream

> * 打开一个输入文件，如果没有该文件会出现异常。
> * FileNotFoundException 是一个非运行时错误。

1. FileOutputSystem

> * 打开一个输出文件，如果没有该文件会创建一个文件；否则源文件的内容将全部重写。

3. 在I/O操作是会产生 **IOException**非运行时错误， 必须提前捕获。

```java
    //目录
    File file1 = new File("/user/test/");
    //file2、3 指向同一个文件
    File file2 - new File("/user/test/","a.txt");
    File file3 = new File(file1,"a.txt");

    try{
        File pPath = new File(System.getProperty("user.dir")+"/流/src/");
        File in = new File(pPath ,"FileInput.txt");
        File out = new File(pPath,"FileOut.txt");
        System.out.println(in);
        FileInputStream fin = new FileInputStream(in);
        FileOutputStream fout = new FileOutputStream(out);
        int textNu;
        while ((textNu = fin.read())!= -1) {
            fout.write(textNu);
            System.out.println(textNu);
        }
        fin.close();
        fout.close();
    } catch (FileNotFoundException e){
        System.out.println("Error:"+e.getMessage()); 
    }
```

## 字符流

InputStream 和OutStream 是字节流  
Reader和Writer是字符流

BufferReader 和 BufferWriter类 能提高读写处理速度。 

字节流放到字符流的处理器内，需要用到转换器。
InputStreamReader 是将输入的字节流转换成字符输入流。
OutStreamReader 是将输出的字节流转换成字符流输出。

## 随机读写

RandomAccessFile

允许文件同时完成读和写操作，它直接继承Object类  
并且实现了接口DataInput和DataOutput类  
类似存储在文件系统的一个大型的byte数组    
存在指向该隐含数组的光标或索引，成为文件指针。

提供了支持随机文件操作的方法：

> 1. readXXX()或者 writeXXX():如 ReadInt(),ReadLine(),WriteChar(),WriteDouble()等
> 2. int skipBytes(int n):将指针向下移动若干字节
> 3. length():返回文件长度
> 4. long getFilePointer():返回指针当前位置
> 5. void seek(long pos):将指针调用所需位置

构造函数：

```java
RandomAccessFile(File file,String mode)
RandomAccessFile(String name,String mode)
```

mode 的取值：

> * r:只读，任何写操作都讲抛出 IOException  
> * rw:读写，文件不存在时会创建该文件，文件存在是，原文件内容不变，通过写操作改变文件内容。  
> * rws:打开以便读取和写入，对于 "rw"，还要求对文件的内容或元数据的每个更新都同步写入到底层存储设备。  
> * rwd:打开以便读取和写入，对于 "rw"，还要求对文件内容的每个更新都同步写入到底层存储设备。  

## 对象I/O

Java 提供了Serializable的接口，只要实现了这一接口就可以使用ObjectInputStream和ObjectOutputStream 进行对象的输入输出。

## 拷贝

```java
    Path path1 = Paths.get("/home/project/1.txt");
    Path path2 = Paths.get("/home/project/2.txt");
    Files.copy(path1,path2, StandardCopyOption.REPLACE_EXISTING);
```

StandardCopyOption 属性：
options 中指定了REPLACE_EXISTING属性。当该命令复制目录时，如果目录中已经有了文件，目录中的文件将不会被复制。CopyOption 参数支持以下 StandardCopyOption 和 LinkOption 枚举：

> * REPLACE_EXISTING - 即使目标文件已存在，也执行复制。如果目标是符号链接，则复制链接本身（而不是链接的目标）。如果目标是非空目录，则复制将失败并显示 FileAlreadyExistsException 异常。
> * COPY_ATTRIBUTES - 将与文件关联的文件属性复制到目标文件。支持的确切- 文件属性是文件系统和平台相关的，但 last-modified-time 跨平台支持并复制到目标文件。 
> * NOFOLLOW_LINKS - 表示不应遵循符号链接。如果要复制的文件是符号链接，则复制链接（而不是链接的目标）。

## 移动和重命名

```java
    Files.move(Path,Path,StandardCopyOption);
```
> * REPLACE_EXISTING - 即使目标文件已存在，也执行移动。如果目标是符号链接，则替换符号链接，但它指向的内容不受影响。
> * ATOMIC_MOVE - 将移动作为原子文件操作执行。如果文件系统不支持原子移动，则抛出异常。使用，ATOMIC_MOVE 您可以将文件移动到目录中，并保证观察目录的任何进程都可以访问完整的文件。



