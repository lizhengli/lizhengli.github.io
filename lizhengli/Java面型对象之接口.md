# Java面型对象之接口

---

###接口是interface，其中的方法必须全部为抽象的


###说到interface我们就会提到抽象类，因为两者有相似之处，却也有着明显的区别：
1.接口中的方法必须全部为抽象的，而抽象类中的方法可以有抽象的，也可以有普通的
2.类的继承只能为单继承，而接口却可以多实现
3.抽象类可以有自己的构造器，而接口却不能有构造器
4.抽象类和正常的Java类除了不能实例化之外没有任何区别，而接口确实完全不同的类型！
5.接口只能使用public修饰符
6.借口没有main方法所以我们不能运行它
7.在速度方面抽象类要比接口快一点
8.添加新的方法的时候，如果你往抽象类中添加新的方法，你可以给它提供默认的实现。因此你不需要改变你现在的代码。如果你往接口中添加方法，那么你必须改变实现该接口的类。

###接口的应用：
#### 1.工厂模式：
//汽车类

    interface Car{
    public void run();
    public void stop();
}

class Benz implements Car{
    public void run(){
        System.out.println("Benz开始启动了。。。。。");
    }
    public void stop(){
        System.out.println("Benz停车了。。。。。");
    }
}

class Ford implements Car{
    public void run(){
        System.out.println("Ford开始启动了。。。");
    }
    public void stop(){
        System.out.println("Ford停车了。。。。");
    }
}
// Toyota汽车类

    class Toyota implements Car{
    public void run(){
        System.out.println("Toyota开始启动了。。。");
    }
    public void stop(){
        System.out.println("Toyota停车了。。。。");
    }
}

//工厂类

    class Factory{
    public static Car getCarInstance(String type){
        Car c=null;
        try {
            c=(Car)Class.forName("org.jzkangta.factorydemo03."+type).newInstance();//利用反射得到汽车类型　
        } catch (InstantiationException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    
        return c;
    }
}

public class FactoryDemo03 {

    public static void main(String[] args) {
        Car c=Factory.getCarInstance("Toyota");
        if(c!=null){
            c.run();
            c.stop();
        }else{
            System.out.println("造不了这种汽车。。。");
        }
        

    }

}

####2.适配器模式

1.// 适配器类，直接关联被适配类，同时实现标准接口  
.class Adapter implements Target{  
    // 直接关联被适配类  
    private Adaptee adaptee;  
      
    // 可以通过构造函数传入具体需要适配的被适配类对象  
    public Adapter (Adaptee adaptee) {  
        this.adaptee = adaptee;  
    }  
      
    public void request() {  
        // 这里是使用委托的方式完成特殊功能  
        this.adaptee.specificRequest();  
    }  
.}  
  
  
// 测试类  
public class Client {  
    public static void main(String[] args) {  
        // 使用普通功能类  
        Target concreteTarget = new ConcreteTarget();  
        concreteTarget.request();  
          
        // 使用特殊功能类，即适配类，  
        // 需要先创建一个被适配类的对象作为参数  
        Target adapter = new Adapter(new Adaptee());  
        adapter.request();  
    }  
}  

####代理设计模式（静态代理，动态代理，jdk动态代理）
此设计模式博主也只是简单了解，以后在做补充。





