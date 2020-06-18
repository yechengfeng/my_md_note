## 一、jdbc技术存在问题

>- 大量的代码冗余
>- 实体对象和查询结果不能做自动封装（需要手动封装实体）

代码示例：

```java
UserDao
  public void add(User user);
	public User findById(String id);
UserDaoImpl
  public void add(User user) {//问题1.执行增删改时，代码存在大量的冗余
  	//获取连接
  	Connection conn = …… getConnection();
  	//创建pstm
  	String sql = "insert into ……";
  	pstm = conn.prepareStatement(sql);
  	//赋值
  	pstm.setString(1, user.getName());
  	……
    //执行sql
    pstm.executeUpdate();
	}
	
	public User findById(String id) {
    //获取连接
    Connection conn = …… getConnection();
    String sql = "select * from …… where id = ?";
    pstm = conn.prepareStatement(sql);
    //赋值
    pstm.setString(1, id);
    //执行sql
    ResultSet rs = pstm.executeQuery();
    //处理结果集
    User user = null;
    if(rs.next()) {
      user = new User();//问题2.不能完成实体与数据库的直接转换，需要手动封装
      user.setId(rs.getString("id"));
      user.setName(rs.getString("name"));
      ……
    }
  }
```

## 二、Mybatis核心开发思路

配置文件2个

主配置文件

### 1. 主配置文件mybatis-config.xml

> 1）书写连接相关参数
>
> ​		driver、url、username、password
>
> 2）书写mapper映射文件
>
> ​		<mappers>
>
> ​				<mapper resources="……">
>
> ​		</mappers>

代码示例：

```xml
com.baizhi.dao
interface UserDao
public User findById(String id);

映射文件 UserDaoMapper.xml
<select id="Dao接口中方法名findById" parameterType="参数类型String" resultType="com.baizhi.entity.User">
  select id, name from t_user where id = #{id}
</select>
其中id的值对应的是方法名findById；parameterType对应的是参数类型String类型；
resultType即为返回值的类型，自动封装成对象；#{id}即为传入的参数名；
```

