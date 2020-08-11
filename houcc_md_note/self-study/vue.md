# 疑问

### 1. 为什么main.js中`import router from './router'`直接导入的是index.js文件

`答`：这个不是vue的规定而是node加载模块的方式，当require("./router")(import会被转化为require)，node是这样寻找目标的：

* 首先寻找目录下有没有router.js或者router.node，如果有就导入
* 如果没有就看是否有router目录，如果没有就require失败，抛出异常"Cannot find module './router'"
* 如果有router目录会在其下寻找package.json文件，如果有则按照package的配置来导入
* 如果没有package.json，看是否有index.js或者index.node，如果有就导入没有就失败

# Vue实战

## 1. Vue引言

> `渐进式`JavaScript框架 --摘自官网

```markdown
# 渐进式
   1.易用  html css JavaScript
   2.高效  开发前端页面 非常高效
   3.灵活  开发灵活 多样性
   
# 总结
	Vue 是一个JavaScript框架
	
# 后端服务端开发人员：
	Vue渐进式JavaScript框架：让我们通过操作很少的DOM，甚至不需要操作页面中任何DOM元素，就很容易完成数据和视图绑定  双向绑定 MVVM
	
	注意：日后在使用Vue过程中不需要引入JQuery框架
	
	htmlcss → javascript → jquery → angularjs → Vue

# Vue作者
	尤雨溪 国内的
```

## 2. Vue入门

### 2.1 下载Vuejs

```js
//开发版本
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

//生产版本
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

### 2.2 Vue第一个入门应用

 ```html
<div id="app">
    {{msg}}  {{username}}  {{pwd}}
    <br/>
    <span>
        {{username}}
        <h1>{{pwd}}</h1>
    </span>
</div>

<!--引入vue.js-->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    const app = new Vue({
        el: "#app", //element 用来给Vue实例定义一个作用范围
        data: {     //用来给Vue实例定义一些相关数据
            msg: "百知欢迎你，期待你的加入！",
            username: "hello, Vue!",
            pwd: "12345"
        }
    });
</script>
 ```

```markdown
# 总结：
	1.vue实例（对象）中el属性：代表Vue的作用范围 日后在Vue的作用范围内都可以使用Vue的语法
	2.vue实例（对象）中data属性：用来给Vue实例绑定提供一些相关数据，绑定的数据可以通过{{变量名}}在Vue作用范围内取出
	3.在使用{{}}进行获取data中数据时，可以在{{}}中书写表达式、运算符、调用相关方法以及逻辑运算等
	4.el属性中可以书写任意的CSS选择器[JQuery选择器]，但是在使用Vue开发时推荐使用id选择器
```

## 3. v-text和v-html

### 3.1 v-text

> `v-text`: 用来获取data中数据将数据以文本形式渲染到指定标签内部 类似于JavaScript中的innerText

```html
<div id="app">
    <span>{{message}},我们期待您的加入</span>
	<br/>
    <span v-text="message + '!'"></span>,我们期待您的加入
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    const app = new Vue({
        el: "#app",
        data: {
            message: "百知欢迎您"
        }
    });
</script>
```

```markdown
# 总结
	1.{{}}(插值表达式)和v-text获取数据的区别在于 
		a.使用v-text取值会将标签中原有的数据覆盖，使用插值表达式不会覆盖标签原有的数据
		b.使用v-text可以避免在网络环境较差的情况下出现插值闪烁
```

### 3.2 v-html

> `v-html`:用来获取data中数据将数据中含有的html标签先解析再渲染到指定标签内部 类似于JavaScript中的innerHTML

```html
<div id="app">
    <span>{{message}},我们期待您的加入</span>
	<br/>
    <span v-text="message + '!'"></span>,我们期待您的加入
	<br/>
    <span v-html="message + '!'"></span>,我们期待您的加入
</div>

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
    const app = new Vue({
        el: "#app",
        data: {
            message: "<a href=''>百知教育</a>欢迎您"
        }
    });
</script>
```

## 4. Vue中事件绑定（v-on）

### 4.1 绑定事件语法

```js
	<div id="app">
        <h3>{{message}}</h3>
        <h3 v-text="message"></h3>
        <h3 v-html="message"></h3>
        <h3>年龄：{{age}}</h3>

        <input type="button" value="点我改变年龄" v-on:click="changeAge">
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        const app = new Vue({
            el: "#app",
            data: {
                message: "hello,欢迎来到百知课堂！",
                age: 23
            },
            methods: {   //method: 用来定义Vue中事件
                changeAge:function() {
                    this.age++;
                    alert("事件触发");
                }
            }
        });
    </script>
```

```markdown
# 总结：
	事件三要素 1)事件源：发生事件dom元素 2)事件：发生特定的动作，如click…… 3)监听器：发生特定动作之后的事件处理程序，通常是js中函数
	1.在Vue中绑定事件是通过v-on指令完成的 v-on:事件名 如 v-on:click
	2.在v-on:事件名的赋值语句是当前事件触发调用的函数名
	3.在vue中事件的函数统一定义在Vue实例的methods属性中
	4.在vue的事件中this指的就是当前的Vue实例，日后可以在事件中通过使用this获取Vue实例中相关数据
```

```html
	<div id="app">
        <h2>{{age}}</h2>
        <input type="button" value="通过v-on事件修改年龄：每次+1" v-on:click="changeAge">
        <input type="button" value="通过@绑定事件修改年龄：每次-1" @click="changeAgeTwo">
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        const app = new Vue({
            el: "#app",     //element: 用来指定vue作用范围
            data: {         //data   : 用来定义vue实例中相关数据
                age: 23
            },
            methods: {      //methods: 用来定义事件的处理函数
                changeAge:function () {
                    this.age++;
                },
                changeAgeTwo:function () {
                    this.age--;
                }
            }
        });
    </script>
```

```markdown
# 总结：
	1.日后在vue中绑定事件时可以通过@符号形式 简化v-on的事件绑定
```

