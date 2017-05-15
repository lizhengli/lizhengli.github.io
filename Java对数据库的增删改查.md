Java实现对数据库的增删改查
import java.sql.*;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
public class SqlDemo {

	public static void main(String[] args) {
	    //声明Connection对象
		Connection con;
		//驱动程序名
		String driver = "com.mysql.jdbc.Driver";
		//URL指向要访问的数据库名mydata
		String url = "jdbc:mysql://localhost:3306/java";
		//MySQL配置时的用户名
		String user = "root";
		//MySQL配置时的密码
		 String password = "123456";
		//遍历查询结果集
		try {
			//加载驱动程序
			Class.forName(driver);
			//1.getConnection()方法，连接MySQL数据库！！
			con = DriverManager.getConnection(url,user,password);
			if(!con.isClosed())
			System.out.println("Succeeded connecting to the Database!");
			//2.创建statement类对象，用来执行SQL语句！！
			Statement statement = con.createStatement();
			//要执行的SQL语句
			String sql = "select * from emp";
			String del = "select * from emp where ename like '李%'";
			//3.ResultSet类，用来存放获取的结果集！！
		    ResultSet rs = statement.executeQuery(sql);
		   // ResultSet rs2 = statement.executeQuery(del);
			System.out.println("-----------------");
			System.out.println("执行结果如下所示:");  
			System.out.println("-----------------");  
			System.out.println("姓名" + "\t" + "职位"+"\t"+"薪资");  
			System.out.println("-----------------");       
			String job = null;
			String id = null;
			Float gz = null;
			while(rs.next()){
				//获取stuname这列数据
				job = rs.getString("job");
				//获取stuid这列数据
				id = rs.getString("ename");
				//获取sal这列数据
				gz = rs.getFloat("sal");
				//输出结果
				System.out.println(id + "\t" + job+"\t"+gz);
			}
			PreparedStatement psql;
			ResultSet res;
			//预处理添加数据，其中有两个参数--“？”
			psql = con.prepareStatement("insert into emp (empno,ename,job,hiredate,sal)"
			+ "values(?,?,?,?,?)");
			psql.setInt(1,0004);
			psql.setString(2,"0002");
			psql.setString(3,"凡凡");
			//psql.setInt(1, 3212);      //设置参数1，创建id为3212的数据
			//psql.setString(2, "王刚");      //设置参数2，name 为王刚
			//psql.setString(3, "总裁");
			DateFormat dateFormat2 = new SimpleDateFormat("yyyy-MM-dd");
			java.util.Date myDate2 = dateFormat2.parse("2010-09-14");
			psql.setDate(4,new java.sql.Date(myDate2.getTime()));
			psql.setFloat(5, (float) -6666.3);
			//预处理更新数据
			//psql = con.prepareStatement("update emp set sal = ? where ename = ?");
			//psql.setFloat(1,(float)5000.0);
			//psql.setString(2,"王刚");
			psql.executeUpdate();  //执行更新
			//预处理删除数据
			//psql = con.prepareStatement("delete from emp where sal > ?");
			//psql.setFloat(1,4500);
			//psql.executeUpdate();  //执行更新
			//psql.close();
			rs.close();
			con.close();
		}catch(ClassNotFoundException e) {   
			//数据库驱动类异常处理
			System.out.println("Sorry,can`t find the Driver!");   
			e.printStackTrace();   
		}catch(SQLException e) {
		//数据库连接失败异常处理
			e.printStackTrace();  
		}catch (Exception e) {
		
			e.printStackTrace();
		}finally{
			System.out.println("数据库数据成功获取！！");
		}
	 }

	}

