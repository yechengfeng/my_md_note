## 一、Spring的引言

spring 春天      2002年      罗德·约翰森创作

定义：Spring框架是一个`集众多设计模式（工厂模式、代理模式、策略模式、单例模式……）`于一身的`开源的`、`轻量级`的`项目管理`框架。致力于JAVAEE`轻量级解决方案`

`轻量级解决方案：提供一个简单的、统一的、高效的方式构造整个应用，并且可以将单层框架以最佳的组合揉合在一起建立一个连贯体系。`

struts2 + Spring + mybatis

特点：Spring框架不再是替换项目中某个技术，而是将项目中使用单层框架进行 整合|管理|揉合

Spring框架具体在项目中核心使用

Spring `项目管理框架：就是用来对现有项目中组件进行管理（创建 使用 销毁）`

​												 用来负责项目中组件对象的创建 使用 销毁

spring框架主要管理action、service、dao，而entity组件通常不交给spring进行管理

## 二、Spring的第一个程序

#### 1. 引入spring框架相关依赖

注意：引入spring核心模块以及依赖模块

> - spring-core  核心依赖
>
> - spring-beans
>
> - spring-web
>
> - spring-expression
>
> - spring-aop
>
> - spring-context
>
> - spring-context-support
>
> - spring-aspects
>
> - spring-jdbc

#### 2. 引入spring框架配置文件

`配置文件`： 名字随便  位置随便（本项目中resources目录里面）

​						  applicationContext.xml  |  spring.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

</beans>
```

#### 3. 通过spring管理组件

```xml
<!--通过spring管理组件，
    beans:用来管理组件对象的创建
    class:用来指定管理组件对象的全限定名  包.类
    id:用来指定spring框架创建的当前组件对象在spring(容器|工厂)中唯一标识  全局唯一
-->
<bean class="com.study.UserDaoImpl" id="userDaoImpl"></bean>
```

#### 4. 启动工厂，获取对象进行测试

```java
ApplicationContext context = new ClassPathXmlApplicationContext("com/study/spring.xml");
UserDao userDao = (UserDao) context.getBean("userDaoImpl");
System.out.println(userDao);
userDao.save("houchangchang");
```



## 三、Spring框架中的核心思想之一IOC

spring框架中的核心思想： `IOC思想（控制反转）、AOP思想（面向切面编程）`

#### 1. IOC

​	Inversion of Control 控制反转

​	定义：所谓控制反转其实指的是控制权力的反转

​	通俗定义：`就是将原来手动通过new关键字创建对象的权力交给spring，通过在配置文件中配置bean标签形式创建对象`，交给spring由spring创建对象的过程就叫控制反转。

#### 2. DI

​	Dependency Injection 依赖注入

#####  1）定义

​	为组件中成员变量完成赋值过程，这个过程就称之为依赖注入

##### 2）注入方式

###### `方式1-set方法注入`

​			A）组件对象中需要哪个组件 就将哪个组件声明为成员变量并提供公开的SET方法

​			B）在spring的配置文件中对应的组件标签内使用property标签去完成属性的赋值操作

注入语法：

```java
Dao层组件
public class DeptDaoImpl implements DeptDao {
    @Override
    public void save(String name) {
        System.out.println("Dao层的name: " + name);
    }
}

Service层组件
public class DeptServiceImpl implements DeptService {
  	//需要DAO层组件对象 依赖DAO组件	
    private DeptDao deptDao;
    public void setDeptDao(DeptDao deptDao) {
        this.deptDao = deptDao;
    }
    @Override
    public void save(String name) {
        deptDao.save(name);
        System.out.println("Service层的name: " + name);
    }
}

配置文件赋值：
<!--管理DAO组件-->
<bean class="com.di.DeptDaoImpl" id="aa"></bean>
<!--管理Service组件-->
<bean class="com.di.DeptServiceImpl" id="deptService">
    <!--依赖的注入
        property: 用来给组件中的属性进行复制操作
        name:     用来指定给组件中哪个属性进行赋值
        ref:      用来指定赋值对象在工厂中唯一标识
    -->
    <property name="deptDao" ref="aa" />
</bean>
          
启动工厂测试
ApplicationContext context = new ClassPathXmlApplicationContext("com/di/spring.xml");
DeptService deptService = (DeptService) context.getBean("deptService");
deptService.save("百知教育");
```

###### `方式2-构造方法注入`

​		使用类中构造方法为类中成员变量赋值过程，称之为构造注入	

​			A）需要哪个组件属性就将哪个组件属性声明为成员变量，并提供公开构造方法

​			B）在配置文件中对应的组件标签内部使用<constructor-args>标签进行注入

注入语法：

```xml
<bean class="com.cid.EmpDaoImpl" id="EmpDaoImpl">
    <!--管理DAO组件
        1.set注入，使用的是property标签
				2.构造方法注入，使用的是constructor-arg标签
		-->
		<constructor-arg index="0" name="name" value="张三"/>
		<constructor-arg index="1" name="age" value="23"/>
		<constructor-arg index="2" name="bir" value="2020/05/06"/>
		<constructor-arg index="3" name="arr">
				<array>
						<value>cat</value>
						<value>dog</value>
						<value>duck</value>
				</array>
		</constructor-arg>
		<constructor-arg index="4" name="list">
				<list>
						<value>football</value>
						<value>pingpang</value>
						<value>basketball</value>
				</list>
		</constructor-arg>
</bean>
```

###### `方式3-autowire自动注入`

在spring工厂配置文件中通过制定自动注入方式 开启组件属性的自动赋值

	​	注意：
	
	- 底层使用原理也是SET方式注入
	- 自动注入需要在对应组件标签开启才能使用
	- 只能用于引用类型的注入|对象类型|组件类型的注入

自动注入语法：

>- 需要谁就将谁声明为成员变量，并提供SET方法
>
>- 在对应组件标签中加入`autowire`属性并指定自动注入方式

注入实例：

```xml
<!--管理DAO组件-->
<bean class="com.aid.StudentDaoImpl" id="studentDao"></bean>
<!--管理Service组件
    autowire: 用来给组件中成员变量完成自动赋值操作
    byType: 根本类型完成自动注入 根据成员变量类型去工厂找 找到对应类型完成赋值 找不到就不赋值
            注意：如果工厂中存在多个类型一致的组件，使用类型自动注入会报错
    byName: 根据名称完成自动注入 根据成员变量名称去工厂中获取与之一致名字，找到赋值 找不到不赋值
-->
<bean class="com.aid.StudentServiceImpl" id="studentService" autowire="byName"></bean>
```



`IOC总结`：控制反转，就是将原来手动通过new关键字创建对象的权力交给spring，由spring工厂创建对象过程，当然spring不仅要创建对象还要在创建对象的同时通过DI的方式维护组件与组件之间的调用关系。



​		  