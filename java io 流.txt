#Java I/O 流
1.按照方向分为：
输入流（InputStream） 输出流(OutputStream)；
2.按照处理单位不同分为：
字符流(Reader) 字节流(Writer)；

InputStream OutputStream 
上面两个类是输入输出流的顶级类，其他类都是从这两个类继承产生的；

        字节流         字符流

输入流  InputStream    Reader

输出流  OutputStream   Writer

下面代码表示创建一个文件并向里面输入数据保存：
class Demo{
  public static void main(String[] args){
    File f = new File("Test.txt");
     if(!f.exists()){
      try{ //抛出异常；
        f.createNewFile();//如果文件不存在那么就创建一个；
      } catch(IOException e){
        e.printStackTrace();
      }
    }
    FileReader fr = null;
    FileWriter fw = null;
    String strings = "hello world";
    char[] chars = new char[1024];//缓冲区
    int len = 0;
    try{
      fr = new FileReader(f);
      StringBuffer snb = new StringBuffer();
      while((len = fr.read(chars))!=-1){ //将源文件里的数据读入，避免覆盖
        snb.append(new String(chars,0,len));
        strings+=snb;
      }
      fw = new FileWriter(f);
      fw.write(strings);//将数据写出文件
    }catch(IOException e){
      e.printStackTrace();
    }finally{
      if(fr!=null){
        try{
          fr.close();//关闭输入流；
        }catch(IOException e){
          e.printStackTrace();
        }
      }
      if(fw!=null){
        try{
          fw.close();//关闭输出流；
        }catch(IOException e){
          e.printStackTrace();
        }
      }
    }
  }
}
