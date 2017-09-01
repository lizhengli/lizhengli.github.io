# Java线程经典例子生产消费者模式



---
##Java线程生产消费模式应用广泛，体现全面
代码示例：

    public class Producter implements Runnable{
	///生产者
	private Storage storage;
	private int number;
	public Producter(Storage storage,int number){
		this.storage = storage;
		this.number = number;
	}
	
	public void  run(){
		while(true){
			try {
				//睡觉
				Thread.sleep(2000);
			} catch (InterruptedException e) {
	
				e.printStackTrace();
			}
			storage.push(number);
	    	}
        		
    	}
     
    }
    public class Cousrtem implements Runnable{
    	//消费者
    	private Storage storage;
	    private int number;
	    public Cousrtem(Storage storage,int number){
		    this.storage = storage;
		    this.number = number;
	    }
	        
	        
    	public void run(){
	    	while(true){
		    	try {
			    	Thread.sleep(2000);//睡眠两秒
			    } catch (InterruptedException e) {
	            
				    e.printStackTrace();
		    	}
			storage.pop(number);
		    }
	        	
	    }
        
    }
    public class Main {
    	public static void main(String[] args){
		    
	    	Storage storage = new  Storage(0);
		    
	        	//消费者
	       	Cousrtem cousrtem1 = new Cousrtem(storage,40);
	    	Cousrtem cousrtem2= new Cousrtem(storage,70);
		    Cousrtem cousrtem3 = new Cousrtem(storage,40);
		    
		    //生产者
		    Producter producter1 = new Producter(storage,80);
		    Producter producter2 = new Producter(storage,60);
		    Producter producter3 = new Producter(storage,20);
		    
		    //启动线程
		    new Thread(cousrtem1).start();
		    new Thread(cousrtem2).start();
		    new Thread(cousrtem3).start();
		    new Thread(producter1).start();
		    new Thread(producter2).start();
		    new Thread(producter3).start();
	    }
    }
    
##附：线程的生命周期

新->可运行<->运行->死
        |       |
        上      下
    等待/阻塞/睡眠
        







