#### 1. SpringBoot使用RestTemplate来实现项目间接口调用

https://blog.csdn.net/likekobe2012/article/details/82663725

>- 拦截器
>
>1. 编写WebConfig配置文件implements接口WebMvcConfigurer，重写addInterceptors方法，用于对访问路径进行拦截。



#### 2. JsonNode与JSONOBject用法的不同

```java
//ObjectMapper provides functionality for reading and writing JSON
String str = "{"username": "张三", "age": 23}";
ObjectMapper objectMapper = new ObjectMapper();
JsonNode jsonNode = objectMapper.readTree(str);
JsonNode jsonCode = jsonNode.get("username");
```

#### 3. jpa中相关注解

> @CreationTimestamp 在插入时针对注解的属性对应的日期类型创建默认值
>
> @UpdateTimestamp 在更新时针对注解的属性对应的日期类型创建默认值

#### 4. 什么是阿里云OOS?

`阿里云OOS`：Object Storage Service 阿里云对象存储服务

OSSObject



#### 5. ClassPathResource类

用来获取resources文件夹下的文件

```java
ClassPathResource classPathResource = new ClassPathResource("data/测试.txt");
```

文件传输时，文件名乱码（setContentDespositionFormData）

```
headers.setContentDespositionFormData("attachment", new String(“测试.txt”.getBytes("utf-8"), "iso-8859-1"));
```



#### 6. BeanWapper接口

BeanWapper beanWrapper = new BeanWapperImpl();



#### 7. DAO、DO、PO、BO、VO、DTO、POJO理解

> 1）`DAO`：data access object 数据访问对象，主要用来封装对数据库的访问。
>
> 2）`DO`：domain object 持久对象，就是从现实世界中抽象出来的有形或无形的业务实体。
>
> 3）`PO`：persistant object持久对象，最形象的理解就是一个PO就是数据库中的一条记录。好处是可以把一条记录作为一个对象处理，可以方便的转为其他对象。
>
> 4）`BO`：business object业务对象。主要作用是把业务逻辑封装为一个对象，这个对象可以包括一个或多个其它的对象。
>
> 5）`VO`：value object值对象、view object表现层对象。主要对应界面显示的数据对象。对于一个WEB页面、或者SWT、SWING的一个界面，用一个VO对象对应整个界面的值。
>
> 6）`DTO`：Data Transfer Object数据传输对象。主要用于远程调用等需要大量传输对象的地方。
>
> 比如有一张表有100个字段，那么对应的PO就有100个属性。但是我们界面上只要显示10个字段，客户端用web service来获取数据，没有必要把整个PO对象传递到客户端，这时我们就可以用只有这10个属性的DTO来传递结果到客户端，这样也不会暴露服务端表结构。到达客户端后，如果用这个对象来对应界面显示，那此时它的身份就转为VO
>
> 7）`POJO`：plain ordinary java object简单Java对象



#### 8. 使用Specification做查询

> equal：相等
>
> like：模糊查询
>
> in：



#### 9. java8的lambda表达式学习































































































