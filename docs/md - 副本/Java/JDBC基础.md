# JDBC基础

## 1.快速入门

```java
package com.ztt;

import java.sql.Connection;
import java.sql.Driver;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.Statement;

/**
 * @author Zhtao
 * @date 2022/2/26 20:17
 */
public class Jdbcdemo01 {
    public static void main(String[] args)  throws Exception{
        // 1.导入jar包

        // 2.注册驱动
        Class.forName("com.mysql.cj.jdbc.Driver");

        // 3.获取驱动
        Connection con = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/db2", "root", "123456");
        // 4.获取执行者对象
        Statement stat = con.createStatement();
        // 5.执行sql语句，并且接受结果
        String sql = "select * from user";
        ResultSet rs = stat.executeQuery(sql);
        // 6.处理结果
        while (rs.next()) {
            System.out.println(rs.getInt("id") + "\t" + rs.getString("NAME"));
        }
        // 7.释放资源
        con.close();
        stat.close();
        rs.close();
    }

}
```

mysql环境：

![image-20220226203152761](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220226203152761.png)



执行结果：

![image-20220226203242115](https://cdn.jsdelivr.net/gh/zhaotaogit/images/note_img/image-20220226203242115.png)

## 2.DriverManager

### 1.注册驱动

- 注册给定的驱动程序：static void registerDriver(Driver driver);

- 写代码使用:Class.forName("com.mysql.jdbc.Driver")

- 在com.mysql.jdbc.Driver类中存在静态代码块

  ```java
  static {
      try {
          java.sql.DriverManager.registerDriver(new Driver());
      } catch (SQLException E) {
          throw new RuntimeException("Can't register driver!");
      }
  }
  ```

  

### 2.获取数据库连接

static Connection getConnection(String url,String user,String password)

返回值:Connection 数据库连接对象

参数:

- url:指定连接的路径。语法：jdbc:mysql://ip地址:端口号/数据库名称
- user:用户名
- password:密码

## 3.Connection

### 1.数据库连接对象

- 获取执行者对象
  - 获取普通执行者对象:Statement createStatement();
  - 获取预编译执行者对象:PreparedStatement prepareStatement(String sql);
- 管理事务
  - 开启事务:setAutoCommit(bolean autoCommit); 参数为false，则开启事务
  - 提交事务:commit();
  - 回滚事务:rollback();
- 释放资源
  - 立即将数据库连接对象释放:void close();