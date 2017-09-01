# Java的常用类


---

##一丶StringBuffer类

###什么是StringBuffer？
StringBuffer类和String一样，也用来代表字符串，只是由于StringBuffer的内部实现方式和String不同，所以StringBuffer在进行字符串处理时，不生成新的对象，在内存使用上要优于String类

###StringBuffer的常用方法代码示例：

    public class UsingStringBuffer {  
            /** 
        * 查找匹配字符串 
        */  
        public static void testFindStr() {  
            StringBuffer sb = new StringBuffer();  
            sb.append("This is a StringBuffer");  
            // 返回子字符串在字符串中最先出现的位置，如果不存在，返回负数  
        System.out.println("sb.indexOf(\"is\")=" + sb.indexOf("is"));  
        // 给indexOf方法设置参数，指定匹配的起始位置  
        System.out.println("sb.indexOf(\"is\")=" + sb.indexOf("is", 3));  
    // 返回子字符串在字符串中最后出现的位置，如果不存在，返回负数  
    System.out.println("sb.lastIndexOf(\"is\") = " + sb.lastIndexOf("is"));  
    // 给lastIndexOf方法设置参数，指定匹配的结束位置  
    System.out.println("sb.lastIndexOf(\"is\", 1) = "  
    + sb.lastIndexOf("is", 1));  
    }  
        
        /** 
        * 截取字符串 
        */  
        public static void testSubStr() {  
             StringBuffer sb = new StringBuffer();  
            sb.append("This is a StringBuffer");  
    // 默认的终止位置为字符串的末尾  
        System.out.print("sb.substring(4)=" + sb.substring(4));  
    // substring方法截取字符串，可以指定截取的起始位置和终止位置  
    System.out.print("sb.substring(4,9)=" + sb.substring(4, 9));  
    }  
        
    /** 
    * 获取字符串中某个位置的字符 
    */  
        public static void testCharAtStr() {  
            StringBuffer sb = new StringBuffer("This is a StringBuffer");  
            System.out.println(sb.charAt(sb.length() - 1));  
        }  
        
        /** 
            * 添加各种类型的数据到字符串的尾部 
            */  
        public static void testAppend() {  
            StringBuffer sb = new StringBuffer("This is a StringBuffer!");  
            sb.append(1.23f);  
            System.out.println(sb.toString());  
        }  
        
        /** 
        * 删除字符串中的数据 
        */  
        public static void testDelete() {  
            StringBuffer sb = new StringBuffer("This is a StringBuffer!");  
            sb.delete(0, 5);  
            sb.deleteCharAt(sb.length() - 1);  
            System.out.println(sb.toString());  
            }  
            
            /** 
            * 向字符串中插入各种类型的数据 
            */  
            public static void testInsert() {  
            StringBuffer sb = new StringBuffer("This is a StringBuffer!");  
      // 能够在指定位置插入字符、字符数组、字符串以及各种数字和布尔值  
        sb.insert(2, 'W');  
        sb.insert(3, new char[] { 'A', 'B', 'C' });  
        sb.insert(8, "abc");  
        sb.insert(2, 3);  
        sb.insert(3, 2.3f);  
        sb.insert(6, 3.75d);  
        sb.insert(5, 9843L);  
        sb.insert(2, true);  
        System.out.println("testInsert: " + sb.toString());  
    }  
        
        /** 
        * 替换字符串中的某些字符 
        */  
    public static void testReplace() {  
    StringBuffer sb = new StringBuffer("This is a StringBuffer!");  
        // 将字符串中某段字符替换成另一个字符串  
            sb.replace(10, sb.length(), "Integer");  
            System.out.println("testReplace: " + sb.toString());  
        }  
        /** 
        * 将字符串倒序 
        */  
     public static void reverseStr() {  
        StringBuffer sb = new StringBuffer("This is a StringBuffer!");  
        System.out.println(sb.reverse()); // reverse方法将字符串倒序  
     }  
    }  
    
##Math类
常用方法：
Math.PI 记录的圆周率 
	Math.E 记录e的常量 
	Math中还有一些类似的常量，都是一些工程数学常用量。
Math.abs 求绝对值 
	Math.sin 正弦函数 Math.asin 反正弦函数 
	Math.cos 余弦函数 Math.acos 反余弦函数 
	Math.tan 正切函数 Math.atan 反正切函数 Math.atan2 商的反正切函数 
	Math.toDegrees 弧度转化为角度 Math.toRadians 角度转化为弧度 
	Math.ceil 得到不小于某数的最大整数 
	Math.floor 得到不大于某数的最大整数 
	Math.IEEEremainder 求余 
	Math.max 求两数中最大 
	Math.min 求两数中最小 
	Math.sqrt 求开方 
	Math.pow 求某数的任意次方, 抛出ArithmeticException处理溢出异常 
	Math.exp 求e的任意次方 
	Math.log10 以10为底的对数 
	Math.log 自然对数 
	Math.rint 求距离某数最近的整数（可能比某数大，也可能比它小） 
	Math.round 同上，返回int型或者long型（上一个函数返回double型） 
	Math.random 返回0，1之间的一个随机数
用法实例： 
double s=Math.sqrt(7); 
double x=Math.pow(2,3) //计算2的3次方

##日期操作类
java api中日期类型的继承关系>>
    java.lang.Object
      --java.util.Date
          --java.sql.Date
          --java.sql.Time
          --java.sql.Timestamp
java.util.Date表示特定的瞬间，精确到了毫秒>>
boolean	after(Date when) 
          测试此日期是否在指定日期之后。
 boolean	before(Date when) 
          测试此日期是否在指定日期之前。
 Object	clone() 
          返回此对象的副本。
 int	compareTo(Date anotherDate) 
          比较两个日期的顺序。
 boolean	equals(Object obj) 
          比较两个日期的相等性。
 long	getTime() 
          返回自 1970 年 1 月 1 日 00:00:00 GMT 以来此 Date 对象表示的毫秒数。（最常用的方法了）

##DateFormat类 
日历，可以对date格式化




