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





### 2. ElasticSearch安装

前提条件jdk环境

网上提供的安装教程[Windows下安装elasticsearch7.4.0+Kibana+ik分词器](https://blog.csdn.net/qq_38138069/article/details/102516947)

#### 1）安装`elasticsearch`

> - 点击[ElasticSearch](https://www.elastic.co/cn/downloads/past-releases/elasticsearch-6-3-2)下载ZIP包并解压
> - 双击bin目录下elasticsearch.bat文件，访问localhost:9200（默认端口号9200）

![es](elasticsearch.assets/es-1593333673369.png)

**注意**：ElasticSearch安装包应该放在没有空格和汉字的路径下，否则请求时会出现500

#### 2）安装ElasticSearch的操作界面`kibana`

> - 点击[kibana](https://www.elastic.co/cn/downloads/past-releases#kibana)下载与elasticsearch相同版本的kibana并解压；
> - 双击bin目录下kibana.bat文件启动kibana，启动完成后访问localhost:5601（默认端口号5601）

**注意**：kibana默认连接本地的elasticsearch，如需访问其他服务器的es或者es的端口号有被调整过，需要在config/kibana.yml文件中重新设置elasticsearch.hosts

#### 3）安装`IK分词器`

> - 点击[IK分词器](https://github.com/medcl/elasticsearch-analysis-ik/releases)下载对应版本的elasticsearch_analysis_ik；
> - 在elasticsearch安装包plugins文件夹下创建文件analysis-ik文件，讲ik分词器zip包解压到改文件夹；
> - 在config文件夹下的IKAnalyzer.cfg.xml配置文件中添加自定义分词此表和停用词词表，在相应的词表文件中添加分词重启es就可以啦~

`安装elasticsearch-head`

- 安装node.js，官网[https://nodejs.org/zh-cn/download/](https://nodejs.org/zh-cn/download/)下载node.js的msi版本进行傻瓜式安装；安装完成进入cmd终端执行node可进入node环境，两次ctrl+c退出；查看版本node -v   npm-v；安装淘宝npm:npm install ``-``g cnpm ``-``-``registry``=``https:``/``/``registry.npm.taobao.org；安装脚手架npm install ``-``g @vue``/``cli；版本2：npm install ``-``g @vue``/``cli；执行vue -V验证安装是否成功
- 安装grunt

```js
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm install -g grunt-cli
```

- 安装elasticsearch-head：[https://github.com/mobz/elasticsearch-head](https://github.com/mobz/elasticsearch-head)下载解压；cmd终端进入elasticsearch-head-master目录，执行npm install，完成之后启动npm run start，访问localhost:9100

`es默认不允许跨域连接，若想实现跨域，进入elasticsearch的config目录下修改文件elasticsearch.yml：末尾添加 http.cors.enabled: true
　　　　 http.cors.allow-origin: "*" 然后再重启`

### 3. ElasticSearch语法学习

