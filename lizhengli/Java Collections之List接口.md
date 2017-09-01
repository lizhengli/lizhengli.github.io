# Java Collections之List接口



---

##类集设置的目的
其基本的作用就是完成了一个动态的对象数组，里面的数据元素可以动态的增加


##Collenction接口
Collection
    		|--List:元素是有序的，元素可以重复。因为该集合体系有索引。
      	|--ArrayList:底层的数据结构使用的是数组结构。特点：查询速度很快。但是增删稍慢。线程不同步。
        	|--LinkedList:底层使用的链表数据结构。特点：增删速度很快，查询稍慢。线程不同步。
        	|--Vector:底层是数组数据结构。线程同步。被ArrayList替代了。因为效率低。
    	|--Set：元素是无序，元素不可以重复

##List接口
###新的子类ArrayList
    ArrayList List = new ArrayList(); 
	for( int i=0;i <10;i++ ) //给数组增加10个Int元素 
	List.Add(i); 

###旧的子类Vector
vector是线程同步的，所以它也是线程安全的，而arraylist是线程异步的，是不安全的。如果不考虑到线程的安全因素，一般用arraylist效率比较高。
如果集合中的元素的数目大于目前集合数组的长度时，vector增长率为目前数组长度的100%,而arraylist增长率为目前数组长度的50%.如过在集合中使用数据量比较大的数据，用vector有一定的优势

###Vecror 和ArrayList类的区别
ArrayList不具备线程同步的安全性，但速度较快，所以叫裸奔。
Vector具备线程安全。
Vector与ArrayList一样，也是通过数组实现的，不同的是它支持线程的同步，即某	一时刻只有一个线程能够写Vector，避免多线程同时写而引起的不一致性，但实现	同步需要很高的花费，因此，访问它比访问ArrayList慢。
ArrayList中

    public boolean add(E e) {  
        
        ensureCapacity(size + 1);  
        // 增加元素，判断是否能够容纳。不能的话就要新建数组  
          
         elementData[size++] = e;  
        
        return true;  
    
    }  
    public void ensureCapacity(int minCapacity) {  
    
        modCount++;   
    
        int oldCapacity = elementData.length;  
    
        if (minCapacity > oldCapacity) {  
    
        Object oldData[] = elementData; 
        // 此行没看出来用处，不知道开发者出于什么考虑  
    
        int newCapacity = (oldCapacity * 3)/2 + 1; 
        // 增加新的数组的大小  
    
        if (newCapacity < minCapacity)  
        
         newCapacity = minCapacity;  
        
        // minCapacity is usually close to size, so this is a win:  
            
            elementData = Arrays.copyOf(elementData, newCapacity);             
        }  
    
    }  
    
    Vector中：
        private void ensureCapacityHelper(int minCapacity) {  
        
            int oldCapacity = elementData.length;  
        
            if (minCapacity > oldCapacity) {  
            
                Object[] oldData = elementData;  
                int newCapacity = (capacityIncrement > 0) ?(oldCapacity + capacityIncrement) : (oldCapacity * 2);  
        
        if (newCapacity < minCapacity) { 
            newCapacity = minCapacity;  
         }  
        
            elementData = Arrays.copyOf(elementData, newCapacity);  
            
        }  
    
    }  
    
##链表操作类：LinkedList
LinkedList类是双向列表,列表中的每个节点都包含了对前一个和后一个元素的引用

    public class LinkedListTest{ 
        public static void main(String[] args) {
            LinkedList<String> lList = new LinkedList<String>();
            lList.add("1");
            lList.add("2");
            System.out.println("链表的第一个元素是 : " + lList.getFirst());
            System.out.println("链表最后一个元素是 : " + lList.getLast());
        
        }
    }






