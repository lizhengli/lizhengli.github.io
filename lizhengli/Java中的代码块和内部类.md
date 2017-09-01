# Java中的代码块和内部类



---

##一丶代码块

1.普通代码块
直接在一个方法中出现的{}就称为普通代码块，例子程序如下：

　　

    public class CodeDemo01{

　　public static void main(String[] args){

　　//普通代码块

　　{

　　int x = 10;

　　System.out.println("x=" + x);

　　}

　　int x = 100;

　　System.out.println("x=" + x);

　　}

　　}
2.构造块

直接在类中定义的没有加static关键字的代码块{}称为构造代码块，例子程序如下：

    public class CodeDemo02{

　　public CodeDemo02(){

　　System.out.println("========这是构造方法=========");

　　}

　　//这是构造代码块，而且在new对象时，构造代码块优先构造方法执行

　　{

　　System.out.println("=========这是构造块!=========");

　　}

　　public static void main(String[] args){

　　new CodeDemo02();

　　new CodeDemo02();

　　}

　　}
3.静态代码块

例子程序如下：

    public class CodeDemo03

　　{

　　static{

　　System.out.println("这是主类中的静态代码块!");

　　}

　　public static void main(String[] args){

　　new Demo();

　　new Demo();

　　new Demo();

　　}

　　}

　　class Demo

　　{

　　static{

　　System.out.println("这是Demo类中的静态代码块!");

　　}

　　{

　　System.out.println("这是Demo类中的构造块!");

　　}

　　public Demo(){

　　System.out.println("这是构造方法!");

　　}

　　}
###注意：静态块优先于主方法的执行，静态块优先于构造方法的执行，而且只执行一次！

##二丶内部类
###1.内部类的基本格式
外部类名.内部类名  变量名 = 外部类对象.内部类对象;
Outer.Inner in = new Outer().new Inner();

###2.在外部产生内部类的实例化对象示例：

    public class Main {
 
    public static void main(String[] args) {
 
        // 非静态内部类实例对象无法独立存在, 必须依赖于一个外部类的实例对象
        // 所以必须先实例化一个外部类对象
        Demo demo = new Demo();
 
        // 因为 非静态内部类 也是类的 非静态成员, 所以可以用 对象. 来访问
        // 下面用 外部类对象.内部类构造器 来创建内部类对象
        Demo.InnerDemo innerDemo = demo.new InnerDemo();
 
        innerDemo.show();
    }
 
}
 
/**
 * 一个外部类
 */
class Demo {
 
    /**
     * 内部类, 这里的内部类是非静态的。
     *
     * 实例化静态内部类很简单, 直接 类名.内部类名, 这里不多说。
     */
    public class InnerDemo {
 
        /**
         * 内部类的一个方法
         */
        public void show() {
            System.out.println("这是一个内部类的方法");
        }
 
    }
 
}

###3.在方法中定义内部类示例 
方法内部类就是内部类定义在外部类的方法中，方法内部类只在该方法的内部可见，即只在该方法内可以使用。
由于方法内部类不能在外部类的方法以外的地方使用，因此方法内部类不能使用访问控制符和 static 修饰符。
如下所示代码为在方法内部定义一个内部类:

    public class FunOuter {
int out_x = 100;
public void test(){
class Inner{
String x = "x";
void display(){
System.out.println(out_x);
}
}
Inner inner = new Inner();
inner.display();
}
public void showStr(String str){
//public String str1 = "test Inner";//不可定义，只允许final修饰
//static String str4 = "static Str";//不可定义，只允许final修饰
String str2 = "test Inner";
final String str3 = "final Str";
class InnerTwo{
public void testPrint(){
System.out.println(out_x);//可直接访问外部类的变量
//System.out.println(str);//不可访问本方法内部的非final变量
//System.out.println(str2);//不可访问本方法内部的非final变量
System.out.println(str3);//只可访问本方法的final型变量成员
}
}
InnerTwo innerTwo = new InnerTwo();
innerTwo.testPrint();
}
public void use(){
//Inner innerObj = new Inner();//此时Inner己不可见了。
//System.out.println(Inner.x);//此时Inner己不可见了。
}
public static void main(String[] args) {
FunOuter outer = new FunOuter();
outer.test();
}
}

###4.如何使用static声明内部类

    public class StaticInnerClassTest {
       public StaticInnerClassTest() {
              super();
              // TODO Auto-generated constructor stub
       }
 
       public static void main(String[] args) {
              // TODO Auto-generated method stub
        double d[]=new double[20];
        for(int i=0;i<d.length;i++)
               d[i]=100*Math.random();
        //FindMinMax test=new FindMinMax();
        FindMinMax.Pair pair=FindMinMax.getMinMax(d);
        System.out.println("最小值是："+pair.getFirst());
        System.out.println("最大值是："+pair.getSecond());
       }
 
}
 
class FindMinMax{
       static double min=Double.MAX_VALUE;
       static double max=Double.MIN_VALUE;
      
       public static Pair getMinMax(double d[]){
              for(double value:d){
                     if(min>value) min=value;
                     if(max<value) max=value;
              }
              return new Pair(min,max);
       }
      
       public static class Pair{
              public Pair(double first,double second){
                     this.first=first;
                     this.second=second;
              }
             
              public double getFirst(){
                     return this.first;
              }
             
              public double getSecond(){
                     return this.second;
              }
              private double first;
              private double second;
       }
}







