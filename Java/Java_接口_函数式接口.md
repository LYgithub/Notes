
<!-- TOC -->

- [类的继承](#类的继承)
    - [继承的特点](#继承的特点)
- [抽象类 (abstract)](#抽象类-abstract)
    - [格式](#格式)
    - [注意](#注意)
    - [发红包案例](#发红包案例)
        - [分析](#分析)
- [接口(interface)](#接口interface)
    - [默认方法](#默认方法)
    - [静态方法](#静态方法)
    - [私有方法](#私有方法)
    - [常量](#常量)
    - [小结](#小结)
    - [注意](#注意)
- [函数式接口](#函数式接口)
    - [使用](#使用)
        - [参数](#参数)
- [函数式编程](#函数式编程)
    - [Lambda 的延迟执行](#lambda-的延迟执行)
        - [返回值](#返回值)
- [常用函数式接口](#常用函数式接口)
    - [Supplier 接口](#supplier-接口)
    - [Consumer 接口](#consumer-接口)
    - [Predicate 接口](#predicate-接口)
    - [Function 接口](#function-接口)
    - [综合案例](#综合案例)
    - [总结](#总结)

<!-- /TOC -->


## 类的继承

- [P164](https://www.bilibili.com/video/av55246614?p=164)

### 继承的特点

**单继承**
    
    class A{}
    class B extends A{}  🙆‍♂️
    class C extends A,B{} 🙅‍♂️

**多级继承**

- Java.long.Object
    
    class A{}  
    class B extends A {}  🙆‍♂️  
    class C extends B {}  🙆‍♂️  

**多子类**

## 抽象类 (abstract)

- [P165](https://www.bilibili.com/video/av55246614?p=165)

    - 子类就是一个父类，所以是继承关系。
    - 子类中共有的方法，但是所有子类都不一样

### 格式

    含有抽象方法的类，必须是抽象类

```java
    public abstract class Animal{
        //抽象方法定义
        public abstract void eat();
        //普通方法定义
        public void move (){

        }
    }
```

 - 不能直接使用**new**关键字
 - 必须用子类继承抽象父类
 - 子类必须实现父类中所有的抽象方法
 - 创建子类对象进行使用


```java 

public class Cat extends Animal{
    @Override
    public void eat(){
        sout("猫吃鱼！");
    }
}

Cat cat = new Cat;
cat.eat();

```

### 注意

- 抽象类**不能创建对象**
- 抽象类中，可以有构造函数，是供子类创建对象时，初始化父类成员使用的。
  - 如果构造函数是抽象的，则子类中用 supper()调用
  - 先创建父类
  - 后创建子类
- 抽象类不一定有抽象方法，没有抽象方法的抽象类，也不能直接创建对象
- 抽象类的子类，必须实现父类**所有**的抽象方法，否则依然是一个抽象类


### 发红包案例

#### 分析

    红包分为普通红包和运气红包

1. 群主有钱
2. 成员收红包，余额增加

- 类： 群主、普通成员、用户类  
- 共性：姓名、余额  
- 独有：  
  - 群主： 发红包
  - 成员： 收红包
- 发红包
  - 返回值类型： ArrayList<Integer>
  - 方法名称： send
  - 参数列表：
    - 总金额： int totalMoney
    - 分数： int count
```java
public ArrayList <Integer> send (int totalMoney,int count){
    ...
}
```
- 收红包
  - 返回值类型：void
  - 方法名：receive
  - 参数列表：ArrayList<Integer>

```java
public void receive (ArrayList <Integer> list){
    ...
}
```

## 接口(interface)

接口就是一个 **公共的规范接口**  
符合标准 -> 通用  
关键字 interface -> **.class 文件**

- 包含的内容
  - 常量
  - 抽象方法
  - 默认方法 JDK8
  - 静态方法 JDK8
  - 私有方法 JDK9

**接口是引用类型**

public interface 接口名称{
    //接口内容
}

- 定义
- 注意：
  - 接口不能直接使用，必须使用一个实现类来实现接口
    ```java
    public class 实现类名 implements 接口名称{

    }
    ```
  - 实现类**必须**重写 接口中所有的抽象类
  - 创建实现类使用接口
  - 如果有抽象方法没有重写，那么该类就是一个**抽象类**


### 默认方法

- 从JDK8 允许默认方法
    
- 可以解决接口升级问题
  - 如果接口添加抽象方法，就会导致所有子类全部实现
  - 使用default 方法，在**接口中实现方法体**
- 使用

```java
    public default 返回值 方法名称(方法参数){
        //可以有方法体
        //public 可以省略
    }
```

- 默认方法会被实现类所**继承** 
- 也可被实现类**重写**

### 静态方法

static ：共享方法

```java
    public static void test(){
        //带有方法体
    }
```
- 接口名称可以直接 **.** 调用
- **不能通过实现类调用静态方法** 
  - 实现多个接口，静态方法可能发生冲突
  - 不需要创建实现类对象

### 私有方法

    一种安全机制

- 普通
  - 多个**默认**方法之间重复代码问题

```java
private void test(){

}
```

- 静态
  - 多个**静态**方法之间重复代码问题

```java
private static void test(){

}
```

### 常量

接口中够可以定义成员"变量" **public static final** (省略依旧)  
不可修改

public static final int x = 1;

共有、接口名称 **.** 访问

- 常量必须赋值
- 完全大写
- 下划线连接单词

[接口小结](https://www.bilibili.com/video/av55246614?p=182)

### 小结

- 在Java 9+ 版本中，接口的内容有：

1. 成员变量其实是称量，格式：
    - [public] [static] [final] 数据类型 常量名 = 数据值;
    - 注意：
      - 常量必须进行赋值，且不可改变
      - 常量名完全大写，用下划线分割
2. 接口中最重要的是抽象方法，格式：
    - [public] [abstract] 返回值类型 方法名称 (参数列表);
    - 注意:
      - 实现类必须实现所有的抽象方法
3. 从Java8 开始 ,允许定义默认方法，格式：	
    - [public] default 返回值类型 方法名称(参数列表){ 方法体 }
    - 注意:
      - 默认方法也可以被覆盖重写
4. 从Java8 开始, 允许定义静态方法，格式:
   - [public] static 返回值类型 方法名称(参数列表) { 方法体 }
   - 注意：
     - 通过接口名称直接调用，不能通过实现类进行调用
5. 从Java9 开始, 允许定义私有方法,格式：
   - 普通私有方法：private 返回值类型 方法名称(参数列表){ 方法体 }
   - 静态私有方法：private static 返回值类型 方法名称(参数列表){ 方法体  }
   - 注意:
     - private 的方法只能在接口内调用，不能被实现类和别人使用。

### 注意

    接口不能有静态代码块和构造方法 抽象类有构造方法
    一个类的直接父类只有一个，但是可以实现多个接口
        public class MyInterfaceImpl implements MyInterfaceA,MyInterfaceB{}
    两个抽象方法重名，只需覆盖重写一次即可
    重名的默认方法，实现类一定对重复的覆盖重写    
    一个类如果直接父类中的方法，和接口中的方法发生冲突，直接使用父类的方法
    继承 优先于 接口实现

- 类与类是单继承的
- 类与接口是多实现的
- 接口与接口之间是多继承的
  - 多个父接口当中的抽象方法冲突可以
  - 多个父接口当中的默认方法冲突，那么子接口必须进行默认方法覆盖，【必须带着 default 关键字】

- [P184 结束](https://www.bilibili.com/video/av55246614?p=184)

---

## 函数式接口

- [P410 开始](https://www.bilibili.com/video/av55246614?p=410)

    有且只有一个抽象方法的接口，称之为函数式接口
    可以包含其他的方法（默认方法、静态方法、私有方法）
    函数式编程 Lambda

```java
/**
    @FunctionalInterface    
    可以监测是否是一个函数式接口
 */
@FunctionalInterface
public interface MyFocationInterface{
}
    public abstract void method();
```

### 使用

	一般可以作为参数和返回值来使用

#### 参数

```java
	//定义一个方法，参数使用函数式接口 
	public static void test (MyFunctionInterface myInter){
		myInter.method();
	}

	main(){
		//调用 show 方法，参数使用函数式接口的实现类对象 
		show (new MyFunctionInterfaceImpl());
		//调用show方法 ，参数使用 匿名内部类
		show(new MyFunctionInterface(){
			@Override
			public void method(){
				sout("使用匿名内部类重写接口中的抽象方法！");
			}
		});
		//调用show方法 ，参数使用 Lambda 表达式
		show(()-> sout("Lambda实现接口的抽象方法！"));

	}
```

    匿名内部类生成 .class 文件
    Lambda表达式不会生成 .class 文件

## 函数式编程

### Lambda 的延迟执行

日志可以快速定位问题

```java
package Demo4.Lambda;

/*
    日志案例

    性能浪费的问题：
        调用  showLog 传递的第二个参数是一个拼接后的字符串
        先拼接 后调用方法
        showLog 如果等级不是 1 级，不会输出，字符串白 拼接了，浪费

     使用Lambda 特性进行 优化
     使用前提：必须存在函数式接口
        延迟加载
*/

public class Demo01Logger {
    //定义一个根据日志等级，显示日志信息
    public static void showLog(int level,String message) {
        if(level == 1){
            System.out.println(message);
        }
    }


    public static void main(String[] args) {
        //定义三个日志信息

        String msg1 = "Hello";
        String msg2 = "World";
        String msg3 = "Java";

        //调用showLog 方法，传递参数
		showLog(1,msg1+msg2+msg3);
		//========================

		//Lambda 优化
		showLog2(1,()->msg1+msg2+msg3);


	}
	
	//传递等级 和 接口
	public static void showLog2(int level ,MessageBuilder builder){
		if(level == 1){
			System.out.println(builder.builderMessage());
		}
	}
}

@FunctionalInterface
public interface MessageBuilder {
    public abstract String builderMessage();
}



```

	使用 Lambda 表达式 作为参数传递，仅仅把参数传递到showLog 中
	只有满足条件，日志的等级为1 
		才会调用接口 MessageBuilder 中的方法 BuilderMessage
		才会进行字符串的拼接
	如果条件不满足 level != 1
		MessageBuilder 中的方法不会调用
		资源不会浪费


**Runable** 是一个 函数式接口

```java
public class RunnableLambda {
    public static void threadRun (Runnable run){
        new Thread(run).start();
    }
    public static void main(String[] args) {
        //匿名内部类
        threadRun(new Runnable() {
            @Override
            public void run() {
                System.out.println(Thread.currentThread().getName() +"--> 线程启动！");
            }
        });

        //Lambda 表达式
        threadRun(()-> System.out.println(Thread.currentThread().getName() +"--> 线程启动!"));

        new Thread(()->System.out.println(Thread.currentThread().getName() +"--> 线程启动!")).start();
    }
}
```		

#### 返回值

Comparator 也是一个 函数式借口

```java
package Demo4.Lambda;

import java.util.Arrays;
import java.util.Comparator;

public class Demo03Comparator {
    public static Comparator<String> getComparator(){
        //方法的返回值是一个接口，那么我们可以返回一个匿名内部类

//        return new Comparator<String>() {
//            @Override
//            public int compare(String o1, String o2) {
//                return o2.length()-o1.length();
//            }
//        };
        return (o1, o2) -> o2.length()-o1.length();


    }

    public static void main(String[] args) {
        String [] arr = {
                "liuxin",
                "BBBB",
                "ccdsaffda"
        };
        System.out.println(Arrays.toString(arr));

        Arrays.sort(arr,getComparator());
        Arrays.sort(arr,getComparator());

        System.out.println(Arrays.toString(arr));
    }
}
```

---

## 常用函数式接口

- java.util.funtion

### Supplier 接口

Supplier <T> 接口被称之为**生成型接口**，指定接口的泛型是什么类型  
那么接口中的 get 方法 就会生成什么类型的数据

```java
public class DemoSupplier {
    public  static String getString(Supplier<String> sup){
        return sup.get();
    }

    public static void main(String[] args) {

        System.out.println(getString(() -> "test"));
    }
}
```

```java
public static int getMax (Supplier<Integer> max){
        return max.get();
    }

    public static void main(String[] args) {

        int []arr = {
                1,2,3,4,50,6,7,8,-5,9
        };

        System.out.println(getMax(()->{
            //求数组元素最大值
            int max = arr[0];
            for (int i : arr) {
                if(i > max){
                    max = i;
                }
            }
            return max;
        }));
	}
```


### Consumer 接口

	是一个消费型接口，accept 消费指定泛型的数据
	自定义消费方法，如 输出、计算。

```java
public class DemoConsumer  {
    public static void print(String name ,Consumer<String >  consumer){
        consumer.accept(name);
    }

    public static void main(String[] args) {
        print("张三",(o)-> System.out.println(o+",你好！"));

        print("张三", new Consumer<String>() {
            @Override
            public void accept(String s) {
                System.out.println(new StringBuffer(s).reverse().toString());
            }
        });

        print("李四",(String s) ->{
            String x =new  StringBuffer(s).reverse().toString();
            System.out.println(x);
        });
    }
}

```
- 方法 andThen 

需要两个 Consumer 接口，可以将两个 Consumer 接口组合到一起进行消费

	Consumer<String > con1;
    Consumer <String > con2;

    String s = "hello";
    con1.accept(s);
    con2.accept(s);

    con1.andThen(con2).accept(s);

```java
package Demo4.Interface;

import java.util.function.Consumer;

public class ConsumerTest1 {
    public static void main(String[] args) {
        String s = "Hello ";
        test(s,(o)-> System.out.println( o.toLowerCase()+"-> 1"),
                (o)-> System.out.println(o.toUpperCase()+"-> 2"));
        test2(s,(o)-> System.out.println( o.toLowerCase()+"-> 21"),
                (o)-> System.out.println(o.toUpperCase()+"-> 22"));
    }

    public static void test (String s,Consumer<String> con1,Consumer<String > con2){
        con1.accept(s);
        con2.accept(s);
    }

    public static void test2 (String s,Consumer<String> con1,Consumer<String > con2){
        // con1 在前 先消费
        con1.andThen(con2).accept(s);
        System.out.println("-----------");
        con2.andThen(con1).accept(s);
    }
}

```

### Predicate 接口

对某种数据类型进行判断

boolean test(T t)

```java
package Demo4.Interface;

import java.util.function.Predicate;

/*
    Predicate 对某种数据类型进行判断
    boolean test(T t)
    结果：
        符合条件返回 true
        不符合 返回 false

 */
public class DemoPredicate {
    public static void main(String[] args) {
        System.out.println(testPredicate("Hello", (o) -> o.equals("Hello")));
    }

    /**
     * 定义一个方法
     * 参数传递一个String 类型的字符串
     * 传递一个 Predicate 接口，泛型 String
     * 使用Predicate 中的test 方法对字符串进行判断，并把返回判断结果返回
     * @param s
     * @param pre
     */
    public static boolean testPredicate(String  s,Predicate<String> pre){
        return pre.test(s);
    }
}
```

- 方法 
	- and
	- or
	- negate

```java
package Demo4.Interface;

import java.util.function.Predicate;

/*
	需求：
	非（
        1. 字符串长度 大于 5
        2. 判断字符串是否 含有 i
        3. 或者是否以 St 开头   ）
    Predicate 接口中 有一个 and ，表示并且关系，也可以用于连接两个判断条件
 */
public class PredicateTest {
    public static boolean LengthAndIn(String s, Predicate<String> pre1 , Predicate<String > pre2, Predicate<String > pre3){
//        return  !(pre1.test(s) && pre2.test(s) || pre3.test(s))
        return pre1.and(pre2).or(pre3).negate().test(s);
    }


    public static void main(String[] args) {
        System.out.println(LengthAndIn("String",
                (o) -> o.length() > 5,
                (o) -> o.contains("w"),
                (o)->o.startsWith("St")
        ));
    }
}

```

### Function 接口

	转换类型接口，根据一个类型数据转换成另一个数据类型
	两个泛型参数
- apply 方法 
	- R apply(T t)

```java
/**
 * 字符串转换成 Integer 类型
 * Function 接口，<String ,Integer>
 */
public class DemoFunction {
    public static void change (String s, Function<String,Integer> fun){
        System.out.println(fun.apply(s));
    }

    public static void main(String[] args) {
        change("1",
                o-> Integer.parseInt(o));

        change("1",Integer::parseInt);
    }
}
```

- andThen 默认方法
	- 用来进行组合操作

```java
package Demo4.Interface;

import java.util.function.Function;

/*
    String "123" -> 123 -> +10 -> String

    fun1.apply("123") +10

    fun2.apply(133)
 */
public class andThenFunction {
    public static void main(String[] args) {
		System.out.println(change("123", o -> Integer.parseInt(o) + 10, 
				s -> String.valueOf(s)));
		System.out.println(change("123", o -> Integer.parseInt(o) + 10,
				String::valueOf));
    }

    public static String change (String s, Function<String ,Integer> fun1, Function<Integer,String> fun2){
        //先调用 fun1.apply(String) 后调用 fun2.apply(Integer)
        return fun1.andThen(fun2).apply(s);
    }

}
```


### 综合案例

```java
import java.util.function.Consumer;
import java.util.function.Function;
import java.util.function.Supplier;

/*
    函数模型的拼接

    String str= "赵丽颖,20"

    截取年龄 String -> Integer -> +100
 */
public class andThenFunctionTest {
    public static void main(String[] args) {
        String str= "赵丽颖,20";

        change(()->str.split(",")[1],
                Integer::parseInt,o-> System.out.println(o + 100)
                );
    }

    public static void change (Supplier<String> sup, Function<String,Integer> fun1, Consumer<Integer> con){
        con.accept(fun1.apply(sup.get()));
	}
	
}
```


### 总结

| 接口名称  | 作用       | 抽象方法 | 实现          |
| --------- | ---------- | -------- | ------------- |
| Supplier  | 生成型接口 | get      | Supplier <T>  |
| Consumer  | 消费型接口 | accept   | Consumer<T >  |
| Predicate | 判断型接口 | test     | Predicate<T>  |
| Function  | 转换型接口 | apply    | Function<T,Y> |

综合案例

[P427结束](https://www.bilibili.com/video/av55246614?p=427)

---

**Home + Esc 提示快捷键**


