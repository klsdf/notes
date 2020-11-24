# 概述

所谓的JDBC是Java数据库连接(Java Database Connectivity)的简称,就是如何利用java来操作数据库.

# JDBC基本步骤

1. 注册驱动: 也就是说告诉javaIDE你到底用的是哪个DBMS
2. 获取数据库连接对象: 就是去连接数据库
3. 获取执行sql语句的对象: JDBC是通过一个Statement类型的对象来具体操作数据库的,这步就是创建这个对象.
4. 执行sql，接受返回结果
5. 处理结果: 一般就是打印数据...
6. 释放资源: 就跟c++里面new一样,你new完还得记得delete,不然会内存泄漏.

接下来我们用代码来详细看一下,  

**这个异常是必须加的,不加会报错.**

```java
import java.sql.*;

public class Test {
	public static void main(String[] args) throws Exception {
			/*1.注册驱动,告诉IDE使用mysql*/
			Class.forName("com.mysql.cj.jdbc.Driver");

		  /*2.获取数据库连接对象,连接数据库*/
			Connection connect = DriverManager
					.getConnection("jdbc:mysql://localhost:3306/TwoDimensions?serverTimezone = GMT", "root", "4399");
			/*3.获取执行sql语句的对象*/
			Statement stmt = connect.createStatement();
			/*4.执行sql，接受返回结果*/
      String sql= "select * from girls";
			ResultSet rs = stmt.executeQuery(sql); 
			while (rs.next()) {
				/*5.处理结果,打印刚才查询到的数据,这个操作里面我只打印了一个字段,但是也有别的操作*/
				System.out.println(rs.getString("loli_name"));
			}
			/*6.释放资源*/
			rs.close();
			connect.close();
			stmt.close();
	}
}
```

我们可以发现,其实这些框架都是定死的,不管你连的是啥,不管进行什么操作,大体上都是一样的,只有4和5,根据不同需求要单独处理,所以说以后连接数据库,直接把这个复制过去就行了,仅仅修改4和5的内容即可.

为了节省空间,下面的代码也只会保留4和5的内容,剩下的不会再写.

# 执行SQL

## DDL (数据定义语言)



## DQL (数据查询语言)

## DML (数据操作语言)

## TCL  (事务控制语言)