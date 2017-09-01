#Java语法入门


---

## 一 丶变量
### 1.数据类型
数据类型大体的可以分为两大类：
1.基本数据类型：
数值型 byte、short、int、long、float、double
.整数类型int  
.字符型char 
.布尔型boolean  
.浮点数类型float、double
2.引用数据类型：
类，枚举，注解，接口，数组
## 2数据进制
计算机语言使用的为二进制数制，二进制是计算机技术中广泛采用的一种数制。

##3.标识符
标识符由26个英文字符大小写（a~zA~Z）、数字(0~9)、下划线(_)和美元符号($)组成。
注意：
1.不能以数字开头，不能是关键字
2.区分大小写
3.标识符的可以为任意长度


##4.类型转换
基本数据类型转换之向上转型：
1.Boolean类型是不可以转换为其他基本数据类型

2.整型，字符型，浮点型的数据在混合运算中相互转换，转换时遵	循以下原则：
				容量小的类型可自动转换为容量大的数据类型
				Byte，short，char --int --long --float --double
				Byte,short,char之间不会相互转换，他们在计算时首先会转换为int类型
			基本数据类型之向下转型：
				1.容量大的数据类型转换为容量小的数据类型时，要加上强制				转换符，但可能造成精度的降低或溢出，使用时要格外注意。
				2.有很多种类型的数据混合运算时，系统首先自动的将所有数				据中转换成容器最大的那一种数据类型，在进行计算。
				3.浮点型：默认是double
				4.整形：默认是int


##二丶Java的基本语法格式
Java拥有以下关键字：
abstract	do	implement	private	this
boolean	double	import	protected	throw
break	else	instanceof 	public	throws
byte	extends	int	return	transient
case	false	interface	short	true
catch	final	long	static	try
char	fianlly	native	strictfp	void
class	float	new	super	volatile
continue	for	null	switch	while
default	if 	package	enum	synchronized
assert		

###Java的常量
程序中固定不变的值
例如：false，true


##三丶Java的表达式和语句
###1.条件语句 
条件语句，是程序中根据条件是否成立进行选择执行的一类语句
If,else
###2.循环语句   for( 量: 容器)
for(int i=0;i<100;i++){
....
}
While(true){

}
do{

}while(i=1)
###3.break 和continue
break：终止该层循环
continue：跳过该层循环

##Java经典例子---冒泡排序：

    public class Program
    {
        public static void Main(string[] args)
        {
            int[] count = new int[5];  //  需要排序的数组
            int i, j;                  //  循环变量
            int temp;                  //   临时变量
            //读入数组
            Console.WriteLine("请输入5个数：");
            for (i = 0; i < 5; i++)
            {
                Console.WriteLine("输入第{0}个数：", i + 1);
                count[i] = int.Parse(Console.ReadLine());//类型转换
            }
            // 开始排序 -----------冒泡排序
            for (i = 0; i < count.Length - 1; i++)   // 控制比较多少轮
            {
                // 将最大的元素交换到最后
                for (j = 0; j < count.Length - 1 - i; j++)
                {
                    if (count[j] > count[j + 1])
                    {
                        //  交换元素
                        temp = count[j];
                        count[j] = count[j + 1];
                        count[j + 1] = temp;
                    }
                }
            }
            //  排序后输出
            Console.WriteLine("排序后：");
            for (i = 0; i < count.Length; i++)
            {
                Console.WriteLine("{0}\t", count[i]);
            }
            Console.ReadLine();
        }
    }
}

###此篇简单的讲解了Java的语法，以及应用了一个简单的冒泡排序的案例，
希望对大家有所帮助！




