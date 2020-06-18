# ElasticSearch

## 一、Restful概念

### 1. 什么是RestFul?

`定义`：如果一个架构符合Rest设计，就称这个架构为Restful架构。Restful是一种软件架构风格，既不是标准也不是规范。

### 2. 什么是Rest?

HTTP协议

`REST`：Resource Representational State Transfer 资源的表现层状态转化

`Representational`：表现层。将网络中资源具体呈现出来的形式称之为表现层

`State Transfer`：状态转化。如果客户端要操作服务器端资源，必须通过某种手段让服务器的资源发生状态转化。

Rest设计原则：

>- 使用REST的URL替换传统URL请求
>
>  传统url：http://localhost:8989/xxx/find?id=21
>
>  RestURL：http://localhost:8989/xxx/find/id
>
>- 使用http四种动词对应服务器端四种操作
>
>  HTTP动词：GET查询获取资源	POST更新操作(添加)	PUT添加操作(更新)	DELETE删除操作

Restful应用场景

```java
@RestController	//这是一个Restful风格控制器
xxxController
//GET查询
@GetMapping("/get")
public String get() {
  ...
}
@PostMapping("/update")
public String post() {
  ...
}
@PutMapping("/put")
public String put() {
  ...
}
```

## 二、ElasticSearch

### 1. 什么是全文检索？



