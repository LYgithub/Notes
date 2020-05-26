<!-- TOC -->

- [Java的Terminal执行](#java的terminal执行)
- [数据类型](#数据类型)
    - [基本数据类型](#基本数据类型)
    - [数据输入](#数据输入)
- [执行结构](#执行结构)
    - [跳转语句](#跳转语句)
- [Math类](#math类)
    - [Math类与数学函数](#math类与数学函数)
- [字符串](#字符串)
    - [比较](#比较)
    - [常用方法](#常用方法)
    - [StringBuffer](#stringbuffer)
    - [Random 类](#random-类)
- [时间和日历](#时间和日历)
    - [Date类](#date类)
    - [Calendar类](#calendar类)
- [类](#类)
    - [基本规则](#基本规则)
    - [构造函数](#构造函数)
    - [类变量与类方法](#类变量与类方法)
    - [类的继承](#类的继承)
    - [$\color{#189}{方法覆盖}$](#\color189方法覆盖)
    - [$\color{#189}{方法重载}$](#\color189方法重载)
    - [多态性](#多态性)
        - [$\color{red}{多态的实现方式：}$](#\colorred多态的实现方式)
    - [判断数据类型方法（[obj] instanceof [class]）](#判断数据类型方法obj-instanceof-class)
    - [类的封装性](#类的封装性)
    - [抽象类](#抽象类)
    - [final类](#final类)
    - [接口](#接口)
    - [类和接口](#类和接口)
    - [内部类](#内部类)
    - [匿名内部类](#匿名内部类)
    - [Object类](#object类)
- [图形化界面](#图形化界面)
    - [$\color{#099}{组件和容器}$](#\color099组件和容器)
    - [窗体程序的创建](#窗体程序的创建)
    - [$\color{#188}{Button创建}$](#\color188button创建)
    - [$\color{#189}{登录页面}$](#\color189登录页面)
    - [$\color{#189}{GUI事件}$](#\color189gui事件)
        - [委托模型](#委托模型)
    - [事件源对象](#事件源对象)
    - [事件适配器](#事件适配器)
    - [使用多个窗体](#使用多个窗体)
    - [组件布局（布局管理器管理）](#组件布局布局管理器管理)
        - [FlowLayout](#flowlayout)
        - [BorderLayout](#borderlayout)
        - [GridLayout](#gridlayout)
        - [CardLagout](#cardlagout)
        - [无布局管理](#无布局管理)
        - [复杂的布局](#复杂的布局)
    - [$\color {#199}{控件}$](#\color-199控件)
    - [例子](#例子)
- [异常及其分类](#异常及其分类)
    - [错误和异常](#错误和异常)
    - [自定义异常](#自定义异常)
- [多进程](#多进程)
    - [线程的调度和控制](#线程的调度和控制)
    - [线程变量](#线程变量)
    - [线程同步](#线程同步)
        - [Synchronized](#synchronized)

<!-- /TOC -->
---

## Java的Terminal执行

1. 创建 `.java`文件
   1. 命令：vim filename.java
   2. 注意：文件名与类名一致

2. 将源文件编译成字解码文件
   1. 命令： java filename.java
   2. 结果：生成`.class` 文件

3. 执行过程  
   1. java filename
   2. 注意：`没有后缀`

    ![Java1_1](https://gitee.com/KawYang/Notes/raw/master/Image/Java/Java1_1.png)

## 数据类型

### 基本数据类型

```java
public class Main{
    public static void main(String []args){
        int x,y,sum;
        x = 3;
        y = 5;
        sum = x + y;
        System.out.println(sum);
    }
}
```

### 数据输入

```java
    Scanner reader = new Scanner(System.in);
    //reader.next()  读取一个单词 ，charAt 是第几个字符，字从0 开始编号
    char x = reader.next().charAt(0);
    int a = reader.nextInt();
```

## 执行结构

### 跳转语句

- continue: $\color{red}{不使用“返回值”时}$ 表示跳出该次循环，即之后的代码不在执行。  
但是，该语句可以通过 指定跳转位置，改变跳转的方向

```java
     /**
     * 跳转指令
     */
    public static void GoTo(){
        outer:for (int j = 0; j < 10 ; j++) {
            //不用参数时continue 返回的位置  
            for (int i = 0; i<10;i++){
                    if (i>5) {
                    System.out.println(j+" "+ i);
                    continue outer;
                }
            }
        }
    }
    public static void GoTo(){
        for (int j = 0; j < 10 ; j++) {
            for (int i = 0; i<10;i++){
                if (i>5) {
                    System.out.println(j+" "+ i);
                    break;
                }
            }
        }
    }
```

- 以上代码通过 $\color{red}{outer:}$ 指定了continue的跳转位置，所以在此处相当于$\color{red}{break}$
  - 通过该方法可以跳出多重循环。 $\color{red}{但区别于 GOTO语句}$

```java
    /**
     * 跳转指令
     */
    public static void GoTo(){
        test:for (int j = 0; j < 10 ; j++) {
            for (int i = 0; i<10;i++){
                for(int px = 1;px <10;px++) {
                    if (i > 5) {
                        System.out.println(j + " " + i);
                        continue test;
                    }
                }
            }
        }

    }
```

## Math类

### Math类与数学函数

![Math_1](https://gitee.com/KawYang/Notes/raw/master/Image/Java/Math_1.png)
![Math_2](https://gitee.com/KawYang/Notes/raw/master/Image/Java/Math_2.png)
![Math_3](https://gitee.com/KawYang/Notes/raw/master/Image/Java/Math_3.png)

## 字符串

String 不可变  
声明：直接赋值或者new一个

```java
String s1 = "abc";
String s2 = "abc";
String s3 = new String ("abc");
String s4 = new String ("abc");
```

区别：

- 执行完 s1 会在字符池 创建一个“abc”字符串
- 执行s2 会在字符池中查找是否有一样的字符串。有将首地址赋给s2

- s3 和 s4 new了两个不同的存储空间，所以不在一个区域。
  
### 比较

- == ：比地址不必内容
- equals() :比较内容
- equalsIgnoreCase() :忽略大小写比较
  - //如果其他语言不提供可以将字符串都转换成小写后比较
- compareTo() : 比较大小（0，+，—）
- compareToIgnoreCase(): 忽略大小写

```java
    public static void main(String[] args) {
        String s1 = "abc";
        String s2 = "abc";
        String s3 = "ABC";
        String s4 = new String("abc");
        System.out.println("s1.compareTo(s2):"+s1.compareTo(s2));
        System.out.println("s1.compareToIgnoreCase(s3):"+s1.compareToIgnoreCase(s3));
        //比较的是地址啊
        System.out.println("s1 == s2:"+ (s1 == s2));
        //比较的是内容
        System.out.println("s1.equals(s2):"+ s1.equals(s2));
        //忽略大小写比较
        System.out.println("s1.equalsIgnoreCase(s3):"+s1.equalsIgnoreCase(s3));
        System.out.println("s1 == s4:"+(s1 == s4));
        System.out.println("s1.equals(s4):"+s1.equals(s4));
    }
```

```vim
String s1 = "abc";
String s2 = "abc"
String s3 = "ABC";
String s4 = new String("abc");
------------------------------
s1.compareTo(s2):0
s1.compareToIgnoreCase(s3):0
s1 == s2:true
s1.equals(s2):true
s1.equalsIgnoreCase(s3):true
s1 == s4:false
s1.equals(s4):true
```

### 常用方法

- 长度 ： length()  
- 连接 ：+ or concat()  
- 判断开头结尾 ：
  - startsWith()  
  - endsWith()
- 取子串：
  - (从第几个字符开始截取,结束)
  - 左闭右开
  - substring(int,int)

![String_1](https://gitee.com/KawYang/Notes/raw/master/Image/Java/String_1.png)

![String_2](https://gitee.com/KawYang/Notes/raw/master/Image/Java/String_2.png)

### StringBuffer

字符串可以修改

```java
    public static void main(String[] args) {
        StringBuffer s1 = new StringBuffer();
        s1.append("Hello");
        s1.append("World!");
        //HelloWorld!
        s1.insert(5," ");
        //Hello World!
        s1.replace(11,12,"?");
        //Hello World?
        s1.delete(0,6);
        // World?
    }
```

### Random 类

- Random random = new Random(int a);  
//a 是种子
- random.nextInt(int b)  
//b 是生成的范围（从0开始到b）$\color{red}{「左闭右开」}$

```java
    public static void main(String[] args) {
        try{

            Random random1 = new Random         (1);
            Random random2 = new Random(1);
            for (int i = 0; i < 10; i++) {
                System.out.print(random1.nextInt(10)+"\t");
            }
            System.out.println();
            Thread.sleep(1000);
            for (int i = 0; i < 10; i++) {
                System.out.print(random2.nextInt(10)+"\t");
            }
            System.out.println();

        }catch (Exception e){
            System.out.println(e);
            e.printStackTrace();
        }
    }
```

## 时间和日历

### Date类

yy :年  MM :月  dd :日  
E : 星期  G：公元  
HH:时  mm:分  ss:秒

```java
    public static void DateTest(){

        Date date = new Date();
        System.out.println(date);
        String patten = "yy-MM-dd";
        SimpleDateFormat sdf = new SimpleDateFormat(patten);
        String timePattern = sdf.format(date);
        System.out.println(timePattern);
        patten = "yyyy年MM月dd日,E HH时mm分ss秒";
        sdf = new SimpleDateFormat(patten);
        timePattern = sdf.format(date);
        System.out.println(timePattern);
    }
```

### Calendar类

$\color{red}{(calendar.get(Calendar.DAY\_OF\_WEEK)+6)\%7 }$

```java

    public static void CalendarTest(){

        Calendar calendar = Calendar.getInstance();
        /**
         *  日期
         */
        //或者calender.get(1);
        int year = calendar.get(Calendar.YEAR);
        //从0开始
        int month = calendar.get(Calendar.MONTH)+1;
        int day = calendar.get(Calendar.DATE);
        System.out.println(year+"年"+month+"月"+day+"日");
        /**
         *  时间
         */
        //Calendar.HOUR 是12 进制 HOUR_OF_DAY 24小时制
        int hour = calendar.get(Calendar.HOUR_OF_DAY);
        int minute = calendar.get(Calendar.MINUTE);
        int second = calendar.get(Calendar.SECOND);
        System.out.println(hour+":"+minute+":"+second);
        //日期设置
        calendar.set(2007,11,21);
        System.out.println(calendar.get(Calendar.MONTH));

        //星期 一 -> 2
        //星期 六 -> 7
        //星期 日 -> 1
        System.out.println((calendar.get(Calendar.DAY_OF_WEEK)+6)%7);
    }
```

## 类

### 基本规则

自定义的数据类型，包含属性和操作
> (首字母大写，变量和方法首字母小写)
> 变量用名词或者形容词
> 方法名用动词
> 返回值是boolen型 明前加is
> 名有多个单词，除首单词外，其余单词首字母大写

```java
class Point {
    int x,y;
    move(int x,int y);
    show();
}
```

### 构造函数

### 类变量与类方法

实例变量：创建对象时，分配内存，通过对象访问这些对象  
类变量：在常见第一个类时分配空间，和其他类共享  
类变量和类方法何以通过对象访问也可通过类名进行访问

```java
    class Point{
        static int color;
        static void move();
    }
```

### 类的继承

> 关键字 extends
> 子类不能继承父类的构造方法
> Object 是全部对象的父类
> 无多重继承

$\color{yellow}{C++对于多继承采用虚继承的方法，解决同时继承两个相同的数据成员和方法的问题}$  
[C++多继承](https://blog.csdn.net/yhc166188/article/details/81587968)

```java
/**
 * @author LiYang
 * @Project Name: JavaTest
 * @Package Name: PACKAGE_NAME
 * Created by MacBook Air on 2020/02/10.
 * Copyright © 2020 LiYang. All rights reserved.
 */
public class _emend {
    public static void main(String[] args) {
        Shape shape = new Shape("red",12.5);
        shape.print();
        Line line = new Line("red",12.5,10.5);
        line.print();
    }
}

class Shape {
    private String color;
    private double width;
    Shape(){}
    Shape(String color, double width){this.color=color;this.width=width;}
    String getColor(){return color;}
    double getWidth(){return width;}
    void setColor(String color){this.color = color;}
    void setWidth(double width){this.width = width;}

    void print(){
        System.out.println("颜色为："+color+"\n宽度为："+width);
    }
}

class Line extends Shape {
    private double length;
    Line(){}
    Line(String color, double width, double length){
        //调用父类构造函数
        super(color,width);
        // setColor(color);
        // setWidth(width);
        this.length = length;
    }
    public void print(){
        //使用super调用父程序同名方法
        super.print();
        System.out.println("长度为："+this.length);
    }
}

//矩形类
// ...
//正方形类
```



### $\color{#189}{方法覆盖}$

在子类中创建与父类同名、同参数的方法即为方法覆盖  
$\color{red}{super关键字可以调用父类被覆盖的方法}$  
this关键字则调用子类创建的方法

约束：
1. 一致声明(名称、参数)
2. 不低于基类访问权限
3. 抛出的异常类型不能比原方法多

### $\color{#189}{方法重载}$

Java 也通过参数的类型区别方法  
重载：方法名相同，参数不同：个数、类型、次序不同  
$\color{red}{不包括返回值}$

```java
    class Fushu{
        double shi,xu;
        Fushu add(Fushu f){
            Fushu f1;
            f1 = new Fushu();
            f1.shi = f.shi + shi;
            f1.xu = f.xu + xu;
            return f1;
        }
        Fushu add(double f){
            Fushu f1;
            f1 = new Fushu();
            f1.shi = f + shi;
            f1.xu = xu;
            return f1;
        }
    }
```

### 多态性

多态性是指一个方法可以有多种实现版本，$\color{red}{“一种定义，多种实现”}$

![Class_1](https://gitee.com/KawYang/Notes/raw/master/Image/Java/class_1.png)

 > 创建一个鸟🐦类A，申请一个大雁的对象赋值给A，A可以调用大雁下蛋的方法。
 同样将A对象，申请一个鸭的对象赋值给A，A又可以调用鸭的下蛋的方法。  
 如果唐老鸭也下蛋的话，依旧可以调用下蛋方法。
 这样对象A就表现出两种不同的下蛋方法，即多态  
 
$\color{red}{鸭属于鸟，但鸟不一定属于鸭}$  
所以，鸭对象可以赋值给鸟类变量；但是鸟对象不能赋值给鸭变量。  

$\color{red}{只能调用鸟(A))类中含有的方法}$  
如果要调用之类中新创建的方法，需要进行强制数据类型转换

#### $\color{red}{多态的实现方式：}$
1. 方法重载，是一种静态的实现方式
2. 类的继承，通过方法的覆盖实现的多态，特别的Object类使我们所有类的父类
3. 接口，首先解决的是多继承的问题，更重要的是给出了不同类对象之间多态实现的方式。

### 判断数据类型方法（[obj] instanceof [class]）

### 类的封装性

合理的访问、屏蔽实现的细节

| 是否能访问  | 同一个类中 | 同一个包中 | 不同包中子类 | 不同包中非子类 |
| :---------: | :--------: | :--------: | :----------: | :------------: |
|   private   |     ✅      |     ❌      |      ❌       |       ❌        |
| （default） |     ✅      |     ✅      |      ❌       |       ❌        |
|  protected  |     ✅      |     ✅      |      ✅       |       ❌        |
|   public    |     ✅      |     ✅      |      ✅       |       ✅        |

### 抽象类

抽象类永远不能被实例化  
只做继承过程中作为超类使用，不能实例化抽象类的对象。  
关键字 ： abstract 
抽象方法只声明，没有方法体；  
包含抽象方法的类一定是抽象类；  
抽象类中可以包含非抽象方法。  
抽象类无法实例化，含有子类共有的属性和方法。  
子类中必须将抽象的方法实例化。
使用多态进行使用。
 
```java
abstract class Shape{
    //抽象方法
    abstract void Print();
}
```

```java
public class _extends {
    public static void main(String[] args) {
        Shape shape;
        //多态实现
        shape = new Line("red",12.5,10.5);
        shape.print();
        shape = new LinePro();
        shape.print();
        //#
    }
}

abstract class Shape {
    private String color;
    private double width;
    public Shape(){}
    Shape(String color, double width){this.color=color;this.width=width;}
    String getColor(){return color;}
    double getWidth(){return width;}
    void setColor(String color){this.color = color;}
    void setWidth(double width){this.width = width;}
    //抽象方法
    abstract void print();
}

class Line extends Shape {
    private double length;
    Line(){}
    Line(String color, double width, double length){
        super("sd",123.3);
        setColor(color);
        setWidth(width);
        this.length = length;
    }
    //子类中将抽象方法实现
    public void print(){
        System.out.println("颜色为："+super.getColor()+"\n宽度为："+super.getWidth()+"\n----");
        System.out.println("线的颜色是:"+this.getColor()+"\n宽度为："+this.getWidth()+"\n长度为："+this.length);
    }
}

class LinePro extends Line{
    double pro;
    public void print(){
        super.print();
        System.out.println(pro);
    }
}
```

### final类

不能被继承的类
例如：String类就不能继承
final可以防止程序员创建绕过安全限制的子类

> final方法

类可以继承，但是方法不允许修改，可以创建final方法

> final 属性

常量、命名全部大写、单词间_分隔

> 空白final属性  (不设置初值)

只能在构造函数内赋值

### 接口

关键字：interface
创建方法与类创建相似
在接口中，所有的方法都是抽象方法（可以理解为抽象类）
主要用于创建类和类之间的一个“协议”
类虽然不同，但是有着一些共同的方法

![interface_1](https://gitee.com/KawYang/Notes/raw/master/Image/Java/interface_1.png)

```java
interface Flyer{
    public abstract void takeoff();
    //规定只能是 public abstract 类型
    void land();
}

class Airplane implements Flyer{
    int x;
    double y;
    //实现方法
    public void takeoff(){

    }
    public void land(){

    }
    //#
    void other(){

    }
}
```

注意：
> * 接口实现只能用 **public**  
> * 抽象类可以不用实现接口中全部的方法**abstract**  
> * 接口也可以添加数据成员，默认为**public static final**
> * 可以实现不相关两个对象通过多态处理

### 类和接口

1. 类是实例的抽象
2. 接口是规则、标准的集合
3. 接口可以多重继承、类只有一个父类

$\color{red}{抽象类和接口的不同}$

1. 抽象类约定多个子类；接口约定不同关系的方法
2. 抽象类含有普通类访问权限的成员；接口中所有成员访问权限都是 public
3. 抽象类里边包含非抽象方法；接口中全部都是抽象方法
4. 抽象类可以声明成员变量；接口只能声明常量

$\color{red}{抽象类和接口相同点}$

1) 都含有抽象方法
2) 都不能实例化

### 内部类

类的嵌套，同样具有类的所有属性，在一个类里边进行声明一个类  
用 ``.`` 进行访问。如Line.Point

```java
class Line{
    Point x1,x2;
    void printf(){

    }
    //内部类
    protected class Point{
        protected int x,y;
        protected void print(){
            System.out.println("("+x+","+y+")");
        }
    }
}
```

当声明“委托”(函数传递的参数为类的名称「new ClassName」)时,内部类与外部类名称相同，会首先传递内部类

### 匿名内部类

当某个类在创建的时候只是用一次，可以在使用语句中直接定义，不必为类命名。

```java
    fr.addWindowListener(new WindowAdapter(){
        public void windoClosing(WindowEvent e){
            System.exit(0);
        }
    });
```
程序会监测到WindowAdapter是一个接口(??)，不能声明，就会解析为继承的某个类。  
相当于 ``WindowAdapter f = new SonName();``(多态)

匿名为了编译器减少垃圾的生成。(有名关联内容较多)

### Object类

在Object类内设置了一些通用的方法。

1. protect void finalize(); 回收内存 析构函数？？
2. public String toString(); 返回字符串形式
3. public boolean equals(Object object); 比较两个对象是否“相等” （类型相同比较地址地址）
4. public int comperTo(Object object); 比较两个对象的大小（返回 0 ，+ ，-）
5. 

```java
public class objected {
    public static void main(String[] args) {
        Person person1 = new Person(110,20,true);
        Person person2 = new Person(120,21,true);
        System.out.println(person1.comperTo(person2));
        System.out.println(person1.equals(person2));
    }
}

class Person{
    int tall,age;
    boolean gender;
    Person(int tall,int age,boolean gender){
        this.tall = tall;
        this.age = age;
        this.gender = gender;
    }
    Person(){
        this(120,20,true);
    }
    //重写 Object 中的 equals 函数
    public boolean equals(Object b){
        return tall == ((Person)b).tall;
    }
    //重写 Object 中的 comperTo 函数
    public int comperTo(Object b){
        return age - ((Person)b).age;
    }
}
```

---

## 图形化界面

### $\color{#099}{组件和容器}$

抽象窗口工具包 AWT  
Swing

AWT容器：
| 基本组件 |   名称   |                                        |     |
| :------: | :------: | :------------------------------------- | --- |
| window类 |  窗口类  | 无边框和标题,不能附加到其他的容器      |     |
| Frame类  |  框架类  | 可以有一个菜单条，否则与window十分相似 |     |
| Dailog类 | 对话框类 | 只有在一个相应的Frame类存在才存在      |     |
| Panel类  |  面板类  | 在窗口里边进行划分                     |     |

控件

Button、Label、TextField、TextArea。。。

![Form_0](https://gitee.com/KawYang/Notes/raw/master/Image/Java/Form_0.png)
![Form_1](https://gitee.com/KawYang/Notes/raw/master/Image/Java/Form_1.png)

### 窗体程序的创建

使用控件直接申请，创建相应对象，然后通过对象内置函数进行设置控件功能等

```java
package win1;

import java.awt.*;

/**
 * @author Mac
 * @Project Name: WinForm
 * @Package Name: win1
 * Created by MacBook Air on 2020/02/05.
 * Copyright © 2020 KawYang. All rights reserved.
 */
public class MyFrame {
    public static void main(String[] args) {
        //窗口标题 Hello world
        Frame fr = new Frame("Hello World");
        fr.setSize(500,500);
        fr.setBackground(Color.cyan);
        Panel pa = new Panel();
        pa.setSize(530,630);
        pa.setBackground(Color.GRAY );
        fr.add(pa);
        fr.setVisible(true);
    }
}
```

效果图：  

![Form_2](https://gitee.com/KawYang/Notes/raw/master/Image/Java/Form_2.png)

---

### $\color{#188}{Button创建}$

```java
public class MyButton {
    public static void main(String[] args) {
        Frame fr = new Frame("MyButton");
        fr.setLayout(new FlowLayout());
        Button button1 = new Button("OK");
        Button button2 = new Button("OPEN");
        Button button3 = new Button("CLOSE");
        button1.setEnabled(true);
        button2.setEnabled(false);
        fr.add(button1);
        fr.add(button2);
        fr.add(button3);
        fr.setSize(300,300);
        fr.setVisible(true);
    }
}
```

效果图：

![From_3](https://gitee.com/KawYang/Notes/raw/master/Image/Java/Form_3.png)

### $\color{#189}{登录页面}$

```java
public class Login {
    public static void main(String[] args) {
        JFrame fr = new JFrame("Login");
        fr.setSize(400,100);
        fr.setBackground(Color.cyan);
        //设置窗体在桌面上的位置
        fr.setLocation(300,300);
        //容器
        Container fr_container = fr.getContentPane();
        //设置布局
        fr_container.setLayout(new FlowLayout());
        fr_container.add(new JLabel("User"));
        fr_container.add(new JTextField("user1",10));
        fr_container.add(new JLabel("Passed"));
        fr_container.add(new JPasswordField("passed",10));
        fr_container.add(new JButton("OK"));
        fr_container.add(new JButton("Cancel"));
        fr.setVisible(true);
    }
}

```

### $\color{#189}{GUI事件}$

当用户执行某个动作时，对该动作说做的反应  
动作触发事件的发生

```java
    //获取执行程序的当前路径
    String file = System.getProperty("user.dir");
    // file = /Users/mac/MyCodes/IDEAProjects/JavaTest
    ImageIcon icon = new ImagIcon(file+"/01.jpg");
    //设置照片
    jLabel1.setIcon(icon);
```

#### 委托模型

> * 事件源对象：产生事件的组件对象，如按钮
> * 事件对象：描述事件发生时状态信息，如点击鼠标
> * 事件监听器：提供事件处理对象

Java虚拟机对事件不作处理，先对监听进行注册，当发生某个事件时，在注册中谁感兴趣，对该事件进行处理。事件处理机制处理。  

### 事件源对象

多个控件共同使用同一段代码，需要获取触发事件的空间信息  $\color{red}{ActionEvent}$  
方法： getSource() 获取事件对象

```java
    JRadioButton jr = (JRadioButton) evt.getSource()
    if (jr == jRadioButton1){
        ...
    }
    if(evt.getSource() == jRadioButton1){
        ...
    }
```
 
$\color{red}{IDEA创建监听器}$

点击控件-> Creat Listener
| 编号  |      事件类      |    事件监听接口     | 描述                         |
| :---: | :--------------: | :-----------------: | :--------------------------- |
|   1   |   ActionEvent    |   ActionListener    | 此接口用于接收动作事件。     |
|   2   |  ComponentEvent  |  ComponentListener  | 此接口用于接收组件事件。     |
|   3   |    ItemEvent     |    ItemListener     | 此接口用于接收项目事件。     |
|   4   |     KeyEvent     |     KeyListener     | 该接口用于接收按键事件。     |
|   5   |    MouseEvent    |    MouseListener    | 该接口用于接收鼠标事件。     |
|   6   |   WindowEvent    |   WindowListener    | 该接口用于接收窗口事件。     |
|   7   | AdjustmentEvent  | AdjustmentListener  | 该接口用于接收调整事件。     |
|   8   |  ContainerEvent  |  ContainerListener  | 此接口用于接收容器事件。     |
|   9   | MouseMotionEvent | MouseMotionListener | 该接口用于接收鼠标运动事件。 |
|  10   |    FocusEvent    |    FocusListener    | 该接口用于接收焦点事件。     |

[参考内容](https://www.yiibai.com/swing/swing_event_listeners.html)

ActionListener 最常用的事件（如按钮->单击）

```java
/**
 *事件监听器类
 *该类需要实现ActionListener接口的方法（资格）
 */
class ButtonHandler implements ActionListener{
    
    @Override
    public void actionPerformed(ActionEvent e){
        System.out.println("点击");

    }
    
}

/**
 * @author Mac
 */
public class ButtonTest {
    public static void main(String[] args) {
        JFrame fr = new JFrame("Button");
        JButton button = new JButton("点击");
        button.setBackground(Color.cyan);
        //创建事件委托（注册）
        button.addActionListener(new ButtonHandler());
        button.setSize(20,50);
        button.setText("登录");
        fr.add(button);
        fr.setSize(300,300);
        fr.setVisible(true);
    }
}
```

![Event_2](https://gitee.com/KawYang/Notes/raw/master/Image/Java/Event_2.png)


### 事件适配器

Adapter类
通过适配器添加控件的事件
例：
```java
class WindowClose extends windowAdapter {
    public void windowClosing(WindowEvent e){
        Systeam.exit(0);
    }
}
public static void main(String []args){
    Frame fr = new Frame("Login");
    fr.addwindowListener(new WindowClose());
    fr.setSize(300,300);
    fr.setVisible(true);
}
```
如果使用监听器，需要实现windowLisenter 类内的全部方法  
如果使用适配器，需要继承windowAdapter 类，实现相应的一个方法。  
适配器内方法全部实现，但是都没有内容{}







### 使用多个窗体

普通窗体和对话框  

对话框：如果不操作会掩盖下边的窗体  
关闭： Exit（系统关闭）、Dispose（关闭当前窗体）、Hide（隐藏当前窗体） 属性：DefaultCloseOperation

菜单：

|    名     | 功能   |
| :-------: | :----- |
| JMenuBar  | 菜单条 |
|   JMenu   | 菜单   |
| JMenuItem | 菜单项 |

通用对话框

|      名       | 功能                                 |
| :-----------: | :----------------------------------- |
| JFileChooser  | 文件选择对话框                       |
|  JOptionPane  | 消息对话框   (例如是否退出？YES，NO) |
| JColorChooser | 颜色选择对话框                       |

### 组件布局（布局管理器管理）

跨平台 窗口大小不确定

控件大小随着窗口的大小调整而改变

```java
    Frame f = new Frame();
    f.setLayout(new FlowLayout());
```

#### FlowLayout

类似文字可以折行  

是Panel的缺省布局管理器（Panel里不设置，用的是FlowLayOut）

#### BorderLayout

上中下左右，变化大小窗口，中间变化最大，边上不变  
是window ，Frame和Dialog缺省的布局管理器

#### GridLayout

调整大小是，均匀分格的大小，均匀变化（“田”）  
使组件呈网格状布局。

#### CardLagout

开片式布局  
用事件进行处理  

> - 能够用实现两个或更多的成员共享同一个空间
> - 共享空间的成员之间的关系就像一叠卡片一样
> - 在一张客片中只能显示一个组件或者一个容器（嵌套多个组件)
>

#### 无布局管理

> - setLayout(null) :布局管理方式为空
> - setLocation(),setSize(),setBounds(): 动态设置大小
> - 如果用户不管理，控件显示效果与平台有关。

#### 复杂的布局

### $\color {#199}{控件}$

|         名          |                         功能                          |
| :-----------------: | :---------------------------------------------------: |
|    JRadioButton     |                        单选钮                         |
|     ButtonGroup     |                        按钮组                         |
|      JCheckBox      |                        复选框                         |
| text、selected 属性 | 设置内容和选定   $\color{red}{isselected()}$       ｜ |
|    Color、Font类    |  设置字体颜色和大小$\color{red}{import\ java.awt.*}$  |


### 例子

```java
package form;

import javax.swing.*;
import java.awt.*;

/**
 * @author LiYang
 * @Project Name: WinForm
 * @Package Name: form
 * Created by MacBook Air on 2020/02/09.
 * Copyright © 2020 LiYang. All rights reserved.
 */
public class login {
    private JPanel test;
    private JButton 登录Button;
    private JButton 取消Button;
    private JTextField textField1;
    private JPasswordField passwordField1;


    public login() {
        登录Button.addActionListener(e -> {
            String name = textField1.getText();
            System.out.println(name);
            String key = String.valueOf(passwordField1.getPassword());
            System.out.println(key);
        });
        取消Button.addActionListener(e -> System.exit(0));
    }

    public static void main(String[] args) {
        JFrame frame = new JFrame("login");
        frame.setContentPane(new login().test);
        frame.setLocation(500, 200);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.pack();
        frame.setVisible(true);
    }

    {
// GUI initializer generated by IntelliJ IDEA GUI Designer
// >>> IMPORTANT!! <<<
// DO NOT EDIT OR ADD ANY CODE HERE!
        $$$setupUI$$$();
    }

    /**
     * Method generated by IntelliJ IDEA GUI Designer
     * >>> IMPORTANT!! <<<
     * DO NOT edit this method OR call it in your code!
     *
     * @noinspection ALL
     */
    private void $$$setupUI$$$() {
        test = new JPanel();
        test.setLayout(new GridBagLayout());
        final JPanel spacer1 = new JPanel();
        GridBagConstraints gbc;
        gbc = new GridBagConstraints();
        gbc.gridx = 1;
        gbc.gridy = 3;
        gbc.fill = GridBagConstraints.VERTICAL;
        test.add(spacer1, gbc);
        final JPanel panel1 = new JPanel();
        panel1.setLayout(new GridBagLayout());
        gbc = new GridBagConstraints();
        gbc.gridx = 1;
        gbc.gridy = 2;
        gbc.fill = GridBagConstraints.BOTH;
        test.add(panel1, gbc);
        final JPanel spacer2 = new JPanel();
        gbc = new GridBagConstraints();
        gbc.gridx = 1;
        gbc.gridy = 1;
        gbc.fill = GridBagConstraints.VERTICAL;
        panel1.add(spacer2, gbc);
        final JPanel spacer3 = new JPanel();
        gbc = new GridBagConstraints();
        gbc.gridx = 1;
        gbc.gridy = 0;
        gbc.fill = GridBagConstraints.VERTICAL;
        panel1.add(spacer3, gbc);
        final JLabel label1 = new JLabel();
        Font label1Font = this.$$$getFont$$$(null, -1, 18, label1.getFont());
        if (label1Font != null) label1.setFont(label1Font);
        label1.setText("用户名：");
        gbc = new GridBagConstraints();
        gbc.gridx = 0;
        gbc.gridy = 0;
        gbc.anchor = GridBagConstraints.WEST;
        panel1.add(label1, gbc);
        final JLabel label2 = new JLabel();
        Font label2Font = this.$$$getFont$$$(null, -1, 18, label2.getFont());
        if (label2Font != null) label2.setFont(label2Font);
        label2.setText("密  码：");
        gbc = new GridBagConstraints();
        gbc.gridx = 0;
        gbc.gridy = 1;
        gbc.anchor = GridBagConstraints.WEST;
        panel1.add(label2, gbc);
        passwordField1 = new JPasswordField();
        passwordField1.setColumns(8);
        gbc = new GridBagConstraints();
        gbc.gridx = 2;
        gbc.gridy = 1;
        gbc.anchor = GridBagConstraints.WEST;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        panel1.add(passwordField1, gbc);
        textField1 = new JTextField();
        textField1.setColumns(8);
        gbc = new GridBagConstraints();
        gbc.gridx = 2;
        gbc.gridy = 0;
        gbc.anchor = GridBagConstraints.WEST;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        panel1.add(textField1, gbc);
        final JPanel spacer4 = new JPanel();
        gbc = new GridBagConstraints();
        gbc.gridx = 1;
        gbc.gridy = 1;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        test.add(spacer4, gbc);
        final JPanel panel2 = new JPanel();
        panel2.setLayout(new GridBagLayout());
        gbc = new GridBagConstraints();
        gbc.gridx = 1;
        gbc.gridy = 4;
        gbc.fill = GridBagConstraints.BOTH;
        test.add(panel2, gbc);
        登录Button = new JButton();
        登录Button.setText("登录");
        gbc = new GridBagConstraints();
        gbc.gridx = 0;
        gbc.gridy = 0;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        panel2.add(登录Button, gbc);
        final JPanel spacer5 = new JPanel();
        gbc = new GridBagConstraints();
        gbc.gridx = 1;
        gbc.gridy = 0;
        gbc.fill = GridBagConstraints.VERTICAL;
        panel2.add(spacer5, gbc);
        取消Button = new JButton();
        取消Button.setText("取消");
        gbc = new GridBagConstraints();
        gbc.gridx = 2;
        gbc.gridy = 0;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        panel2.add(取消Button, gbc);
        final JPanel spacer6 = new JPanel();
        gbc = new GridBagConstraints();
        gbc.gridx = 2;
        gbc.gridy = 2;
        gbc.weightx = 1.0;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        test.add(spacer6, gbc);
        final JPanel spacer7 = new JPanel();
        gbc = new GridBagConstraints();
        gbc.gridx = 0;
        gbc.gridy = 2;
        gbc.weightx = 1.0;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        test.add(spacer7, gbc);
        final JLabel label3 = new JLabel();
        Font label3Font = this.$$$getFont$$$("Courier", Font.BOLD, 55, label3.getFont());
        if (label3Font != null) label3.setFont(label3Font);
        label3.setText("Hello World");
        gbc = new GridBagConstraints();
        gbc.gridx = 1;
        gbc.gridy = 0;
        gbc.anchor = GridBagConstraints.WEST;
        test.add(label3, gbc);
        final JPanel spacer8 = new JPanel();
        gbc = new GridBagConstraints();
        gbc.gridx = 1;
        gbc.gridy = 5;
        gbc.fill = GridBagConstraints.VERTICAL;
        test.add(spacer8, gbc);
    }

    /**
     * @noinspection ALL
     */
    private Font $$$getFont$$$(String fontName, int style, int size, Font currentFont) {
        if (currentFont == null) return null;
        String resultName;
        if (fontName == null) {
            resultName = currentFont.getName();
        } else {
            Font testFont = new Font(fontName, Font.PLAIN, 10);
            if (testFont.canDisplay('a') && testFont.canDisplay('1')) {
                resultName = fontName;
            } else {
                resultName = currentFont.getName();
            }
        }
        return new Font(resultName, style >= 0 ? style : currentFont.getStyle(), size >= 0 ? size : currentFont.getSize());
    }

    /**
     * @noinspection ALL
     */
    public JComponent $$$getRootComponent$$$() {
        return test;
    }

}
```
如图：

![Form_1](https://gitee.com/KawYang/Notes/raw/master/Image/Java/Form_4.png)


## 异常及其分类

软件的容错性

### 错误和异常

> 错误：运行过程中，硬件或操作系统发生的问题，如虚拟机崩溃
> 异常：硬件和操作系统正常，运行时发生错误。如除0

异常分类：
运行时异常
其他异常

常用异常类-运行时异常
|               名               |                                    |
| :----------------------------: | :--------------------------------- |
|      ArithmeticException       | 一个不寻常算术运算产生的异常。     |
| ArrayIndexOutOfBoundsException | 数组索引超出范围所产生的异常。     |
|       ClassCastExcption        | 类对象强迫转换不当所产生的异常。   |
|      NullPointerException      | 对象引用参考值为null所产生的异常。 |

常用异常类-必须处理的异常
|           名           |                                                    |
| :--------------------: | :------------------------------------------------- |
| ClassNotFoundException | 找不到类或接口所产生的异常。                       |
|  InterruptedException  | 目前线程等待执行另一线程中断目前线程所产生的异常。 |
|      IOException       | 输入输出访问异常。                                 |

### 自定义异常

创建Exception 的子类就是创建了一个新的异常  
找离异常信息最接近的父类进行继承，许多相似方法都被继承
class 自定义异常 extends 父异常类名{
    类体;
}

抛出异常：

```java
    /**
     * @param userName 
     * @return user
     * @throws TooManyTimesWrongLogin
     */
    public static User check (String userName) throws TooManyTimesWrongLogin {
        String password;
        Scanner reader=new Scanner(System. in);
        for(int i=0;i<3;i++) {
            System.out.print1n("请输入密码，您还有" + (3 - i) + "次机会，输入Q或q表示取消登陆。");
            password = reader.next();
            if (userName.equals("admin") && password.equals(" 123456 ")){
             return new User(userName, true);
            }
            else if(password. equalsIgnoreCase("Q"))
                return new User (userName, false) ;
            throw new TooManyTimesWrongLogin (userName, "10.10.10.25");
        }
    }
```

## 多进程

进程是一个可并发执行的具有独立功能的应用程序，是操作系统进行资源分配和调度的基本单位。
进程又由线程组成，进程分配资源，线程共享进程资源，不单独申请。 

一、 继承Thread类实现多线程  
1. 定义一个线程类，继承Thread类，并重写run()方法
2. 创建该子类对象创建线程，用start运行
   
二、 实现Rnnnable接口实现多线程

1. 创建一个类实现Runnable接口，重写run()方法实现代码
2. 把Runnable对象作为参数传递给Thread类的一个构造方法，然后start运行   
   
三、通过 Callable 和 Future 创建线程。  
[参考](https://www.runoob.com/java/java-multithreading.html)

```java
package test;

/**
 * @author LiYang
 * @Project Name: JavaTest
 * @Package Name: test
 * Created by MacBook Air on 2020/02/13.
 * Copyright © 2020 LiYang. All rights reserved.
 */
public class ThreadTest {
    public static void main(String[] args) {
        MyThread myThread1 = new MyThread();
        myThread1.start();
        Thread thread = new Thread(new MyRunnable());
        thread.start();

    }
}

//一、 通过继承Thread类，创建MyThread对象实现进程
class MyThread extends Thread{
    public void run(){
        for(int i = 0;i<10;i++){
            System.out.println("MyThread Run!"+i);
            try {
                sleep(100);
            } catch (InterruptedException e) {
                System.out.println(e);
            }
        }
    }
}

//二、 通过实现Runnable接口实现多线程
class MyRunnable implements Runnable{
    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("MyRunnable Run!"+i);
            try {
                Thread.sleep(200);
            } catch (InterruptedException e) {
                System.out.println(e);
            }
        }
    }
}
```

运行结果：

```vim
MyThread Run!0
MyRunnable Run!0
MyThread Run!1
MyThread Run!2
MyRunnable Run!1
MyThread Run!3
MyThread Run!4
MyRunnable Run!2
MyThread Run!5
MyThread Run!6
MyRunnable Run!3
MyThread Run!7
MyRunnable Run!4
MyThread Run!8
MyThread Run!9
MyRunnable Run!5
MyRunnable Run!6
MyRunnable Run!7
MyRunnable Run!8
MyRunnable Run!9
```

### 线程的调度和控制

线程优先级：1-10级 数越大优先级越高；相同优先级，系统调度算法  
调度策略：抢占式调度策略

线程基本控制方法：
| 序号  |                   方法                    | 描述                                                                                                     |
| :---: | :---------------------------------------: | :------------------------------------------------------------------------------------------------------- |
|   1   |        public static void yield()         | 暂停当前正在执行的线程对象，并执行其他线程                                                               |
|   2   |  public static void sleep(long millisec)  | 在指定的毫秒数内让当前正在执行的线程休眠（暂停执行），此操作受到系统计时器和调度程序精度和准确性的影响。 |
|   3   | public static boolean holdsLock(Object x) | 当且仅当当前线程在指定的对象上保持监视器锁时，才返回 true。                                              |
|   4   |   public static Thread currentThread()    | 返回对当前正在执行的线程对象的引用。                                                                     |
|   5   |      public static void dumpStack()       | 将当前线程的堆栈跟踪打印至标准错误流。                                                                   |

### 线程变量

ThreadLocal 即线程变量
一个线程可以根据一个 ThreadLocal 对象查询到绑定在这个线程上的一个值。
可以通过 set(T)方法来设置一个值，在当前线程下再通过 get()方法获取到原先设置的值。

```java
/**
 * ThreadDemo1 采用ThreadLocal(线程变量)的方式创建integer变量
 * ThreadDemo2 采用类变量的方式创建integer变量
 */
public class ThreadLocalDemo {
    public static void main(String[] args) {
        test();
        System.out.println("===========");
        test2();
    }

    /**
     * 不同对象，创建两个线程
     * 测试结果:每个线程变量互不影响，都相对独立。
     * 因为是四个不同的ThreadDemo对象分别创建的线程，称不上是多线程。
     * 相等于创建了四个不同的类对象
     */
    public static void test(){
        new Thread(new ThreadDemo1()).start();
        new Thread(new ThreadDemo1()).start();
        System.out.println("1----------");
        new Thread(new ThreadDemo2()).start();
        new Thread(new ThreadDemo2()).start();
    }


    /**
     * 同一个对象，创建两个线程。
     * ThreadDemo1 采用ThreadLocal变量，两个线程互不影响，变量相对独立
     * ThreadDemo2 采用类变量方式，对于同一个Thread对象，两个线程之间变量相互影响
     * 同一个对象，共享资源，在多线程中容易发生错误。
     */
    public static void test2(){
        ThreadDemo1 threadDemo1 = new ThreadDemo1();
        new Thread(threadDemo1).start();
        new Thread(threadDemo1).start();
        System.out.println("2-----------");
        ThreadDemo2 threadDemo2 = new ThreadDemo2();
        new Thread(threadDemo2).start();
        new Thread(threadDemo2).start();
    }
}

class ThreadDemo1 implements Runnable{
    /**使用ThreadLocal提供的静态方法创建一个线程变量 并且初始化值为0*/
    private static ThreadLocal<Integer> threadLocal = ThreadLocal.withInitial(() -> 0);

    @Override
    public void run(){
        for (int i = 0; i < 10; i++) {
            //get方法获取线程变量值
            Integer integer = threadLocal.get();
            integer += 1;
            //set方法设置线程变量值
            threadLocal.set(integer);
            System.out.println(integer);
        }
    }
}

class ThreadDemo2 implements Runnable{
    private Integer integer = 0;

    @Override
    public void run() {
        for (int i = 0; i < 10; i++) {
            System.out.println("Thread2 "+integer++);
        }
    }
}
```

耐人寻味的结果：
```vim 
1
2
3
4
5
6
7
8
9
10
1
2
3
4
5
6
7
8
9
10
1----------
===========
Thread2 0
Thread2 1
Thread2 2
Thread2 3
Thread2 4
Thread2 5
Thread2 6
Thread2 7
Thread2 8
Thread2 9
1
2
3
1
4
2
3
5
4
6
5
7
6
8
7
9
8
9
10
10
2-----------
Thread2 0
Thread2 1
Thread2 2
Thread2 3
Thread2 4
Thread2 5
Thread2 6
Thread2 7
Thread2 8
Thread2 9
Thread2 0
Thread2 1
Thread2 2
Thread2 3
Thread2 4
Thread2 5
Thread2 6
Thread2 7
Thread2 8
Thread2 9
Thread2 10
Thread2 11
Thread2 12
Thread2 13
Thread2 14
Thread2 15
Thread2 16
Thread2 17
Thread2 18
Thread2 19
```

```vim
1----------
1
2
3
4
5
6
7
8
9
10
1
2
3
4
5
6
7
8
9
10
Thread2 0
Thread2 1
Thread2 2
Thread2 3
Thread2 4
Thread2 5
Thread2 6
Thread2 7
Thread2 8
Thread2 9
===========
Thread2 0
Thread2 1
Thread2 2
Thread2 3
Thread2 4
Thread2 5
Thread2 6
Thread2 7
Thread2 8
Thread2 9
2-----------
1
2
3
4
5
6
7
8
9
10
1
2
3
4
5
6
7
8
9
10
Thread2 0
Thread2 1
Thread2 2
Thread2 3
Thread2 4
Thread2 5
Thread2 6
Thread2 7
Thread2 8
Thread2 9
Thread2 10
Thread2 11
Thread2 12
Thread2 13
Thread2 14
Thread2 15
Thread2 16
Thread2 17
Thread2 18
Thread2 19
```

### 线程同步

    当多个线程操作同一个对象时，就会出现线程安全问题，被多个线程同时操作的对象数据可能会发生错误。线程同步可以保证在同一个时刻该对象只被一个线程访问。

#### Synchronized

    关键字 synchronized 可以修饰方法或者以同步块的形式来进行使用，它确保多个线程在同一个时刻，只能有一个线程处于方法或者同步块中，保证了线程对变量访问的可见性和排他性。它有三种使用方法：

> * 对普通方式使用，将会锁住当前实例对象  
> * 对静态方法使用，将会锁住当前类的 Class 对象  
> * 对代码块使用，将会锁住代码块中的对象

三种加锁方式：
```java
public class SynchronizedDemo {
    private static Object lock = new Object();

    public static void main(String[] args) {
        //同步代码块 锁住lock
        synchronized (lock) {
            //doSomething
        }
    }

    //静态同步方法  锁住当前类class对象
    public synchronized static void staticMethod(){

    }
    //普通同步方法  锁住当前实例对象
    public synchronized void memberMethod() {

    }
}
```

    java.util.concurrent 包,提供了多种在并发编程中的适用工具类。包括原子操作类，线程池，阻塞队列，Fork/Join 框架，并发集合，线程同步锁等。
    JUC 中的 ReentrantLock 是多线程编程中常用的加锁方式，ReentrantLock 加锁比 synchronized 加锁更加的灵活，提供了更加丰富的功能。

```java
import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.ReentrantLock;

/**
 * @author 实验楼11
 * @Project Name: 实验楼
 * @Package Name: PACKAGE_NAME
 * Created by MacBook Air on 2020/02/16.
 * Copyright © 2020 LiYang. All rights reserved.
 */
public class ThreadTestPro {
    private static ReentrantLock lock = new ReentrantLock();
    private static int count = 0;
    private static Condition condition = lock.newCondition();

    public static void main(String[] args) {
        Thread A = new Thread(() -> {
            //加锁 一次只有一个线程输出
            lock.lock();
            try {
                while (true) {
                    //因为只循环3次 所以到9的时候就结束循环
                    if (count == 9) {
                        break;
                    }
                    //当余数为0 就输出A
                    if (count % 3 == 0) {
                        count++;
                        System.out.println("A");
                        //唤醒其他等待线程
                        condition.signalAll();
                    } else {
                        try {
                            //等待
                            condition.await();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                }
            } finally {
                lock.unlock();
            }
        });
        Thread B = new Thread(() -> {
            lock.lock();
            try {
                while (true) {
                    if (count == 9) {
                        break;
                    }
                    if (count % 3 == 1) {
                        count++;
                        System.out.println("B");
                        condition.signalAll();
                    } else {
                        try {
                            condition.await();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                }
            } finally {
                lock.unlock();
            }
        });
        Thread C = new Thread(() -> {
            lock.lock();
            try {
                while (true) {
                    if (count == 9) {
                        break;
                    }
                    if (count % 3 == 2) {
                        count++;
                        System.out.println("C");
                        condition.signalAll();
                    } else {
                        try {
                            condition.await();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                }
            } finally {
                lock.unlock();
            }
        });

        A.start();
        B.start();
        C.start();

    }
}
```

```vim
A
B
C
A
B
C
A
B
C
```


