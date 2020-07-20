# 疑问

### 1. 为什么main.js中`import router from './router'`直接导入的是index.js文件

`答`：这个不是vue的规定而是node加载模块的方式，当require("./router")(import会被转化为require)，node是这样寻找目标的：

* 首先寻找目录下有没有router.js或者router.node，如果有就导入
* 如果没有就看是否有router目录，如果没有就require失败，抛出异常"Cannot find module './router'"
* 如果有router目录会在其下寻找package.json文件，如果有则按照package的配置来导入
* 如果没有package.json，看是否有index.js或者index.node，如果有就导入没有就失败

