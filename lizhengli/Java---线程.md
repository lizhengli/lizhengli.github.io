# Java---线程



---

##一、进程与线程的区别
关于进程的特性
独立性：
进程是系统中独立存在的实体，它可以拥有自己独立的资源，每个进程都拥有自己私有的地址空间。在没有经过进程本身运行的情况下是不能访问其中的内容的。

动态性：
进程与程序的区别在于，程序是静态的，进程是动态的。程序只是一个静态的指令集合，而进程是一个正在系统中运行的指令集合。有了时间的概念，如生命周期；

并发性：
进程之间，交替着执行。
线程，一个顺序执行流；
它是进程的组成部分，一个进程可以有多个线程

##二丶Java的线程实现的两种方式

###继承Thread类
继承Thread类，重写Thread的run()方法，将线程运行的逻辑放在其中。
代码示例：

    public class Xc extends Thread{
        String name = null;
        int ticket = 0;
        public MyThread(String name){
            this.name = name;
        }
        public synchronized void run(){
            for (int i = 0; i < 5; i++) {
                 System.out.println(Thread.currentThread().getName()+this.name+" 		ticket:"+ticket++)
                 try {
                    Thread.sleep(100);
                }catch(Exception e){
                    E.printStackTrace();
                }
            }
            //通过以下方式运行
            public static void main(String[] args){
            Xc xc1 = new Xc(“线程1”)；
            Xc xc2 = new Xc(“线程2”)；
            xc1.start();
            xc2.start();
        }
    
    }
    
##实现Runnable接口
代码示例：

    public class RunDemo implements Runable{
        private int tick = 50;
        public void run(){
            while(true){
                if(tick > 0) {
                System.out.println( Thread.currentThread().getName() + " sail --" + tick--);
             }
        }
     }
    }
    
    
        public class Tick{
            public static void main(String[] args){
                RunDemo rd = new RunDemo();
                Thread t1 = new Thread(rd);
                Thread t2 = new Thread(rd);
                t1.start();
                t2.start();
            
            }
        }
        
##两种实现方式的区别
实现Runnable接口相对于继承Thread类来说，有如下显著的好处：
(1)适合多个相同程序代码的线程去处理同一资源的情况，把虚拟CPU（线程）同程序的代码，数据有效的分离，较好地体现了面向对象的设计思想。
(2)可以避免由于Java的单继承特性带来的局限。我们经常碰到这样一种情况，即当我们要将已经继承了某一个类的子类放入多线程中，由于一个类不能同时有两个父类，所以不能用继承Thread类的方式，那么，这个类就只能采用实现Runnable接口的方式了。
(3)有利于程序的健壮性，代码能够被多个线程共享，代码与数据是独立的。当多个线程的执行代码来自同一个类的实例时，即称它们共享相同的代码。 多个线程操作相同的数据，与它们的代码无关。当共享访问相同的对象是，即它们共享相同的数据。当线程被构造时，需要的代码和数据通过一个对象作为构造函数 实参传递进去，这个对象就是一个实现了Runnable接口的类的实例。
###另外：
一个是多个线程分别完成自己的任务，一个是多个线程共同完成一个任务。

##线程的操作方法
1.取得当前的线程、设置和取得名字

    public final String getName();获取线程的名字；
    public final void setName();设置线程的名字；
2.判断线程的运行状态
    线程计数器，使用Thread.join方法
3.线程的休眠
结束休眠状态有两种途径：
①休眠时间到达后，线程重新进入运行状态。
②处于休眠状态的线程遇上Java.lang.InterruptedException异常，从而被迫停止休眠。
使线程进入休眠状态可以直接调用Thread.sleep();打断某线程的休眠状态的手段是调用该线程的interrupt()方法

    public class MyThread implements Runable{
        public void run(){
            System.out.println(“sleep”);
            try{
            Thread.sleep(2000);
        }catch(Exception e){
        
        }
        System.out.println(“休息两秒”)
        }
    }
    public class MyThread2{
        public static void main(String[] args){
            MyThread mt = new MyThread();
            Thread th = new Thread(mt);
            Th.start();
        }
    }       
    
##线程的中断
中断是通过调用Thread.interrupt()方法
代码示例：

    public class Thread3 extends Thread{  
        public void run(){  
            while(true){  
                if(Thread.interrupted()){  
                System.out.println("Someone interrupted me.");  
            }  
            else{  
             System.out.println("Going...");  
            }  
            long now = System.currentTimeMillis();  
            while(System.currentTimeMillis()-now<1000){  
            // 为了避免Thread.sleep()而需要捕获InterruptedException而带来的理解上的困惑,  
            // 此处用这种方法空转1秒  
             }  
           }  
    }  
        public static void main(String[] args) throws InterruptedException {  
        Thread3 t = new Thread3();  
        t.start();  
        Thread.sleep(3000);  
        t.interrupt();  
        }  
    }  
    
    
##线程的同步与死锁
所谓死锁: 是指两个或两个以上的进程在执行过程中，因争夺资源而造成的一种互相等待的现象，若无外力作用，它们都将无法推进下去。那么为什么会产生死锁呢？
1.因为系统资源不足。
2.进程运行推进的顺序不合适。   
 3.资源分配不当。            
 学过操作系统的朋友都知道：产生死锁的条件有四个：
1.互斥条件：所谓互斥就是进程在某一时间内独占资源。
2.请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
3.不剥夺条件:进程已获得资源，在末使用完之前，不能强行剥夺。
4.循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。





