# Java IO之File类



---
##使用File类创建文件
代码示例如下 ：

    public class FileDemo{
        public static void main(String[] args){
        //构造函数File（String pathname）;
            File f1 = new File(“d://abc//liu.txt”);
        //构造函数File（String parent , string chlid）;
            File f2 = new File(“d://abc”,”2.txt”);
                
            System.out.println(f1);

        }
    }
    
##删除文件
代码示例：

    public class DeleteFile {

      /**
     * 删除文件或空文件夹
     * @param file
     * @return
     * @throws Exception
     */
    public static boolean deleteFile(String path)throws Exception{
        File file = new File(path);
        boolean flag = false;
        if(file.isFile()){
            flag = file.delete();
        }
        if(file.isDirectory()){
            if(file.listFiles().length <= 0){
                flag = file.delete();
            }
        }
        return flag;
    }
    
    /**
     * 删除文件夹下的所有文件
     * @param path
     * @throws Exception
     */
    public static void deleteDir(String path)throws Exception{
        File file = new File(path);
        File[] files = null;
        if(file.isFile()){
            file.delete();
        }else{
            files = file.listFiles();
            for (int i = 0; i < files.length; i++) {
                //System.out.println(files[i].getPath());                deleteDir(files[i].getPath());
                files[i].delete();
            }
            file.delete();
        }
    }
    
    public static void main(String[] args)throws Exception{
        //System.out.println(deleteFile(new File("d:1.txt")));
        //System.out.println(new File("d:/demo").getName());
        deleteDir("d:/html");
    }
}

##File 判断文件类型

    public class Ch2 {
        private static final String RAGEX="[0x00-0x07]";
        public static void main(String[] args) throws IOException {
            File file=new File("c:/abc");
            File[] files=file.listFiles();
            for(int i=0;i<files.length;i++){
                 System.out.println(files[i].getName()+"\t"+getCheck(files[i          ]));
        }
        }
        public static boolean getCheck(File f) throws IOException{
            BufferedReader br=new BufferedReader(new             FileReader(f));
            String temp="";
            while((temp=br.readLine())!=null){
                for(int i=0;i<temp.length();i++){
                    if((temp.charAt(i)+"").matches(RAGEX)){
                        return true;
                }
            }
        }
          br.close();
          return false;
        }
    }
    
##列出目录中的内容
代码示例：

    public class FileStructure {
            
        int tabCounter = 0;
            
        public void listFilesAndFolders(String folder) {
            
        File file = new File(folder);
            
        if (!file.exists() || !file.isDirectory()) {
                
            System.out.println("目录无效");
            System.exit(1);
            
        }
            
        File[] fileArray = file.listFiles();
            
        for (int i = 0; i < fileArray.length; i++) {
            
            if (fileArray[i].isDirectory()) {
            
                System.out.println(getTabs() + "- " +         fileArray[i].getName());
            tabCounter++;
            listFilesAndFolders(fileArray[i].getAbsolutePath());
            
        }
        else {
            
            System.out.println(getTabs() + fileArray[i].getName());
        }
    }
        tabCounter--;
        
    }
                
        private String getTabs() {
                      
        StringBuffer buffer = new StringBuffer();
        for (int i = 0; i < tabCounter; i++)
            buffer.append("\t");
            
            return buffer.toString();
        }
            
        public static void main(String[] args) {
            
        FileStructure fileStructure = new FileStructure();
        fileStructure.listFilesAndFolders("C:\\temp");
     }
    }





