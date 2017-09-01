# Java Set接口及集合输出


---
##散列存放：HashSet
HashSet是个链表数组。每一个数组元素就是一个列表，我们称为散列表元
使用hashset查找效率很高！
hashCode方法必须与equals方法必须兼容
代码示例：

    //hashCode与equals方法的兼容
     public class Employee{
           public int id;
           public String name="";
           //相同id对象具有相同散列码
           public int hashCode(){ 
                  return id;
           }
           //equals必须比较id
            public boolean equals(Employee x){
                  if(this.id==x.id) return true;
                    else return false;
            }
        }
        
##注意：
    HashSet不能重复存储equals相同的数据
    HashSet的存储是无序的
    hashCode必须和equals必须兼容
    往hashset里面存的时候一定是先判断hash code 值
    
##排序的子类：TreeSet
TreeSet同样也是一个有序的，它的作用是提供有序的Set集合
Treeset的主要方法：

1.add：将指定的元素添加到此 set（如果该元素尚未存在于 set 中）

    public boolean add(E e) {        return m.put(e, PRESENT)==null;    }

2.addAll：将指定 collection 中的所有元素添加到此 set 中
3.iterator：返回在此 set 中的元素上按升序进行迭代的迭代器

    	public Iterator<E> iterator() {        
			  return 	m.navigableKeySet().iterator();
		}
		
4.remove：将指定的元素从 set 中移除（如果该元素存在于此 set 中）
5.size：返回 set 中的元素数（set 的容量）

    public int size() {        return m.size();    }
    
    
    
    
#集合的输出方式（其一）
##Iterator （迭代器）
迭代器的应用：

    list l = new ArrayList();
    l.add("aa");
   	l.add("bb");
	l.add("cc");
	for (Iterator iter = l.iterator(); iter.hasNext();) {
	  Sting str = (String)iter.next();
	    System.out.println(str);
	}
	/*迭代器用于while循环
	Iterator iter = l.iterator();
	while(iter.hasNext()){
	    String str = (String) iter.next();
	    System.out.println(str);
	}
	
##ListIterator
ListIterator迭代器包含的方法有：
1.add(E e): 将指定的元素插入列表，插入位置为迭代器当前位置之前
hasNext()：以正向遍历列表时，如果列表迭代器后面还有元素，则返回 true，否则返回false
    2.hasPrevious():如果以逆向遍历列表，列表迭代器前面还有元素，则返回 true，否则返回false
   3. next()：返回列表中ListIterator指向位置后面的元素
    4.nextIndex():返回列表中ListIterator所需位置后面元素的索引
    5.previous():返回列表中ListIterator指向位置前面的元素
    6.previousIndex()：返回列表中ListIterator所需位置前面元素的索引
    7.remove():从列表中删除next()或previous()返回的最后一个元素（有点拗口，意思就是对迭代器使用hasNext()方法时，删除ListIterator指向位置后面的元素；当对迭代器使用hasPrevious()方法时，删除ListIterator指向位置前面的元素）
    8.set(E e)：从列表中将next()或previous()返回的最后一个元素返回的最后一个元素更改为指定元素e  
    




