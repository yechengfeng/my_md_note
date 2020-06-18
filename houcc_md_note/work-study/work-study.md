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