# Java八股文

[toc]

## 基本概念

### 三大特性

java三大特性（面向对象编程三大特性）：继承，封装，多态。

### String和StringBuffer

-  String是一个不可变的字符序列

- StringBuffer是一个可变的字符序列，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象

* 无参构造方法，Sting为空字符初始容量为0，StringBuffer初始容量为16
* 如果要操作少量的数据用 String；
* 多线程操作字符串缓冲区下操作大量数据 StringBuffer；
* 单线程操作字符串缓冲区下操作大量数据 StringBuilder。

### Overload和Override

```
    Overload是重载的意思，Override是覆盖的意思，也就是重写。
    重载Overload：在同一个类中，允许存在一个以上的同名函数，只要他们的参数个数或者参数类型不同即可。
    重载的特点：与返回值类型无关，只看参数列表
```



### &和&&的区别

```
&和&&都可以用作逻辑与的运算符，表示逻辑与（and），当运算符两边的表达式的结果都为true时，整个运算结果才为true，否则，只要有一方为false，则结果为false。
  
&&还具有短路的功能，即如果第一个表达式为false，则不再计算第二个表达式。

&还可以用作位运算符，当&操作符两边的表达式不是boolean类型时，&表示按位与操作。
```

### Spring框架中设计模式

- 代理模式：在AOP和remoting中被用的比较多。
- 单例模式：在spring配置文件中定义的bean默认为单例模式。
- 模板方法模式：用来解决代码重复的问题。
- 前端控制器模式：Spring提供了DispatcherServlet来对请求进行分发。
- 依赖注入模式：贯穿于BeanFactory / ApplicationContext接口的核心理念。
- 工厂模式：BeanFactory用来创建对象的实例。

### BeanFactory和ApplicationContext的区别

```
BeanFactory在启动的时候不会去实例化Bean，中有从容器中拿Bean的时候才会去实例化；
BeanFactory是Spring里面最低层的接口，提供了最简单的容器的功能，只提供了实例化对象和拿对象的功能；


ApplicationContext在启动的时候就把所有的Bean全部实例化了。
ApplicationContext还可以为Bean配置lazy-init=true来让Bean延迟实例化；
ApplicationContext继承BeanFactory接口，它是Spring的一个更高级的容器。
```

### Spring的核心模块

```

Spring Core【核心容器】：核心容器提供了Spring的基本功能。核心容器的核心功能是用IOC容器来管理类的依赖关系。

Spring AOP【面向切面】：Spring的AOP模块提供了面向切面编程的支持。SpringAOP采用的是纯Java实现，采用基于代理的AOP实现方案，AOP代理由IOC容器负责生成、管理，依赖关系也一并由IOC容器管理。

Spring ORM【对象实体映射】：提供了与多个第三方持久层框架的良好整合。

Spring DAO【持久层模块】： Spring进一步简化DAO开发步骤，能以一致的方式使用数据库访问技术，用统一的方式调用事务管理，避免具体的实现侵入业务逻辑层的代码中。

Spring Context【应用上下文】：它是一个配置文件，为Spring提供上下文信息，提供了框架式的对象访问方法。

Spring Web【Web模块】：提供了基础的针对Web开发的集成特性。

Spring MVC【MVC模块】：提供了Web应用的MVC实现。Spring的MVC框架并不是仅仅提供一种传统的实现，它提供了一种清晰的分离模型。
```