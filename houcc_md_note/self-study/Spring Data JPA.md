

# Spring Data JPA

## 一、ORM概述

### 1. 使用原始JDBC执行查询语句

实体类

```java
public class User{
	private Integer userId;
  private String username;
  private String address;
  //省略getter和setter方法
}
```

数据库表

```sql
create table t_user(
	`id` bigint primary key auto_increment,
  `username` varchar(50) not null,
  `address` varchar(100)
) ENGINE=InnoDB default CHARSET=utf8;
```

使用JDBC执行查询语句

```java
String sql = "insert into t_user(username, address) values(?, ?)";
//1. 获取连接
Connection conn = DriverManager.getConnection(username, password, url);
//2. 创建statement对象
PreparedStatement ps = conn.prepareStatement(sql);
//3. 可以对占位符进行赋值
ps.setString(1, user.getUsername());
ps.setString(2, user.getAddress());
//4. 发送查询
ps.executeUpdate();s
```

使用JDBC缺点

> - 操作繁琐
> - 占位符赋值麻烦

如何解决？→ 将JDBC封装到工具类

### 2. ORM思想

`主要目的`：操作实体类就相当于操作数据库

`实现`：建立两个映射关系

> - 实体类和表的映射关系
> - 实体类中属性和表中字段的映射关系

实现了ORM思想的框架：`mybatis`、`hibernate`









































