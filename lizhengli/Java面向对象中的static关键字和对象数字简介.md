# Java面向对象中的static关键字和对象数字简介



---

##一、Static关键字
1.static是一个修饰符，用于修饰成员 
2.static修饰的成员被所有对象锁共享 
3.static优先于对象的存在，因为static的成员随着类的加载就已经存在了 
4.static修饰的成员多了一种调用方式，就可以直接被类名调用。类名.静态成员 
5.static修饰的数据是共享数据，对象中的是特有数据

##二丶Static的使用限制
static使用也会有一定的限制：
static表示“全局”或者“静态”的意思，用来修饰成员变量和成员方法，也可以形成静态static代码块，但是Java语言中没有全局变量的概念
static对象可以在它的任何对象创建之前访问，无需引用任何对象。 
用static修饰的代码块表示静态代码块，当Java虚拟机（JVM）加载类时，就会执行该代码块
因为static方法独立于任何实例，因此static方法必须被实现，而不能是抽象的abstract。

##三丶static修饰的主方法：
在Java类中我们通常会见到这样的主方法：
Public static void main（String[] arges）{

}

##四丶Static 的相关应用
static通常会用到以下用途：
 静态方法：
 class Simple {
    static void go() {
       System.out.println("Welcome");
    }
}
静态变量：
声明为static的变量实质上就是全局变量。当声明一个对象时，并不产生static变量的拷贝，而是该类所有的实例变量共用同一个static变量。静态变量与静态方法类似。所有此类实例共享此静态变量，也就是说在类装载时，只分配一块存储空间，所有此类的对象都可以操控此块存储空间，当然对于final则另当别论了
代码实例：
`class Value {
    static int c = 0;
 
    static void inc() {
       c++;
    }
}`

静态类：
public class StaticCls {
    public static void main(String[] args) {
       OuterCls.InnerCls oi = new OuterCls.InnerCls();
    }
}

##五丶对象数组

代码实例：

    public class Student{  
// 成员变量      
private String name; 
private int age; 
// 构造方法
public Student(){
   super();
}
public Student(String name, int age){
super();
this.name = name;
this.age = age；
}// 成员方法
 // getXxx()/setXxx()     
public String getName(){
   return name;
}
public void setName(String name){
   this.name = name;}    
public int getAge(){
return age;}
public void setAge(int age) {
         this.age = age;
     }
     @Override
    public String toString() 
    {
        return "Student [name=" + name + ", age=" + age + "]";
    }
 }






