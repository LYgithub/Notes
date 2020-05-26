# 技巧篇

## 一、三个数找出最大值

```java
    /**
     * 方法一、方法复杂，可拓展性低。
     * @param a
     * @param b
     * @param c
     * @return max
     */
    public static int max1(int a ,int b ,int c){
        if(a>b) {
            if (a > c) {
                return a;
            } else {
                return c;
            }
        }else{
            if(b > c){
                return b;
            }else {
                return c;
            }
        }
    }

    /**
     * 方法二、方法简单
     * @param a
     * @param b
     * @param c
     * @return  max
     */
    public static int max2(int a ,int b ,int c){
        if(a>b&& a>c){
            return a;
        }else if(b>c){
            return b;
        }else{
            return c;
        }
    }

    /**
     * 方法三、方法简单，可拓展性高
     * 运用选择排序的思想
     * @param a
     * @param b
     * @param c
     * @return max
     */

    public static int max3(int a ,int b ,int c){
        int max = a;
        if(max < b){
            max = b;
        }
        if(max < c){
            max = c;
        }
        return max;
    }
```

## 二、Java 的 contiune 的巧妙应用

```java
    /**
     * 计算1000 以内10个最大质数平均值
     */
    public static void number(){
        int sum =0,i = 0;
        outer:for(int j = 1000;j>2;j--){
            for(int x = 2;x<j/2;x++){
                if(j%x == 0){
                    continue outer;
                }
            }
            i++;
            sum += j;
            if(i<10){
                //1 - 9 9个数
                System.out.print(j + "+");
            }else{
                //第 10 个数
                System.out.println(j +"="+sum);
                break;
            }
        }
    }
```

## 三、最大公约数

### 辗转相除法

不需要m 大于 n
测试程序：

```java
public class String_1 {
    public static void main(String[] args) {
        System.out.println("开始测试...");
        test();

        System.out.println("finish");
    }
    /**
     *
     * @param m
     * @param n
     * @return
     */
    public static int gys(int m,int n){
        if(m<n){
            int temp = m;m = n; n = temp;
        }
        int t ;
        do{
            t = m%n;
            m = n;
            n = t;
        }while(t!=0);
        return m;
    }
    public static void test(){
        int i = 1000;
        for (int ix = 1; ix < i; ix++) {
            System.out.println(ix+"测试中。。。");
            for (int j = 1;j<i;j++){
                if(gys(ix,j) != gys(j,ix)){
                    System.out.println(ix+"与"+j+"的最大公约数为："+gys(ix,j));
                    System.out.println(j+"与"+ix+"的最大公约数为："+gys(ix,j));
                }

            }
        }
    }
}
```

---

辗转相除法：

```java
    public int gys(int m,int n){
        int t ;
        do{
            t = m%n;
            m = n;
            n = t;
        }while(t!=0);
        return m;
    }
```

1-999 之间两两相互取余 结果不相等的概率 99.9%
只有当 i 和 j 相等时，相互取余相等都为0

```java
public static void test(){
        int sum = 0;
        for(int i=1;i<1000;i++){
            for (int j= 1;j<1000;j++){
                if(i%j == j%i && i!=j){
                    System.out.println(i + "%" + j +"="+ (i%j));
                    System.out.println(j + "%" + i +"="+ (j%i));
                    System.out.println("---");
                    sum ++;
                }
            }
    }
        System.out.println(sum);
        String df  = new DecimalFormat("#.00").format(sum/(999*999.0)*100);
        System.out.println(df+ "%");
    }
```

## 四、转化成十六进制

```java
    public static String change(int a){
        StringBuffer b = new StringBuffer();
        int n;
        do{
            n = a%16;
            if(n< 10 ){
                b.insert(0,n);
            }
            else {
                b.insert(0,(char)(n-10+'A'));
            }
            a/=16;
        }while (a!=0);
        return b.toString();
    }
```

## 五、日期练习

输入将来的某一天，计算这一天是星期几
距离今天还有多少天

getTimeInMillis();

```java
    public static void main(String[] args) {
        int year,month,day;
        long time1,time2,betweenDays;
        Scanner reader = new Scanner(System.in);
        year = reader.nextInt();
        month = reader.nextInt();
        day = reader.nextInt();
        Calendar calendar = Calendar.getInstance();
        time1 = calendar.getTimeInMillis();
        calendar.set(year,month-1,day);
        time2 = calendar.getTimeInMillis();

        betweenDays = (time2-time1)/(1000*24*60*60);
        System.out.println("距离今天还有："+betweenDays+"天");
         System.out.println("星期："+DayWeek((calendar.get(Calendar.DAY_OF_WEEK)+6)%7));

    }
    public static String DayWeek(int n){

        switch (n){
            case 1: return "一";
            case 2:return  "二";
            case 3:return "三";
            case 4: return "四";
            case 5:return  "五";
            case 6:return "六";
            case 0:return "日";
        }
        return null;
    }
```

## 随机数

从52张扑克牌中抽取5张，要求不与之前的一样
 $\color{red}{采用绑定随机化}$的方法

> 分析：如果从52个整数中随机生成5个数，并且要求5个数不同
> 程序的运行过程具有不确定性，因为基数太小，发生冲突的概率相对较大
>
> * 解决办法：随机生成52 的double数，绑定到52张牌上，然后将这52个随机数进行排序，相当于洗牌的过程。
> * 优点：因为double 的基数较大，产生冲突的概率__几乎__为0

```java
    public static void main(String[] args) {
        int n = 52;
        String huase [] = {"♥️","♦️","♣️","♠️"};
        String daxiao []={"2 ","3 ","4 ","5 ","6 ","7 ","8 ","9 ","10","J ","Q ","K ","A "};
        int puke[] = new int[n];
        double xipai[] = new double[n];
        //每一张牌生成一个随机数
        for (int i = 0; i < n; i++) {
            puke[i] = i;
            xipai[i] = Math.random();
        }
        printf(huase, daxiao, puke);
        //洗牌(排序)
        for (int i = 0; i < n; i++) {
            int min = i;
            for (int j = i; j < n; j++) {
                if (xipai[j]<xipai[min]) {
                    min = j;
                }
            }
            if(i != min){
                int temp = puke[i];puke[i] = puke[min];puke[min] = temp;
                double temp2 = xipai[i];xipai[i] = xipai[min];xipai[min]=temp2;
            }
        }
        System.out.println("----------------------------------------------------------------");
        printf( huase, daxiao, puke);
        System.out.println();
    }

    private static void printf(String[] huase, String[] daxiao, int[] puke) {
        for (int i = 0; i < puke.length; i++) {
            //除13 表示花色 %13 表示大小
            System.out.print(huase[puke[i]/13] + daxiao[puke[i]%13] + " ");
            if ((i+1) % 13 == 0) {
                System.out.println();
            }
        }
    }

```
