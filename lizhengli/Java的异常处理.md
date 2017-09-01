# Java的异常处理


---

##一丶什么是异常？
异常机制，是指程序不正常时的处理方式。具体来说，异常机制提供了程序退出的安全通道。当出现	错误后，程序执行的流程发生改变，程序的控制权转移到异常处理器。

##二丶处理异常的基本语法

    try{
     //可能会出现异常的代码
    }catch{
    解决方法
    }final{
        
    }
    
##三丶异常的处理流程
1、当程序运行时出现异常之后，那么会由JVM自动根据异常的类型实例化一个与之类型匹配的异常类对象，（此处用户不用去关系 new ，由系统自动负责处理）
2、产生异常对象之后会判断当前语句是否存在异常处理，如果没有，那么交给JVM进行默认的异常处理，处理方式为，输出异常信息，并结束程序调用。
3、如果存在异常捕获操作，那么由try语句来捕获产生的异常类实例化对象，而后与每一个try语句后的每一个catch进行比较，如果有合适的捕获类型，则使用当前的catch语句进行异常的处理，如果不匹配，则继续向下匹配其他的catch 。
4、不管最后异常处理时候能够匹配，都要向后执行，如果程序中存在finally语句，那么就先执行finally中的代码，但是执行完毕后需要根据之前的catch匹配结果来决定如何执行，如果之前成功捕获异常，那么就继续执行finally之后的代码，如果之前没有成功捕获，那么将此异常交给JVM进行默认处理（输出异常信息，结束程序运行）

##四丶异常类的继承关系
RuntimeException与Exception, Error不同点： 当方法体中抛出非RuntimeException（及其子类）时，方法名必须声明抛出的异常；但是当方法体中抛出RuntimeException（包括RuntimeException子类）时，方法名不必声明该可能被抛出的异常，即使声明了，JAVA程序在某个调用的地方，也不需要try-catch从句来处理异常

##五丶Throw和Throws关键字

    throws是方法可能抛出异常的声明。(用在声明方法时，表示该方法可能要抛出异常)
	语法：[(修饰符)](返回值类型)(方法名)([参数列表])[throws(异常类)]{......}
	throw是语句抛出一个异常
    throw e;
    
##六丶异常的标准处理代码实例：

    1.try{   
      //（尝试运行的）程序代码   
    }catch(异常类型 异常的变量名){   
        //异常处理代码   
    }finally{   
        //异常发生，方法返回之前，总是要执行的代码   
    }  
    
    
##七丶RuntimeException与Exception 的区别
在Java的异常类体系中,Error和RuntimeException是非检查型异常，其他的都是检查型异常。

所有方法都可以在不声明throws的情况下抛出RuntimeException及其子类 

不可以在不声明的情况下抛出非RuntimeException

简单的说，非RuntimeException要自己写catch块处理掉

##八丶根据需要来自定义异常
自定义异常我们需要继承Exception类

    public class MyFirstException extends Exception {   
        public MyFirstException() {   
            super();   
        }   
        public MyFirstException(String msg) {   
            super(msg);   
        }   
        public MyFirstException(String msg, Throwable cause) {   
            super(msg, cause);   
        }   
        public MyFirstException(Throwable cause) {   
        super(cause);   
    }   
        //自定义异常类的主要作用是区分异常发生的位置，当用户遇到异             常时，   
        //根据异常名就可以知道哪里有异常，根据异常提示信息进行修改    。   
    }  







