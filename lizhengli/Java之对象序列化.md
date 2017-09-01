# Java之对象序列化



---

##对象序列化的基本概念
序列化：把Java对象转换为字节序列的过程。
反序列化：把字节序列恢复为Java对象的过程。

##Serializable接口
所谓的Serializable,就是java提供的通用数据保存和读取的接口
Object serialization 允许你将实现了Serializable接口的对象转换为字节序列，这些字节序列可以被完全存储以备以后重新生成原来的对象

##3.进行序列化操作ObjectOutputStream
创建一个user类：

    public class Users implements Serializable{
        
        private static final long serialversionUID=1L;
            
        private String name;
        private int num;
        public Users(String name,int num){
            this.name =name;
            This.num =num;
        }
        public String getName(){
            return name;
        }
        public int getNum(){
            return num;
        }
    }
    
    public class ObjectStreamDemo
    {
        public static void main(String[] args)  
        {
            User[] user = new User[]{new User("dogg",1),new User("catt",2),new User("pigg",3)};  
        
    // 向文件中写入对象  
    try
    {
        ObjectStreamDemo.writeObj(user,args[0]);  
    }  
    catch(Exception e)  
    {  
        System.out.println(e.toString());  
    }  
        
        // 向文件中追加对象  
    try  
    {  
        // 要追加的对象  
        User[] u = new User[]{new User("append1",4),new User("append2",5)};
        
        ObjectStreamDemo.appendObj(u,args[0]);  
    }
    catch(Exception e)
    {
    System.out.println(e.toString());
    }
    // 读取对象  
    try
    {
        List<User> list = ObjectStreamDemo.readObj(args[0]);
        
    // 输出对象信息  
        Iterator<User> it = list.iterator();  
        while(it.hasNext())  
        {  
            User temp = it.next();  
            System.out.println(temp.getName() + "," + temp.getNum());  
        }  
        }  
        catch(Exception e)  
        {  
            System.out.println(e.toString());  
        }  
    }  
    
    static private void appendObj(Object[] objs,String fileName) throws Exception  
    {  
        File file = new File(fileName);  
        
        // 以追加模式创建文件流对象  
        FileOutputStream fis = new FileOutputStream(file,true);  
        ObjectOutputStream oos = new ObjectOutputStream(fis)  
        {  
        // 重写 writeStreamHeader()方法，空实现  
        protected void writeStreamHeader(){};  
        };  
        
        // 写入数据  
        for(Object o : objs)  
        {
            oos.writeObject(o);  
        }
        
        // 关闭流  
         oos.close();  
        }
        static private List<User> readObj(String fileName) throws Exception  
        {
            File file = new File(fileName);  
        
        // 使用List保存读取出来的对象  
        ArrayList<User> list = new ArrayList<User>();  
        
        // 创建流对象  
        FileInputStream fis = new FileInputStream(file);  
        ObjectInputStream ois = new ObjectInputStream(fis);  
        
        // 读取对象并放入List容器中  
        while(fis.available() > 0)  
        { 
         list.add((User)ois.readObject());  
        }  
        
            ois.close();  
            return list; // 返回List  
        }  
        
         static private void writeObj(Object[] objs,String fileName) throws Exception  
        {  
        // 使用命令行参数中指定的文件名  
        File file = new File(fileName);  
        
        // 创建流对象  
        ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(file));  
        
        // 写入对象  
        for(Object o : objs)  
        {  
            oos.writeObject(o);  
        }  
        
        // 关闭流  
        oos.close();  
     }  
    }  
    
###4.进行反序列化操作ObjectInputStream
    import java.io.*;import java.util.Date;
    public class ObjectSaver {
    public static void main(String[] args) throws Exception {
        /*其中的  D:\\objectFile.obj 表示存放序列化对象的文件*
        
        //反序列化对象
        ObjectInputStream in = new ObjectInputStream(new         FileInputStream("D:\\objectFile.obj"));
        System.out.println("obj1 " + (String) in.readObject()); 
        //读取字面值常量
        System.out.println("obj2 " + (Date) in.readObject()); 
        //读取匿名Date对象
        Customer obj3 = (Customer) in.readObject();   
        //读取customer对象
            System.out.println("obj3 " + obj3);
         in.close();
        }
    }
    class Customer implements Serializable {
        private String name;
        private int age;
        public Customer(String name, int age) {
            this.name = name;
            this.age = age;
         }

        public String toString() {
            return "name=" + name + ", age=" + age;
     }
    }




