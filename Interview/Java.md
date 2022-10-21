# Java八股文

[toc]

## 基本概念

### 三大特性

java三大特性（面向对象编程三大特性）：继承，封装，多态。

### String和StringBuffer

-  String是一个不可变的字符序列

- StringBuffer是一个可变的字符序列，StringBuffer 和 StringBuilder 类的对象能够被多次的修改，并且不产生新的未使用对象

* 无参构造方法，String为空字符初始容量为0，StringBuffer初始容量为16
* StringBuffer：可变字符串、效率低、线程安全；
* StringBuilder：可变字符序列、效率高、线程不安全；

### Overload和Override

- 重载(overload)和覆盖(override)是java多态性的两种不同表现方式 。

- 覆盖(Overriding)是父类与子类之间多态性的一种表现，重载(Overloading)是一个类中多态性的一种表现 。

| 区别点   | 覆盖     | 重载                     |
| -------- | -------- | ------------------------ |
| 参数列表 | 必须不同 | 必须相同                 |
| 返回类型 | 无限制   | 必须相同                 |
| 异常     | 可以修改 | 异常只能减少或删除       |
| 访问权限 | 可以修改 | 不可以降低方法的访问权限 |

### &和&&的区别

`int a = 2;  1>2? && a+1>2?`      该表达式不会判定a+1>2

`int a = 2;  1>2? & a+1>2?`        判定了1>2为假 ，仍会判定a+1>2为真

```
&和&&都可以用作逻辑与的运算符，表示逻辑与（and），当运算符两边的表达式的结果都为true时，整个运算结果才为true，否则，只要有一方为false，则结果为false。
  
&&还具有短路的功能，即如果第一个表达式为false，则不再计算第二个表达式。

&还可以用作位运算符，当&操作符两边的表达式不是boolean类型时，&表示按位与操作。
```

### BeanFactory和ApplicationContext的区别

- ApplicationContext继承BeanFactory接口，它是Spring的一个更高级的容器。
- BeanFactory是Spring里面最底层的接口（最原始的接口），包含了各种Bean的定义，读取bean配置文档，管理bean的加载、实例化，控制bean的生命周期，维护bean之间的依赖关系。
- BeanFactory在启动的时候不会去实例化Bean，中有从容器中拿Bean的时候才会去实例化；
- ApplicationContext在启动的时候就把所有的Bean全部实例化了。
- ApplicationContext还可以为Bean配置lazy-init=true来让Bean延迟实例化；

### final关键字

　　1、final可以修饰类，方法和变量

　　2、final修饰的类，不能被继承，即它不能拥有自己的子类

　　3、final修饰的方法，不能被重写

　　4、final修饰的变量，无论是类属性、对象属性、形参还是局部变量，都需要进行初始化操作。　

### 匿名内部类

**匿名内部类**（Anonymous Inner Class）：是一种没有类名的内部类，不使用关键字class、extends和implements，没有构造方法，它必须继承其他类或实现其他接口。匿名内部类的好处一般是代码更加简洁、紧凑，但带来的问题是易读性下降。

 假设我们有一个接口A ，内部有一个未被实现的方法eat，如果我们想在main中直接调用eat方法 ，则按照传统思路需要一个类B来实现接口A，同时再创建类B的对象来调用A，代码如下：

```java
public class Interface01 {
    public static void main(String[] args) {
        B b = new B();
        b.eat();
    }
}
interface A{
    public void eat();
}
class B implements A{
    @Override
    public void eat() {
        System.out.println("正在调用eat方法");
    }
}

```



**如果我们只是想单纯的使用一次eat方法，不需要创建对象的话，则上面方法略显古板。**

```java
public class Interface01 {
    public static void main(String[] args) {
        new A(){
            @Override
            public void eat() {
                System.out.println("正在调用eat方法");
            }
        }.eat();
    }
}
interface A{
    public void eat();
}
```



  1、匿名内部类中是不能定义构造函数的。

  2、匿名内部类中不能存在任何的静态成员变量和静态方法。

  3、匿名内部类为局部内部类，所以局部内部类的所有限制同样对匿名内部类生效。

  4、匿名内部类不能是抽象的，它必须要实现继承的类或者实现的接口的所有抽象方法



### Session和Cookie

1. 数据存储位置：cookie数据存放在客户的浏览器上，session数据放在服务器上。

2. 安全性：cookie不是很安全，别人可以分析存放在本地的cookie并进行 [ cookie 欺骗 ](./网络安全.md##Cookie欺骗)

3. 服务器性能：session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能，考虑到减轻服务器性能方面，应当使用cookie。

4. 数据大小：单个cookie保存的数据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie。

5. 信息重要程度：可以考虑将登陆信息等重要信息存放为session，其他需要保留信息可以放在cookie中。

   

### Spring框架中设计模式

- 代理模式：在AOP和remoting中被用的比较多。
- 单例模式：在spring配置文件中定义的bean默认为单例模式。
- 模板方法模式：用来解决代码重复的问题。
- 前端控制器模式：Spring提供了DispatcherServlet来对请求进行分发。
- 依赖注入模式：贯穿于BeanFactory / ApplicationContext接口的核心理念。
- 工厂模式：BeanFactory用来创建对象的实例。

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