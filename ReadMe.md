

[TOC]

# 初级面试题（很少会问，但是作为一个合格的程序员应该所有都会）

### String和StringBuilder和StringBuffer区别

- String：底层是final修饰的数组。字符串的**长度不可改变，不适用字符串拼接**
- StringBuilder：**可变字符串**，线程**不安全**的，相对于StringBuffer有速度优势，性能更高。适用于字符串拼接
- StringBuffer：可变字符串，线程**安全**，因为方法有同步锁synchronized，相对于StringBuilder性能低



### ArrayList和LinkedList区别，你一般用哪一个，为什么

- ArrayList：底层基于数组实现，内存分配要求连续性。修改查询性能高，随机取元素(根据索引)速度快。但是增删会涉及到移位操作，性能差

- LinkedList：底层基于链表实现，增加删除性能高。内存分配不要求连续，增删元素不涉及到移位操作，性能高，但是查找元素需要从前往后遍历，所以性能低

  根据场景使用，如果查询修改的居多使用ArrayList  如果增加删除的居多用LinkedList



### 创建线程是几种方式

- 继承Thread类创建线程类

  - 定义Thread类的子类，并重写该类的run方法，该run方法的方法体就代表了线程要完成的任务。因此把run()方法称为执行体
  - 创建Thread子类的实例，即创建了线程对象。
  - 调用线程对象的start()方法来启动该线程。

- 通过实现Runnable接口创建线程类

  - 定义runnable接口的实现类，并重写该接口的run()方法
  - 调用线程对象的start()方法来启动该线程。

- 通过实现Callable接口和Future创建线程

  - 创建Callable接口的实现类，并实现call()方法，该call()方法将作为线程执行体，**并且有返回值**。
  - 创建Callable实现类的实例，使用FutureTask类来包装Callable对象，该FutureTask对象封装了该Callable对象的call()方法的返回值。
  - 使用FutureTask对象作为Thread对象的target创建并启动新线程。
  - 调用FutureTask对象的get()方法来获得子线程执行结束后的返回值

  ​		

### 直接调用线程的start方法和run方法有什么区别

- 启动一个线程需要调用 Thread 对象的 start() 方法。调用线程的 start() 方法后，**创建一个新的线程线程处于可运行状态，此时它可以由 JVM 调度并执行，这并不意味着线程就会立即运行**
- run() 方法是线程运行时由 JVM 回调的方法，无需手动写代码调用，**直接调用线程的 run() 方法，相当于在调用线程里继续调用方法，并未启动一个新的线程**

### mavn的打包和安装用什么命令

- 打包命名：mvn package

- 安装命名：mvn install

### ArrayList和vector区别

- 同步性

  - **Vector是线程安全的**，也就是说是它的方法之间是线程同步的，而**ArrayList是线程序不安全的**，它                    

    的方法之间是线程不同步的。如果只有一个线程会访问到集合，那最好是使用ArrayList，因为它不考虑线程                 

    安全，效率会高些；如果有多个线程会访问到集合，那最好是使用Vector，因为不需要我们自己再去考虑和编                  

    写线程安全的代码。

- 数据增长

  - ArrayList与Vector都有一个**初始的容量大小**，当存储进它们里面的元素的个数超过了容量时，就需                

    要增加ArrayList与Vector的存储空间，每次要增加存储空间时，不是只增加一个存储单元，而是增加多个存                      

    储单元，每次增加的存储单元的个数在内存空间利用与程序效率之间要取得一定的平衡。**Vector默认增长为原**                              

    **来2倍**，而**ArrayList的增长策略在文档中没有明确规定（从源代码看到的是增长为原来的1倍）**。                          

    **ArrayList与Vector都可以设置初始的空间大小，Vector还可以设置增长的空间大小，而ArrayList没有提**              

    **供设置增长空间的方法**。

### 说一下面向对象的几大特征

- 封装
  - 封装的目的是增强安全性和简化编程，使用者不必了解具体的实现细节，而只是要通过外部接口，以特定的访问权限来使用类的成员
- 继承
  - **继承就是子类继承父类的特征和行为**
  - 只能单继承（只能有一个父亲），可以多重继承（子类继承父类，父类还可以继承它的父类）
- 多态
  - 多态同一个行为具有多个不同表现形式或形态的能力。是指一个类实例（对象）的相同方法在不同情形有不同表现形式
  - 优点：
    - 消除类型之间的耦合关系
    - 可替换性
    - 可扩充性
    - 接口性
    - 灵活性
    - 简化性

### 接口和抽象类区别

- 接口
  - 接口是抽象方法和常量值定义的集合，而没有属性和方法的实现,用interface修饰的类
- 抽象类
  - 抽象类是含有抽象方法（只有声明而没有实现的方法）且用abstract修饰的类
- 相同点
  - 都不能被实例化
  - 都能包含抽象方法
- 不同点
  - 在抽象类中**可以写非抽象的方法，也可以声明构造方法，需要子类实例化**；**接口中的方法全是抽象方法**，**不能声明构造方法**。
  - **一个类只能继承一个直接类**，这个父类可以是抽象类，但是**一个类可以实现多个接口**
  - **抽象类可以声明成员变量**，子类可以对该成员变量赋值，**接口中只能声明常量**，**实现接口的类必须对所有的抽象方法进行覆盖**。



### Equals和==的区别

- Equals：比较的**两个类型的值是否相等**，用在引用数据类型。比较是基于他们在内存中的存放位置的地址值的。
- ==：判断两个值是否相等，用在基本数据类型比较。如果要用在引用数据类型上**比较的就只是两个对象在内存中存放的地址**。所以，除非是同一个new出来的对象，他们的比较后的结果为true，否则比较后结果为false。

### int 和 Integer的区别

- int是基本数据类型的一种，整数类型。

- Integer是int的包装类

- Interger变量必须实例化才能使用，而int不用

- Integer实际是对象的引用，当new一个Integer时，实际上是生成一个指针指向此对象；而int则是直接存储数据值 

- Integer的默认值是null，int的默认值是0

  

### 说一下多表JOIN查询，完整查询SQ中的关键字的定义顺序（SELECT ,FROM JOIN等关键字的编写顺序）

编写顺序：

​	**[SELECT]()**  字段1，字段2  [**FROM**]()  表1 [**AS**]()  别名  **[JOIN]()** 表2 [**AS**]() 别名  [**ON**]()  表1别名.外键 [**=**]() 表2别名.主键 [**WHERE**]() 条件判断



### MyBatis结果集映射，如果是单个关联对象用什么映射,如果是一个集合的查询用什么映射

- 单表查询使用**`association`**和**`javaType`**组合    多对一


- ​	集合查询**`collection`**和**`ofType`**组合    一对多

  

### 多表查询，使用JOIN查询和额外SQL方式查询有什么区别，和优缺点

- JOIN查询只会发送一条sql语句，查询一次
  - 优点，减少数据库消耗，性能更高
  
- 额外SQL方式会发送N+1条sql语句
  - 缺点数据库消耗比较大，加大数据库压力从而影响性能
  
    

### Mybatis中 ${}取值和#{}取值的区别

- #{}取值实质上是会生成？占位符，防止sql注入问题

- ${}取值是直接拼接字符串的，有sql注入问题

- #{}一般用在取值，动态传入值得时候

- ${}只会用在跟数据库的表名以及字段名。比如：要动态的查询某一个数据的字段或者数据库中的某一张表，就用${}

  

### Mybatis关联查询，延迟加载和饥饿加载的区别

饥饿加载也叫迫切加载，在关联查询的时候，会同时执行查询多张表的操作

延迟加载也叫懒加载，在关联查询的时候，排队查询，只有需求要查询操作的时候，我才会去操作



### Mybatis一级缓存和二级缓存的区别

- 一级缓存是默认开启的，二级缓存需要手动开启

- 一级缓存作用是在sqlsession范围内的，在同一个sqlsession中执行相同的sql语句时，会在sqlsession中去找，不会再第二次查询。如果中间执行了增删改操作，就会把一级缓存清空。**当关闭sqlsession的时候，一级缓存就不存在了**

- 二级缓存的作用域更大，执行相同的sql语句时，一级缓存会把数据给到二级缓存。**二级缓存是可以跨越多个sqlsession的**

  

### Mybatis的Mapper接口没有实现类为什么可以@Autowire直接注入

注入的是spring的JDK创建动态代理对象。在解析Mapper的时候，java通过反射获取Mapper接口的属于方法



### 说一下你对IOC的理解

IOC是Spring框架两个重要核心之一，IOC即控制反转，控制反转就是将类的创建，初始化，销毁等一系列工作交给Spring管理



### 说一下会对AOP的理解，AOP的使用场景，是什么，AOP的实现原理是什么

- AOP是Spring框架两个重要核心之一，AOP即面向切面编程，AOP是对OOP(面向对象编程)的一种扩展，即可以解决OOP不能解决的问题或者很难解决的问题。

- AOP可以用在事务管理，日志管理，性能监测

- 实现原理就是动态代理，动态代理分为JDK和CGLIB两种代理模式
  - JDK代理模式代理的是实现接口的实现类。默认
  
  - CGLIB代理模式：当没有实现接口，就继承，采用的就是CGLIB代理模式
  
    

### 说一下切面相关的注解，分别是什么意思

- @Aspect:用在类上面，告诉spring这是切面类

- @Pointcut:切点，告诉spring我要切入的是那一层，包的路径

- @Before:前置通知，在方法执行前执行。打在方法上声明

- @After:后置通知，不管方法执行成功与否，都要执行。打在方法上声明

- @AfteReturning:返回通知，当方法正常执行完毕返回的通知。打在方法上声明

- @AfterThrowing:异常通知，当方法执行的时候出现异常执行的通知，打在方法上声明

  

### Bean的四种注册方式

- 普通Bean注册  `<bean id="car" class="cn.itsource._04_bean.b_test.Car"> </bean>`

- 静态工厂模式：写一个静态方法返回当前对象`<!‐‐factory‐method：代表执行工厂中的方法,会把方法返回的对象设置成一个bean ‐‐>` 
  `<bean id="car" class="cn.itsource._04_bean.b_test.CarFactory" factory‐method="createCar"> </bean>`

  - ```java
    /**
     * 描述：静态工厂模式
     * @author:zmc
     **/
    public class CatFactory {
    
        public static Cat getCat(){
            return new Cat();
        }
    }
    
    ```

- 实例工厂模式：普通方法返回当前对象

  - `<!‐‐创建工厂对象‐‐>` 
    `<bean id="carFactory" class="cn.itsource._04_bean.c_test.CarFactory"> </bean>` 
    `<!‐‐调用对应工厂对象中的方法，返回一个bean对象‐‐>` 
    `<bean id="car" factory‐bean="carFactory" factory‐method="createCar" />`

  - ```java
    /**
     * 描述：实例工厂模式
     * @author:zmc
     **/
    public class CatFactory {
    
        public  Cat getCat(){
            return new Cat();
        }
    }
    ```

- 实现FactoryBean接口，覆写三个方法：返回bean的对象实例、返回bean的类型字节码、设置是否单例

  - `<!‐‐这里咱们配置的是一个FactoryBean Spring会为当前这个class对象创建一个bean对象出来 同时,还会创建一个对象 该对象的类型由 getObjectType 方法决定 该对象的值由 getObject 方法决定 而方法isSingleton确定它是否是单例 ‐‐>`
    `<bean id="car" class="cn.itsource._04_bean.d_test.CarFactoryBean"></bean>`

### 注册Bean的注解有哪些：比如@Controller

@Controller  @RestController

@Service

@SpringBootApplication

@Component

@Configuration



### 单例多例的区别

- 单例就是所有的请求都用一个对象来处理，比如我们常用的service和dao层的对象通常都是单例的

- 多例则指每个请求用一个新的对象来处理

  

### Spring的Bean被指定为prototype(原始模型模式)以及singleton(单例模式)有什么区别

- Spring创建Bean默认就是singleton(单例模式)

- 有状态的bean需要使用prototype模式，而对于无状态的bean一般采用singleton模式

- 每次调用bean的方法，prototype都会提供一个新的对象（重新new），并不保存原有的实例

- 而singleton不同，多次调用bean实际上使用的是同一个singleton对象，而且保存了对象的状态信息

  

### BeanFactory和ApplicationContext有什么区别 

- BeanFactory是spring的原始接口，位于类结构树的顶端，针对原始结构的实现类功能比较单一，BeanFactory接口实现的容器，特点是在**每次获取对象时才会创建对象**。

- 继承了BeanFactory接口，拥有BeanFactory的全部功能，并且扩展了很多高级特性，**每次容器启动时就会创建所有的对象**。

  

### BeanFactory和FactoryBean的区别

- BeanFactory是个Factory，也就是IOC容器或对象工厂。

- FactoryBean是个Bean。在Spring中，所有的Bean都是由BeanFactory(也就是IOC容器)来进行管理的，是]注册Bean注册方式之一

  

### 介绍一下Spring框架的组成

![img](https://img-blog.csdnimg.cn/png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zODI4MDU2OA==,size_16,color_FFFFFF,t_70)

- Core模块
  核心容器提供 Spring 框架的基本功能。核心容器的主要组件是 BeanFactory，它是工厂模式的实现。BeanFactory 使用控制反转 （IOC）模式将应用程序的配置和依赖性规范与实际的应用程序代码分开。

- Spring 上下文：
  Spring 上下文是一个配置文件，向 Spring 框架提供上下文信息。Spring 上下文包括企业服务，例如 JNDI、EJB、电子邮件、国际化、校验和调度功能。

- Spring AOP：
  通过配置管理特性，Spring AOP 模块直接将面向方面的编程功能集成到了 Spring 框架中。所以，可以很容易地使 Spring 框架管理的任何对象支持 AOP。Spring AOP 模块为基于 Spring 的应用程序中的对象提供了事务管理服务。通过使用 Spring AOP，不用依赖 EJB 组件，就可以将声明性事务管理集成到应用程序中。

- Spring DAO：
  JDBC DAO 抽象层提供了有意义的异常层次结构，可用该结构来管理异常处理和不同数据库供应商抛出的错误消息。异常层次结构简化了错误处理，并且极大地降低了需要编写的异常代码数量（例如打开和关闭连接）。Spring DAO 的面向 JDBC 的异常遵从通用的 DAO 异常层次结构。

- Spring ORM：
  Spring 框架插入了若干个 ORM 框架，从而提供了 ORM 的对象关系工具，其中包括 JDO、Hibernate 和 iBatis SQL Map。所有这些都遵从 Spring 的通用事务和 DAO 异常层次结构。

- Spring Web 模块：
  Web 上下文模块建立在应用程序上下文模块之上，为基于 Web 的应用程序提供了上下文。所以，Spring 框架支持与 Jakarta Struts 的集成。Web 模块还简化了处理多部分请求以及将请求参数绑定到域对象的工作。

- Spring MVC 框架



### Spring的Bean懒加载和非懒加载有什么区别 

- 懒加载：对象使用的时候才去创建。节省资源,但是不利于提前发现错误；

- 非懒加载：容器启动时立马创建。消耗资源,但有利于提前发现错误

  Spring 默认设置是非懒加载
  
  

### Spring的依赖注入方式有哪些？

- 构造器注入
  - 索引注入  index
  - 参数类型注入   type
  - 参数名注入  name
  
- setter方法注入

- 实现方式  xml和注解

  

### SpringBoot和Spring的区别

- SpringBoot是对Spring框架的扩展

- Spring需要配置繁琐的XML，SpringBoot不需要

- SpringBoot内置tomcat服务器

- SpringBoot简化大量代码，效率更快

  

### @SpringBootApplication注解的含义

开启SpringBoot启动的类。其主要包含三个注解：

- @SpringBootConfiguration 配置标签， @Configuration 注解演化而来的，如同Spring的xml配置文件

- @EnableAutoConfiguration  开启自动配置标签  视图解析器，前端控制器等等

- @ComponentScan  开启IOC自动扫描当前包和当前包的子包

  

### spring-boot-starter-parent的作用

SpringBoot的父级依赖，管理了很多的基础jar包，使用它以后在导入依赖是可以省略版本**version信息**



### spring-boot-starter-web的作用

SpringBoot和SpringMvc整合的jar包，并且导入了日志，tomcat,等等相关的jar包



### SpringBoot中如何读取配置(2种方式)

- 在字段上加上@Value标签     @Value("${username}")
- 通过一个类来接收 。@ConfigurationProperties(prefix = "user")   读取配置文件的第二种方式，prefix = "user"：前缀

### 日志的leavel有哪些？

级别依次是：

- TRACE
- DEBUG 
- INFO      默认
- WARN
- ERROR

### SpringBoot中如何管理事务

- 在`@springBootApplication`的启动类上加上注解`@EnableTransactionManagement`    在工程允许事务的开启
- 在具体实现事务的类上打上注解`@Transaction`一般在service的实现类上注解

### 什么是RBAC ， 相关表怎么设计的？

- RBAC（Role-Based Access Control）权限模型的概念，即：基于角色的权限控制。通过角色关联用户，角色关联权限的方式间接赋予用户权限。
- 在用户与角色之间建立中间表，在角色与权限之间建立中间表，总共5张表

### 在VUE中，什么是MVVM

- M   model  模型，包括数据和一些基本操作
- v    view 视图，页面渲染结果
- vm   view-model 视图和模型双向绑定，模型与视图间的双向操作（无需开发人员干涉）

### 讲几个VUE的指令

- v-if   判断指令
- v-text  填充文本
- v-html 填充文本  与v-text不同的是  v-html会解析文本内容的html标签，而v-text只会当做字符换
- v-bind    将data中的数据绑定到标签上,作为标签的属性.
- v-model   双向绑定  v-model只作用于以下表单: input  select textarea
- v-for  循环遍历
- v-show  为true时就显示内容

### Node你们用的哪个版本，vue你们用的哪个版本，npm你们用的哪个版本

- node-v0-x64
- NPM：管理JS库

### 前后端分离的好处

- 同步开发，提高开发效率
- 前端人员开发前端，后端人员开发后端，责任分明
- 降低维护成本，客户端的问题不需要后台人员参与调试，代码重构和可维护性增强
- 实现高内聚低耦合，减少后端（应用）服务器的并发/负载压力
- 即使后台服务器暂时宕机了，前端页面也可以正常访问，只是无法提供数据

### 你们这个前后端分离项目是怎么部署的

- 前后端分离，前端使用nginx部署
- 后端使用基于SpringBoot的内嵌tomcat部署
- 分开部署通过代理解决前后端域名不一致的问题

### 你们这个前后端分离项目的技术栈是怎么样的

- 前端门户网站：HTML+JQuery+css
- 前端管理网站：VUE+ElementUi
- 后端：基于SpringBoot的SSM框架   SpringBoot+SpringMvc+Mybatis

### 讲一下你用过ElementUI的哪些组件

- button  按钮
- icon   图标
- form  表单   单元框radio  输入框input  多选框Checkbox  选择器  select   级联选择器 Cascader
- 其他组件：对话框Dialog   消息提示Message  

### 你们用什么做项目代码管理的

- Git

### 讲讲Git相对于SVN的区别

- Git在每一个工程师的本地是有一个本地仓库    
- Git在每个工程只产生一个.git目录,而SVN会在每个目录下都生成.svn目录
- Git能快速切换分支，且合并文件的速度比SVN快
- Git采用分布式版本库，内容完整性更好

### 讲几个Git的命令

- git clone   克隆远程仓库到本地仓库
- git add  添加代码到本地仓库
- git commit  提交add后的代码到本地仓库
- git  push  推送到远程仓库
- git  pull 拉取远程仓库

### 讲一下你理解的Redis，为什么Redis很快

- Redis相比Mysql快的原因是Redis是存储在内存中的，读取速度更快
- Redis结构简单
- 采用多路IO复用模型，减少网络IO的时间消耗，避免大量的无用操作，所以速度快
- 单线程避免了线程切换和上下文切换产生的消耗，所以速度快

### 你常用的Redis的数据存储结构有哪些，他们的使用场景分别是什么

- String   缓存，计数器，防攻击，验证码、登录过期
- List   队列  秒杀  
- set    去重
- zset  
- hash

### 每种存储结构说 4 个命令吧

- String

  ​	set key value	设置值

  ​	get key			   取值

  ​    mset key value key value...	设置多个值

  ​	mget key key	获取多个值

  ​	incr key	将key中的值自增1

  ​	decre key	将key中的值自减1

- List

  ​	lpush key value value...	从最左边设置值

  ​	rpush key value value...	从最右边设置值

  ​	lrange key start stop	查询key中指定区间的元素

  ​	lpop key	移出并返回key中最左边的元素

  ​	rpop key	移出并返回key中最右边的元素

- Set

  ​	sadd key value value	添加元素

  ​	smembers key	返回集合key中的所有元素

  ​	srem key member	删除集合key中member元素

  ​	scard key	查询集合key中的元素数量

- ZSet

  ​	zadd key score value (score value)...	添加元素

  ​	zcard key	查询集合key中元素数量

  ​	zcount key min max	返回有序集合key中score 在min和max之间的元素

  ​	zrange key start stop	返回有序集合key中索引在start和stop之间的元素

- Hash

  ​	hset key field value	添加元素

  ​	hget key field	获取key集合中field键对应的值

  ​	hmset key field value (field value)...	添加元素并批量添加子键值对

  ​	hmget key field field	获取key集合中所有的子键值对



### 怎么防止Redis宕机数据丢失问题

- Redis的持久化把内存中的数据集合命令保存到磁盘中做备份，当Redis出现宕机的情况，重启服务器，Redis会在磁盘中加载备份的数据

### Redis持久化是什么？有几种方式

- RDB  保存数据集       
- AOF  保存Redis的命令

### Redis有了AOF持久化为什么还要RDB？

- AOF记录命令的，优点格式清晰，容易理解   数据更安全，采用append模式即使宕机，也不会影响已经保存的数据   缺点数据文件体积大，恢复速度慢
- RDO记录数据集的，有点体积小，恢复速度快，备份方便。缺点是没办法做到数据的百分之百的不丢失，因为它是每隔一段时间保存备份一次数据的。

### Redis内存不够了怎么办？

- 增加物理内存
- 开启淘汰策略，淘汰不常用的一些数据删除老的数据

### 淘汰策略有哪些？

- volatile-lru ：从已设置过期时间的数据集中挑选最近最少使用的数据淘汰
- volatile-ttl：从已设置过期时间的数据集中挑选将要过期的数据淘汰
- volatile-random：从已设置过期时间的数据集中任意选择数据淘汰
- allkeys-lru：从数据集中挑选最近最少使用的数据淘汰
- allkeys-random：从数据集中任意选择数据淘汰
- no-enviction：不使用淘汰

### Redis事务和Mysql事务的区别

- Mysql事务支持原子性，要么同时成功要么同时失败   Redis事务不满足原子性
- Mysql是基于日志，记录修改数据前后状态实现的，Redis事务是基于队列实现的

### 使用Redis如何实现消息广播

- 发布订阅 
- 订阅者通过 SUBSCRIBE channel命令订阅某个频道
- 发布者通过 PUBLISH channel message向该频道发布消息，该频道的所有订阅者都可以收到消息



### 讲一下Session的工作原理

- 当客户端发送一次请求的时候，服务端会保存一个Session,同时生成一个SessionId  服务端再将这个SessionId返回给客户端
- 客户端拿到SessionId会存储在cookie中，每次请求后台的时候就会携带这个SessionId到后台
- 服务端收到这个SessionId就能找到对应的Session数据



### 三方登录流程讲一下

- 用户发起登录请求，后台获取拉起二维码界面重定向到前端
- 用户扫码授权，后台拼接获取授权码的url，并将回调的授权码信息作为参数交给前端去处理
- 前端携带授权码再次向后台发起请求，后台根据授权码拼接获取token的url,拿到用户的openId
- 根据openId去数据库的微信用户表查询
  - 如果微信用户表中没有这个用户信息，就向微信平台发起获取用户信息请求，拿到微信用户的信息保存在微信用户表中，再重定向到前端到绑定页面。
  - 如果微信用户表中有这个用户信息，但是没有绑定本地账号的电话号码，返回给前端到绑定页面
- 如果openId在数据库的微信用户表中有该用户的信息并且电话也绑定了，就默认走登录流程
- 前端用户输入了绑定手机号后，发起请求，后台先进行判断，根据电话号码去查询本地用户表，如果这个电话号码存在，就将本地的用户表和微信用户表进行绑定，最后走登录流程
- 如果手机号在本地用户表中没有手机号信息，那就先把手机号保存到本地用户表，返回ID，最后再跟微信用户表保存起来。最后走登录流程

### Oauth2的优势

- 相比Oauth1来说删除了繁琐的加密算法，利用https传输协议对认证的安全性有了保证
- 对程序员来说更为简单，减轻了负担

### Oauth2的四种授权模式

- 授权码模式     更安全，主流
- 简单模式
- 密码模式
- 客户端模式



### 讲一下什么是非对称加密，什么是数字签名，数字签名的作用是什么？

- 非对称加密是一种算法，采用的是一对秘钥，如果使用公钥加密，就必须要私钥才能解密，反之使用私钥加密就必须要公钥解密
- 数字签名就是公钥和私钥



### 说一下Java中的集合体系，以及他们的特点

- Collection体系集合
  - List集合(有序、有下标、元素可重复)  List实现类：ArrayList、Vector、LinkedList
    - ArrayList 类（数组结构实现，查询快、增删慢； 线程不安全	）
    - Vector 类（数组、线程同步安全）数组结构实现，查询快、增删慢；
    - LinkedList 类（链表）链表结构实现，增删快，查询慢；
  - set集合(**无序、无下标、元素不可重复**（当插入新元素时，如果新元素与已有元素进行equals比较，结果为true时，则拒绝新元素插入）)
    - HashSet 类
      - 无参构建初始容量为16（负载因子75，即+75%容量扩容）
      - 底层使用的HashMap类，即将所有需要存储的值，通过HashMap去重存入
      - 先判断hashCode是否相同，再==比较地址是否相同，再equals内容是否相同
    - TreeSet 类（二叉树-自动排序）
    - LinkedHashSet 类（记录插入顺序）底层使用LinkedHashMap（链表结构）存储，节点形式独立存储数据，并可以指向下一个节点，通过顺序访问节点，可保留元素的插入顺序 - 插入顺序
- Map体系集合
  - HashMap（数组+链表+红黑树）
    - \* keySet()  // 遍历键，可以再get(key)获取value * values()  // 遍历值，只能遍历到值 * entrySet() // 遍历键值对，效率最高
  - HashTable(线程安全) 不允许null作为key或者value
  - Properties 类（配置文件读取）
  - ConcurrentHashMap 类（线程安全且高效的Map）

### HashMap和HashTable的区别在多线程中又要保证线程安全，又要保证性能，应该用哪种Map?		

使用ConcurrentHashmap: 底层采用分段的数组+链表实现，线程安全

### 说说preparedStatement和Statement的区别

statement的sql语句使用字符串拼接，很容易出错，而preparedStatement使用？作为占位符，不容易出错易于维护

statement不对sql语句作处理，直接交给数据库，而preparedStatement支持预编译，事先将编译好的sql语句放到数据库端，相当于缓存，因此效率更高

statement有sql注入风险，preparedStatement没有sql注入风险

### 为什么要使用连接池，数据库连接池的原理

对数据库的操作都需要取得连接，使用完都需要关闭连接，如果每次操作需要打开关闭连接，这样系统性能很低下。连接池就可以动态的管理这些连接的申请，使用和释放，我们操作数据库只需要在连接池里获取连接，使用完放回连接池，这样大大节省了内存，提高效率。

数据库连接池的原理主要分为三部分

​		第一，连接池的建立，在系统初始化时建立几个连接对象以便使用。

​		第二，连接池的管理，客户请求连接数据库时，首先查看连接池中是否有空闲连接，如果有直接分配，如果没有就等待，直到超出最大等待时间，抛出异常

​		第三，连接池的关闭，当系统关闭时，连接池中所有连接关闭

### Session和cookie有什么区别

session和cookie都是为了弥补http协议的无状态特性，解决会话问题

session是以ConcurrentHashMap结构存储在服务器端，同时生成一个sessionid返回客户端并存放到cookie中

cookie是将数据存储在客户浏览器端

session占用服务器的性能，但安全性较高，使用cookie减轻服务器的压力，但有被用户篡改风险因此安全性较低

### 请求转发和重定向的区别？

请求转发：

- 默认一次请求，url路径不会改变
- 可以访问内部资源，但是不能访问外部资源，如www.baidu.com

重定向：

- 多次请求，每次请求url路径会更改
- 不可以访问内部资源，可以访问外部资源

### get和post请求的区别

- get请求携带的参数是拼接在url后面  post则是通过request body传递参数
- post比get请求相比更为安全，因为get请求，参数是直接拼接到url路径后面暴露出来的
- get携带参数有大小限制，post请求没有
- GET在浏览器回退时是无害的，而POST会再次提交请求。

### JSP的原理

jsp的本质就是servlet，静态部分是标准的html，动态部分是java程序

### Mybatis的Mapper接口为什么可以@Autowire直接注入

- 注入的是有JDK动态代理的一个代理类，在解析mapper的时候，mybatis会通过java反射获取到接口中的所有方法

### 在MyBatis如何动态修改SQL（在代码执行的过程中修改SQL）

   答：使用Mybatis的拦截器可以做到

### MyBatis的动态SQL标签有哪些？

- if  判断
- where  
- chose  选择  类似java的swatch
- foreach  遍历
- trim   去空

### Mybatis的mapper如何传递多个参数?

- 在形参列表加上@Param 注解  为字段取个别名
- 也可以用Map传参，xml中结果集用resultMap映射  

### 嵌套子查询和JOIN有什么区别？

- 嵌套查询可能有N+1问题，在查询的时候回额外发送一条sql去查询
- JOIN查询则是只会发送一条sql，在关联查询的时候，会先将join的表进行连表

### 在ResultMap中多对一关联对象查询用什么？一对多关联查询用什么？

- 多对一查询中`ResultMap`结果集映射标签中在一的一方使用**`association`**和**`javaType`**组合


- 一对多查询中`ResultMap`结果集映射标签中在多的一方使用**`collection`**和**`ofType`**组合



### 支付结果通知的幂等性怎么处理的？

拉起支付的时候，保存一份订单记录，支付宝通过同步回调判断状态是否支付成功，如果成功了就返回给前端告诉用户订单已支付

### Spring的Bean被指定为prototype以及singleton有什么区别

这两者分别指的是多例和单例模式，singleton即单例模式，指对象在整个系统中只存在一份；prototype即多例模式系统中可以有多个实例。

如果一个bean是单例模式的，在处理多次请求的时候，在ioc容器中只实例化一个bean，这个对象会被保存在一个map中，当有请求来的时候，会先从map中查看，如果有就直接使用这个对象，没有才会实例化新的对象。

如果是多例模式的bean，每次请求来的时候，会直接实例化新的bean，没有map缓存的过程。

在spring的ioc容器中的bean默认都是单例的，如果需要使用多例，可以指定scope属性：scope="prototype"

### Spring的Bean懒加载和非懒加载有什么区别 

- 懒加载：对象使用的时候才去创建。节省资源,但是不利于提前发现错误；
- 非懒加载：容器启动时立马创建。消耗资源,但有利于提前发现错误
- spring默认的使用时非懒加载即迫切加载

### Spring的依赖注入方式有哪些？ 

- 构造器注入
- setter方法注入
- 静态工厂方法注入
- 实例工厂方法注入

### 说一下Sping的Bean的生命周期

- 初始化   调用bean的构造函数，创建实例   进行参数依赖注入
- 使用
- 销毁

### RequestMapping 和 GetMapping有什么区别？

- @RequestMapping可以指定GET、POST请求方式
- @GetMapping等价于@RequestMapping的GET请求方式

### SpringMVC怎么样设定重定向和转发的

- 转发：在返回值前面加"forward:"
- 在返回值前面加"redirect:

### SpringMVC如何对时间格式的参数进行格式化？有哪些方式？

- 在类的日期属性上添加@DateTimeFormat
- 在控制器中使用@InitBind注解 

### SpringMVC常用的注解有哪些

- @RequestMapping
- @ResponseBody  

### 如何定义SpringMVC的拦截器

- 编写一个类实现HandlerInterceptor 接口  覆写preHandler请求到达之前拦截方法
- 继承HandlerInterceptorAdapter 方式也可以定义SpringMvc拦截器

### HandlerInterceptor和HandlerInterceptorAdapter的区别

相同：

- 都是拦截器，实现Spring的拦截
- 可以作为日志和登录检查使用

区别：

- HandlerInterceptorAdapter是继承    HandlerInterceptor是接口需要实现

### SpringMVC的执行原理

- 用户发送请求至前端控制器DispatcherServlet
- DispatcherServlet收到请求调用处理器映射器HandlerMapping
- 处理器映射器根据请求url找到具体的处理器，生成处理器执行链HandlerExecutionChain(包括处理器对象和处理器拦截器)一并返回给DispatcherServlet
- DispatcherServlet根据处理器Handler获取处理器适配器HandlerAdapter
- 处理器适配器HandlerAdapter执行完成返回ModelAndView
- DispatcherServlet将ModelAndView传给ViewReslover视图解析器
- ViewReslover解析后返回具体View
- DispatcherServlet对View进行渲染视图响应给用户前端

### SpringMVC的Controller是单例还是多例，有没有并发安全问题，如何解决？

- 单例，有安全并发问题，在Controller层不要定义成员变量

### Spring Boot有哪些优点

- 简化Spring的大量的繁琐配置，简单易学，易上手
- 大量减少开发时间，提高生产力
- 内嵌tomcat服务器

### SpringBoot如何做全局异常处理?

- 编写一个全局异常处理的类，在类上打上注解@ControllerAdvice 
- 在方法上打上注解@ExceptionHandler(value=异常的字节码文件)  当出现异常就会被拦截

### 创建线程有几种方式 

- 继承Thread类创建线程类

  - 定义Thread类的子类，并重写该类的run方法，该run方法的方法体就代表了线程要完成的任务。因此把run()方法称为执行体
  - 创建Thread子类的实例，即创建了线程对象。
  - 调用线程对象的start()方法来启动该线程。

- 通过实现Runnable接口创建线程类

  - 定义runnable接口的实现类，并重写该接口的run()方法
  - 调用线程对象的start()方法来启动该线程。

- 通过实现Callable接口和Future创建线程

  - 创建Callable接口的实现类，并实现call()方法，该call()方法将作为线程执行体，**并且有返回值**。
  
  - 创建Callable实现类的实例，使用FutureTask类来包装Callable对象，该FutureTask对象封装了该Callable对象的call()方法的返回值。
  
  - 使用FutureTask对象作为Thread对象的target创建并启动新线程。
  
  - 调用FutureTask对象的get()方法来获得子线程执行结束后的返回值
  
    

### Synchronized 和 lock的区别  

- lock是一个接口，而synchronized是java的一个关键字，synchronized是内置的语言实现；
- synchronized在发生异常时候会自动释放占有的锁，因此不会出现死锁；而lock发生异常时候，不会主动释放占有的锁，必须手动unlock来释放锁，可能引起死锁的发生。（所以最好将同步代码块用try catch包起来，finally中写入unlock，避免死锁的发生。
- lock等待锁过程中可以用interrupt来中断等待，而synchronized只能等待锁的释放，不能响应中断；
- Lock可以通过trylock来知道有没有获取锁，而synchronized不能；
- Lock可以提高多个线程进行读操作的效率。（可以通过readwritelock实现读写分离）
- 在性能上来说，如果竞争资源不激烈，两者的性能是差不多的，而当竞争资源非常激烈时（即有大量线程同时竞争），此时Lock的性能要远远优于synchronized。所以说，在具体使用时要根据适当情况选择。
- synchronized使用Object对象本身的wait 、notify、notifyAll调度机制，而Lock可以使用Condition进行线程之间的调度，
- synchronized可以加在方法上，也可以加在特定代码块中，括号中表示需要锁的对象。
- lock：一般使用ReentrantLock类做为锁。在加锁和解锁处需要通过lock()和unlock()显示指出。所以一般会在finally块中写unlock()以防死锁。
- synchronized是托管给JVM执行的，
  而lock是java写的控制锁的代码。
- **synchronized原始采用的是CPU悲观锁机制，即线程获得的是独占锁**
- **而Lock用的是乐观锁方式。所谓乐观锁就是，每次不加锁而是假设没有冲突而去完成某项操作，如果因为冲突失败就重试，直到成功为止。乐观锁实现的机制就是CAS操作**

### 悲观锁和乐观锁 

- 悲观锁：总是假设最坏的情况，每次去拿数据的时候都认为别人会修改，所以每次在拿数据的时候都会上锁，这样别人想拿这个数据就会阻塞直到它拿到锁**共享资源每次只给一个线程使用，其它线程阻塞，用完后再把资源转让给其它线程**(总有刁民想害朕)。Java中`synchronized`和`ReentrantLock`等独占锁就是悲观锁思想的实现。
- 乐观锁：总是假设最好的情况，每次去拿数据的时候都认为别人不会修改，所以不会上锁，但是在更新的时候会判断一下在此期间别人有没有去更新这个数据，可以使用版本号机制和CAS算法实现。乐观锁适用于多读的应用类型，这样可以提高吞吐量，像数据库提供的类似于write_condition机制，其实都是提供的乐观锁。在Java中java.util.concurrent.atomic包下面的原子变量类就是使用了乐观锁的一种实现方式CAS实现的。

### 线程的几种状态 

- **新建(NEW)**：新创建了一个线程对象。

- **可运行(RUNNABLE)**：线程对象创建后，其他线程(比如main线程）调用了该对象的start()方法。该状态的线程位于可运行线程池中，等待被线程调度选中，获取cpu 的使用权 。

- **运行(RUNNING)**：可运行状态(runnable)的线程获得了cpu 时间片（timeslice） ，执行程序代码。
- **阻塞(BLOCKED)**：阻塞状态是指线程因为某种原因放弃了cpu 使用权，也即让出了cpu timeslice，暂时停止运行。直到线程进入可运行(runnable)状态，才有机会再次获得cpu timeslice 转到运行(running)状态。阻塞的情况分三种： 

> (一). 等待阻塞：运行(running)的线程执行o.wait()方法，JVM会把该线程放入等待队列(waitting queue)中。
> (二). 同步阻塞：运行(running)的线程在获取对象的同步锁时，若该同步锁被别的线程占用，则JVM会把该线程放入锁池(lock pool)中。
> (三). 其他阻塞：运行(running)的线程执行Thread.sleep(long ms)或t.join()方法，或者发出了I/O请求时，JVM会把该线程置为阻塞状态。当sleep()状态超时、join()等待线程终止或者超时、或者I/O处理完毕时，线程重新转入可运行(runnable)状态。

-  **死亡(DEAD)**：线程run()、main() 方法执行结束，或者因异常退出了run()方法，则该线程结束生命周期。死亡的线程不可再次复生。

### Thread和Runnable的区别  

### sleep 和 wait的区别 

- sleep 是来自Thread类，wait是来自Object类
- sleep没有释放锁，而wait是释放了锁的
- 适用范围上sleep可以在任何 地方使用，wait只能在同步的控制方法上或者同步的控制块中使用
- sleep必须捕获异常，wait是可以不用捕获异常的
- sleep是Thread类的静态方法。sleep的作用是让线程休眠制定的时间，在时间到达时恢复，也就是说sleep将在接到时间到达事件事恢复线程执行。wait是Object的方法，也就是说可以对任意一个对象调用wait方法，调用wait方法将会将调用者的线程挂起，直到其他线程调用同一个对象的notify方法才会重新激活调用者。

### Synchronized 加在方法上 锁的对象是什么,加在静态方法上锁住的对象是什么？Synchronized(this) 和 Synchronized (User.class) 的区别 

- 在普通方法上锁的对象等效于this的指定对象的内置锁，即新创建对象的本身
- 而在静态方法上获取的是该方法所在类的内置锁，即xxx.class

### Synchronized 和 volatitle 关键字的区别 

### 面向对象的特征

- 封装
- 继承
- 多态

### RabbitMQ的使用场景

- 服务之间异步通信
- 顺序消费
- 定时任务
- 请求削峰

### RabbitMQ如何防止消息丢失

- 消息持久化
- comfirm机制
- ACK事务机制

### RabbitMQ的交换机有哪几种

- Fanout Exchange   广播模式，队列只要绑定到了交换机上，消息都会转发到绑定的所有队列上
- Topic Exchange     匹配才会转发
- Direct Exchange   要求队列消息与一个特定的路由键完全匹配

### 消息是如何从发送者到达消费者的（RabbitMQ工作流程）

- 消息生产者连接到RabbitMQ Broker代理，创建connection，开启Queue 信道
- 生产者声明交换机名称，类型，是否持久化等
- 发送消息，并指定消息是否持久化等属性和routing key
- exchange交换机收到消息后，根据routing key路由到当前交换机绑定的相匹配的队列里面
- 消费者监听Queue信道，收到消息后，返回发送一个ACK确认告知消息已经被消费
- RabbitMQ Broker收到ack之后将对应的消息从队列里面删除掉

### 如何防止消息重复消费？

- 在写入消息队列的数据做一个唯一标识，消费消息的时候，根据唯一标识去去判断是否消费过
- 如果已经消费了就直接丢弃，如果还没有消费，再进行消费消息。

### Lucene创建索引原理

- 倒排索引

### ES的优势

- 解决原生Lucene使用的不足，优化Lucene的调用方式
- 开箱即用
- 分布式的实时文件存储，每个字段都可以被索引并可以被搜索
- 分布式的实时分析搜索引擎
- 可以扩展上百台服务器，处理PB级结构化或非结构化的数据
- 各种语言的客户端都可以进行交互



### ES的分层结构，index下面是什么？

- index索引库-->type 类型-->Documents 文档-->字段Fields
- 一个type下的document，都有相同的field

### 讲几个ES中的查询对象：比如TermQuery 

- 组合查询与过滤  bool
- 范围查询与过滤  range
- 标准查询   match  和multi_match
- 通配符查询  wildcard
- 前缀匹配查询与过滤  prefix

### 你怎么判断一个字段要不要创建索引

- 看这个字段要不要参与关键字搜索  如果要就可以创建索引以及分词

### 你简单描述一下DSL语法

- ES提供的丰富灵活的查询语言。可以构建更为复杂强大的查询语言
- DSL语言主要分为两部分：DSL查询和DSL过滤

### 你说一下 match和term的区别？

- match 标准查询  要进行分词操作
- term 单词查询   不进行分词操作

### 项目并发高处理过不过来怎么办

- 可以做集群，将完整的应用复制一份，每个应用都具备相等的服务能力，都具有完整的功能

### 什么是集群

- 在单体架构中，为了提升应用的并发作用能力和防止单个节点出现故障，我们会通常会对应用做集群
- 集群即指的是把单体应用复制多个相同的应用，每个应用都有完整的能力，做的都是相同的事情。目的是提升系统的整体性能
- 总的来说就是：集群就是把多个应用分散在不同的服务器，每个应用跑的都是同一套代码做的是相同的工作

### 什么是负载均衡

- 当做了集群后，客户端的请求如何相对平局的分布到集群中的多个应用，这就需要负载均衡

### 什么是分布式

- 分布式就是将一个完整的应用拆分出来多个子应用，多个子应用部署在不同的服务器上，多个子应用组成一个完整的系统，相互合作才能完成最终的业务流程，缺一不可

### 集群和分布式的区别，分别解决什么问题

- 集群就是复制一份具有相同完整能力的应用  主要解决并发问题
- 分布式就是将一个完整的应用拆分到多个子应用，解决问题：减小系统服务器的压力

### 说一下你理解的微服务

- 微服务是SOA架构上的一种发展
- 一种架构模式，提倡单一应用程序分成一组小的服务，每个服务独立运行在自己的进程中，服务之间相互调用，相互协调的为用户提供最终价值



### 说一说Spring Cloud有哪些常用组件，分别有什么用？  

- EurekaServer   服务注册中心，作用：管理服务的通信地址
- Net Ribbon/Feign  负载均衡器     解决微服务之间的通信问题
- Hystrix  熔断器/断路器，   解决微服务的故障  保护微服务的安全组件
- Zuul  服务网关   请求的第一道关卡   安全，如：用户鉴权，请求监控等
- Spring Cloud ConfigServer  分布式配置    统一管理微服务的配置文件
- Bus   消息总线，广播所有微服务消息
- sleuth   链路追踪    监控微服务之间的调用关系，能让程序员直观的看到每个微服务调用的关系，已经调用的时间，是否有异常等等

### Spring Cloud的优缺点？

优点:

- 简单易懂，易部署，易维护
- 对SpringBoot风格再次封装屏蔽掉复杂的繁琐配置
- 服务拆分更细，有利于资源重复利用，提高开发效率
- 提高系统可维护性

缺点：

- 开发成本高，团队挑战大

### 什么是服务注册

- 服务注册是客户端的行为，Eureka是springcloud的一个服务注册与发现的一个组件，管理微服务通信地址的，包含了EurekaServer 服务端(也叫注册中心)和EurekaClient客户端两部分组成
- 服务注册就是微服务在启动的时候会向EurekaServer 服务端提交自己的服务信息（IP,服务名，端口）等，在EurekaServer 会形成一个微服务的通信地址列表存储起来

### 什么是服务发现

- 服务发现就是微服务会定期（默认30s）向注册中心EurekaServer 拉取一份通信地址清单保存到本地缓存中。
- 当一个微服务发起调用另外一个微服务的时候，会根据本地缓存的通信地址清单找到通信地址，然后基于HTTP协议向目标微服务发起请求

### 什么是服务续约

- 服务续约就是微服务会定期（默认30s）想服务注册中心EurekaServer 发送“心跳"请求进行服务续约，其实就是定时向注册中心EurekaServer 发送自己的健康状况，告诉EurekaServer 注册中心自己还活着，不要把自己从微服务的通信地址清单中剔除

### 如果服务挂了，注册中心要等到90s后剔除，那么在剔除前的这段时间内，挂掉的服务有可能还是会被调用，怎么处理？

- 在微服务中集成Hystrix熔断器，使其微服务有服务降级的功能，当挂掉的服务还被调用的时候，通过服务降级处理，返回托底数据

### 你知道EurekaClient服务发现和服务续约每隔30s做一次请求是用什么技术实现的吗？

- 定时任务，使用到的是ScheduledThreadPool周期执行任务的线程池。默认是30s为周期

### Ribbon是什么，Ribbon的工作原理讲一下

- 负载均衡器



### Ribbon有哪些负载均衡算法，怎么配置

- RoundRobinRule（默认）   轮循
- AvailabilityFilteringRule    过滤掉那些因为一直连接失败的被标记为circuit tripped的后端server，并过滤掉那些高并发的的后端server（active connections 超过配置的阈值）
- RandomRule    随机
- ZoneAvoidanceRule   根据性能和可用性来选择
- RetryRule    在一个配置时间段内当选择server不成功，则一直尝试使用subRule的方式选择一个可用的server
- BestAvailableRule   选择并发量最小的方式
- WeightedResponseTimeRule   根据响应时间来分配权重的方式，响应的越快，分配的值越大。

配置：注解和yml方式配置

注解方式：在主启动类编写一个Bean方法，返回类型就是负载均衡的某一个算法如：

```java
 //负载均衡算法
    @Bean
    public RandomRule randomRule(){
        return new RandomRule();
    }
```



### OpengFiegn的工作流程

- Feign即负载均衡器。在微服务发起远程调用的时候，Feign会在本地缓存的服务通信地址（通信地址是在注册中心每30秒拉取的）中通过服务名找到要调用的微服务，通过某种算法实现负载均衡调用远程微服务。默认的算法是轮询

### 为什么Feign的客户端接口没有写实现类也可以直接被依赖注入

- 注入的不是这个接口，其实注入的是jdk动态代理的代理类

### 介绍一下Hystrix

- Hystrix就是springcloud框架的熔断器组件
- 主要处理将出现故障的微服务通过熔断和降级的手法隔离开，防止因为某个服务的故障导致整个系统全部崩溃（雪崩）
- 主要有三大功能：资源隔离  服务熔断  服务降级

### 什么是熔断，什么是降级

- 服务熔断机制就是对微服务的保护机制，当一个服务出现故障异常的时候，服务会迅速触发降级操作返回托底数据，然后熔断（禁用服务的调用），当检查到该节点能正常使用时，再恢复服务
- 服务降级就是当服务因为资源、网络等故障异常的时候，返回事先准备好的一个数据给客户端

### 什么是资源隔离？

- 资源隔离包括线程隔离和信号量隔离，作用是限制调用分布式服务的资源使用，限制请求数量，一个服务出现了问题不会影响其他的服务。就好比疫情期间，感染者都会被隔离开，限制人口的流动量
- 资源隔离的两种方式：信号量隔离和线程池隔离

### 资源隔离：信号量和线程池的区别

信号量隔离：

- 使用一个信号量（数值）限制请求数量，请求不会新开线程，请求进来计数器+1，请求完成计数器-1。允许最大请求：信号量上限

线程池隔离：

- 使用线程池限制请求数量，每个请求都会新的线程中执行，允许的最大线程数：线程池的最大数+排队队列最大数，后续请求就会被拒绝

区别：

- 线程池每次请求会在新的线程中执行，信号量不会新开线程
- 线程池开销大（排队，调度，上下文），信号量不会新开线程，开销低
- 线程池支持异步，信号量不支持异步

### 对于CAP理论，Eureka选择的是AP还是CP？它保证了一致性还是可用性？

- CAP指的是一致性（Consistency）、可用性（Availabillity）、分区容错性（Partition  tolerance），三个只能满足两个。在分布式中，网络是不可控的，所以首先要保证p，然后再ac之间做选择
- Eureka是弱一致性，采用的是ap
- 保证了他的可用性。

### 说一下Eureka的自我保护

默认情况下，如果Eureka Service在一定时间内没有接收到某个微服务的心跳，Eureka Service会进入自我保护模式，在该模式下Eureka Service会保护服务注册表中的信息，不在删除注册表中的数据，当网络故障恢复后，Eureka Service 节点会自动退出自我保护模式

### 你们项目是如何做服务降级的？	

- 配合feign负载均衡器做服务降级
- 在feign负载均衡器编写的接口上的注解@FeignClient添加属性fallback=（降级类的字节码文件）
- 编写一个Hystrix类交给spring管理，然后实现负载均衡器编写的接口，覆写方法，编写服务降级的托底返回数据
- 也可以在负载均衡器的@FeignClient注解添加属于使用fallbackFactory，实现FallbackFactory类。泛型指定负载均衡器的接口，覆写方法，使用匿名内部类方式实现服务降级

### Zuul有哪几类Filter,他们的执行顺序是怎么样的？

- 前置filter    （preFilter）
- 路由filter     (routingFilter)
- 后置filter  (postFilter)
- 异常filter   (errorFilter)

执行顺序：

前置-->路由-->微服务-->路由-->后置

如果出现异常就会直接走异常fiter

### 在Zuul中做登录检查如何实现？

- 编写一个filter类去继承ZuulFilter  覆写四个方法：filterType（filter类型）、filterOrder（filter执行顺序，数值越小越优先执行）、shouldFilter（返回true时执行run方法）、run方法
- 设置类型为前置fiter  return"pre"
- 设置执行顺序  0
- 在shouldFilter方法中通过RequestContext获取请求上下文、请求体、请求url
- 如果是登录或者注册就不应该进行拦截，所以可以使用AntPathMatcher工具类判断请求的url和登录或者注册的url是否相等
- 如果相等就返回false不执行run方法，不执行登录检查逻辑
- 如果不相等就返回true执行run方法，执行登录检查逻辑
- 在run方法中获取请求头token，判断token是否存在，如果不存在就响应给前台“请登录"信息（这里使用fastJson工具将对象转换成json格式，如果内容有中文还应该进行中文编码设置）
- 最后通过RequestContext.getCurrentContext().setSendZuulResponse(false);阻止zuul继续往后执行filter

### 在Zuul中如何做限流？

- 线程池
- 信号量
- 令牌桶: token bucket,原理：以相对恒定的速率向桶中加入令牌，请求来时于桶中取令牌，取到了就放行，没能取到令牌的请求则丢弃
- 单个服务的角度实现限流,原理：利用redis键过期的自动删除的特性。以url为key,如果key不存在，创建key,并设置键过期时间，相同请求过来就对这个key进行计数，使用redis.incr原子方法，当请求超过limit时，则不让请求api

### 了解SpringCloud源码吗？

### 配置中心解决什么问题？

- 在分布式系统中，由于微服务数量很多，所以一般会使用Springcloud config配置中心帮助我们管理各个微服务的配置文件
- 支持配置文件放在配置服务的本地，也支持远程放在git仓库中集中管理

### EureakServer的搭建流程

- pom中导入EureakServer的依赖
- 编写主启动类，打上注解@SpringBootApplication 主启动类注解   @EnableEurekaServer 开启Eureka服务注解
- 编写配置文件application.yml  配置五大内容：端口 服务名   实例ID   使用IP地址注册 注册地址

### Ribbon的整合流程

- pom中导入Ribbon基础依赖
- 在配置文件中做一些相应的配置，如：读取超时的时间，链接超时时间，重试机制，开启饥饿加载 等。
- 在主启动类写一个注册RestTemplate的Bean方法上打上@Bean注解，交给spring管理，并且在方法上打上负载均衡注解@LoadBalanced，让RestTemplate拥有负载均衡的能力
- 在接口controller层具体业务的方法内，使用RestTemplate发送远程调用，调用的链接地址和端口是被调用的微服务的服务名

### Feign的整合流程

- pom中导入Feign的基础依赖
- 在主启动类上打上注解@EnableFeignClients（basePackages=“{feign的接口全限定名}"）
- 编写一个feign的接口`userFeignClient`。 类上打上注解@FeignClient(value=“被调用的微服务的服务名")
- 复制controller层的调用方法，删除方法体（因为这是接口），请求路径相同，请求方法相同，携带参数相同，方法名相同，返回类型相同
- 在controller层@Autowired注入自定义的 feign的接口`userFeignClient`，在方法体中使用接口调用微服务获取

### Hystrix的整合流程

- pom中导入Hystrix的基础依赖
- 配置中心开启Hystrix熔断  feign.hystrix.enable=true
- 编写服务降级的接口，注解@FeignClient（value="远程调用的微服务的服务名"）
- 复制微服务调用的方法到接口中，删除方法体。返回值类型相同，远程调用微服务的路径相同，请求方式相同，参数相同，方法名相同。

### Zuul的整合流程

- pom中导入Zuul网关的依赖
- 编写主启动类，类上打上注解@SpringBootApplication  主启动注解   @EnableEurekaClient 开启Eureka客户端（zuul网关也是需要注册到注册中心的） @EnableZuulProxy 开启zuul网关支持
- 配置yml配置文件，配置Eureka的5大点，端口，注册中心地址，服务名，实例ID，使用IP地址注册   。配置zuul网关的前缀prefix，配置每个微服务的别名，禁用所用浏览器通过服务名访问服务的方式

### ConfigServer的整合流程

服务端：

- 新建config配置中心微服务，导入Eureka客户端依赖，导入config配置中心的依赖，导入web依赖
- 编写主启动类，@SpringBootApplication，@EnableEurekaClient（注册配置中心的地址），@EnableConfigServer 开启配置中心服务端
- 编写application.yml配置文件，配置端口，使用IP注册，实例ID，服务名，注册中心地址。去注册中心注册微服务。
- 新建git仓库，在application配置文件中指定远程仓库的账号，密码以及仓库地址

微服务客户端：

- 在微服务客户端的pom中导入config的依赖
- 在git的远程仓库，新建yml文件，application-微服务名-dev(环境名).yml
- 抽取微服务客户端的yml配置文件拷贝在git中的yml文件上
- 微服务客户端新建bootstrap.yml，指定配置中心服务端的地址，git的配置文件名，环境名，分支



### 为什么要使用Redis做缓存

- 高性能
  - Redis是基于内存实现的，如果传统去数据库查找数据。性能低下。而Redis操作的是缓存就是操作内存，所以速度会更快
  - 那为什么这么快？  基于内存，数据结构简单，单线程避免了不需要的上下文切换和竞争条件， 多路I/O复用模型，非阻塞IO
- 高并发
  - 直接操作缓存能够承受的请求是远远大于直接访问数据库的，所以我们可以考虑把数据库中的部分数据转移到缓存中去，这样用户的一部分请求会直接到缓存这里而不用经过数据库。

### 缓存的执行流程

客户端发起查询请求

判断缓存中是否有数据

​	如果有，直接返回

​	如果没有，就从数据库查询，再把数据同步到缓存

返回数据给客户端

如果数据库中的数据增加或者修改了，那么就会删除缓存的数据，保证缓存与数据库数据的一致性

### SpringCache常用注解

- @EnableCaching：开启Spring Cache框架支持，打在主启动类上。解析对应的注解，实现缓存读写访问     
- @CacheConfig：缓存配置，可以配置当前类型中所用缓存注解的通用信息，示例：配置当类前所有缓存注解的缓存前缀，@CacheConfig(cacheNames = "cache:prefix")
- @Cacheable：表示要对方法返回值进行缓存  。一般用于查询的时候查询到的数据返回值缓存在Redis。**一般用在查询方法上**
- @CacheEvict：淘汰缓存注解，`allEntries` 代表是否删除cacheNames对应的全部的缓存。 ，默认false，可选true。**一般用在更新或者删除的方法上**
- @CachePut: 更新缓存，如果key存在覆盖缓存数据。key不存在，新增数据到缓存。**通常用在新增方法上**



### 说一下security中的常用filter

- SecurityContextPersistenceFilter    security的第一道filter
- UsernamePasswordAuthenticationFilter     认证操作全靠这个过滤器，默认匹配URL为/login且必须为POST请求
- ExceptionTranslationFilter    异常转换过滤器位于整个SpringSecurityFilterChain的后方，用来转换整个链路中出现的异常
- FilterSecurityInterceptor    获取所有配置资源的访问授权信息，根据SecurityContextHolder中存储的用户信息来决定其是否有权限。



### Oauth2授权有几种方式，你们项目用的哪种

- 授权码模式   一般在第三方接口上会用到授权码模式，比如微信三方登录
- 简单模式   相比授权码模式，就是减少了获取授权码的过程
- 密码模式   用于在自己平台上的用户使用
- 客户端模式   最不安全的

项目中三方登录，涉及到用户的信息安全性，所以采用的是授权码模式



### 你使用过ES的哪些聚合查询？

Max求最大  min求最小  avg求平均   sum求和   stats求最大，最小，平均，和

### ES高亮怎么做的？

new一个HighlightBuilder类，使用里面的Field方法，指定要高亮的字段，再指定preTags方法（标签）编写html语法，写入高亮的颜色

```java
HighlightBuilder.Field highlightField  = new HighlightBuilder.Field("name").
        preTags("<font style='color:red'>").
        postTags("</font>");
```

### 

### Oauth2的授权模式有哪些，分别使用在什么场景？

- 授权码模式   一般在第三方接口上会用到授权码模式，比如微信三方登录
- 简单模式   相比授权码模式，就是减少了获取授权码的过程
- 密码模式   用于在自己平台上的用户使用
- 客户端模式   最不安全的  服务于服务之间





### 说一下Eureka的自我保护

默认情况下，如果Eureka Service在一定时间内没有接收到某个微服务的心跳，Eureka Service会进入自我保护模式，在该模式下Eureka Service会保护服务注册表中的信息，不在删除注册表中的数据，当网络故障恢复后，Eureka Servic 节点会自动退出自我保护模式

### 说下Ribbon和Feign的区别呢？

- Ribbon和Feign都是实现负载均衡的组件，Feign的本质是Ribbon，基于Ribbon
- Ribbon 是一个基于 HTTP 和 TCP 客户端的负载均衡器它可以在客户端配置  ribbonServerList（服务端列表），然后轮询请求以实现均衡负载它在联合 Eureka 使用时ribbonServerList 会被  DiscoveryEnabledNIWSServerList 重写，扩展成从 Eureka 注册中心获取服务端列表同时它也会用  NIWSDiscoveryPing 来取代 IPing，它将职责委托给 Eureka 来确定服务端是否已经启动。 使用 HttpClient 或 RestTemplate 模拟http请求，步骤相当繁琐。
- Feign 是在 Ribbon的基础上进行了一次改进，是一个使用起来更加方便的 HTTP 客户端。采用接口的方式， 只需要创建一个接口，**面向接口**；然后在上面添加注解即可 ，将需要调用的其他服务的方法定义成抽象方法即可， 不需要自己构建http请求。然后就像是调用自身工程的方法调用，而感觉不到是调用远程方法，使得编写 客户端变得非常容易。

### Spring,SpringBoot和SpringCloud的关系以及区别

-  Spring Boot简化了基于 Spring的应用开发,通过少量的代码就能创建一个独立的、产品级別的 Spring应用。Spring Boot的核心思想就是约定大于配置,一切自动完成
- Spring Cloud是一系列框架的有序集合。Spring Cloud依赖于Spring Boot。  
- Spring Boot 可以离开Spring Cloud 独立开发单体项目

### ES的keyword和text区别

- keyword不分词
- text分词

### 常见Http状态码

- 200  成功
- 301  告诉客户端链接已经发生该改变，并向新的链接发出请求
- 404  请求失败，客户端请求的资源没找到或不存在
- 500   服务器遇到未知错误，一般就是代码错误了
- 503  无法解决当前的请求   服务器过载或者维护



### 什么是事务

事务指的是对单个工作业务（service方法）执行数据库的一系列操作时，要么全部成功，要么全部失败

### 事务的四大特性

- 原子性  A
- 一致性  C
- 隔离性  I
- 持久性  D

### InnoDB如何保证原子性和持久性的

- 保证原子性是利用InnoDB的undolog回滚日志文件实现的。当删除一条数据的时候，他会先记录下来这条数据保存在undolog表中，如果出现了回滚，就会把原有的数据再insert回去。当添加一条数据的时候，记录下来的是这个数据的主键，回滚的时候就根据主键执行delete
- 保证持久性是利用Redolog实现的。Redolog记录的是数据的备份，在事务提交前，只要将Redolog持久化，当系统崩溃了，Redolog就可以恢复到最新的状态

### 事务并发问题有哪些

- 脏读：读到了事务并未提交的数据，未提交就意味着事务有可能会存在回滚
- 幻读：事物A两次读取相同条件的数据读到的条数不一样
- 不可重复读：同一个事务中多次使用相同条件读取到的数据是不一样的

### 事务隔离级别有哪些，分别能解决什么问题

-  读未提交（READ UNCOMMITTED）  
- 读提交 （READ COMMITTED）解决脏读问题，读取的全是已经提交的数据
- 可重复读 （REPEATABLE READ）解决脏读和不可重复读的问题
- 串行化 （SERIALIZABLE） 解决脏读和不可能重复读以及幻读的问题

### MySql的InnoDB是如何保证原子性的

- 保证原子性是利用InnoDB的undolog回滚日志文件实现的。当删除一条数据的时候，他会先记录下来这条数据保存在undolog表中，如果出现了回滚，就会把原有的数据再insert回去。当添加一条数据的时候，记录下来的是这个数据的主键，回滚的时候就根据主键执行delete

### MySql的InnoDB是如何保证持久性的

- 保证持久性是利用Redolog实现的。Redolog记录的是数据的备份，在事务提交前，只要将Redolog持久化，当系统崩溃了，Redolog就可以恢复到最新的状态

### 说一下事务的执行流程(Undolog+Redolog)

- 开启事务
- 记录回滚日志到undolog
- 执行事务
- 将数据持久化到redolog
- 提交事务
- 将redolog写入数据库磁盘

### 解释一下事务并发丢失更新问题，·如何解决

丢失更新就是两个不同的事务在某一时刻对同一个数据进行读取后，先后进行修改，导致第一次操作数据丢失。比如取款，余额起始是1000元，A事务进来查询到是1000元，想要存款100元，此时B事务进来也查询到1000元余额，要取款100元。B事务先执行了取款业务，此时余额就成了900元，A事务提交事务，存款成了1100元。最终导致银行丢失100元。

解决方案：

- 悲观锁思想。加入写锁（排他锁），事务未经提交，其他的事务根本没法获取修改权，因此排它锁可以用来控制丢失更新。在sql语句最后加入for update语句
- 乐观锁思想。在表中加入一个版本控制字段，记录这条数据的版本，每次操作同一条数据的时候把上次版本作为条件进行更新

​	

### InnoDB事务隔离的实现原理是什么

MVCC机制和读写锁

读写锁：要求每次在读的操作时候，多个事务需要获取一个共享锁，这个锁不是排他性的，不会相互之间互斥。但那是在写的操作的时候，就需要写锁，只允许一个线程获得该锁，只有等这个线程释放了锁，其他线程才能进行写操作

MVCC机制就是多版本并发控制，它是在读取数据的时候通过一种类似数据快照的形式保存一个副本，不同的事务看到的数据快照版本是不一样的，即使一个事务修改了数据，对其他事务也是不可见的，只能看到第一次查询的数据快照

### 什么是分布式事务，  分布式事务你知道哪些解决方案？  这些方案如何选型

- 在微服务中，每个服务之间可能存在调用关系，并且每个服务之间有不同的数据库，所以分布式事务就是要解决一个请求同时对多个数据库写操作的一致性。
- 解决方案：
  - 2pc   基于XA协议实现的二阶段提交方案   强一致性   注册登录的时候用
  - TCC  补偿性事务
  - 可靠消息最终一致性    一般适用于平台内部，对一 致性要求相对较高(微服务的2个子系统之间)。比如优惠券和积分以及短信
  - 最大努力通知    所谓最大努力通知就是系统A用最大努力通知系统B，能不能成功，不做完全保证，如果没通知到位，  系统B可以主动来调用系统A的接口查询结果状态。一般适用于跨平台业务，或对接了上方平台的业务场景(支付结果通知)。支付宝

### 什么是2pc,基于什么协议，有什么缺点？

- 2PC即两阶段提交协议,是将整个事务流程分为两个阶段,准备阶段( Prepare phase).提交阶段( commit phase ) , 2是指两个阶段, P是指准备阶段, C是指提交阶段。
- 基于XA协议实现的两阶段提交方案
- 缺点(**二阶段能保证分布式事务的原子性，但是也有一些明显的缺陷**)
  - 在第一阶段，如果参与者迟迟不回复协调者，就会造成事务的阻塞，性能不好
  - 单节点故障，如果协调器挂了，参与者会阻塞，比如在第二阶段，如果事务协调器宕机，参与者没办法回复信息，长时间处于事务资源锁定，造成阻塞(事务操作是要加锁的)。
  - 在第二阶段，如果在事务协调器发出"commit"执行后宕机，一部和参与者收到了消息提交了事务，而  一部分没有消息没法做出事务提交操作，这样就出现了数据不一致。
  - 在第二阶段，如果事务事务协调器发出“commit”指令后宕机，收到“commmit”指令的参与者也宕机了， 那么事务最终变成了什么效果，提交了还是没提交？没有谁知道。

### Seata相比传统2PC有什么区别，以及优点？

Seata是由阿里中间件团队发起的开源项目Fescar ,后更名为Seata ,它是一个是开源的分布式事务框架。

- 区别
  - 传统2PC方案的RM(资源管理器)实际上是在数据库层, RM本质上就是数据库自身,通过XA协议实现,而Seata的RM是以jar包的形式作为中间件层部署在应用程序这一侧的。
  - 传统2PC无论第二阶段的决议是commit还是rollback ,事务性资源的锁都要保持到Phase2完成才释放。而Seata的做法是在Phase1就将本地事务提交,这样就可以省去Phase2持锁的时间,整体提高效率。



### Seata的TC,TM,RM的含义，以及作用？

- Transaction Coordinator(TC) - 事务协调器：一个独立运行的组件，负责维护全局事务的运行状态，负责根据TM的指令协调并驱动全局事务的提交或回滚，负责向资源管理器发起事务提交，回滚指令。
- Transaction Manager(TM) - 事务管理器 ：控制全局事务的边界，负责开启一个全局事务，并最终发起全局提交或全局回滚的决议，通知TC提交或者回滚事务。
- Resource Manager(RM) - 资源管理器： 控制分支事务，负责分支事务注册、负责向TC汇报分支事务状态，并接收事务协调器的指令，驱动分支（本地）事务的提交和回滚

### 你知道TCC吗，它有什么样的优缺点？

TCC, 是基于补偿型事务的AP系统的一种实现, 具有弱一致性

- 优点：异步执行效率高  TCC能够对分布式事务中的各个资源进行分别锁定, 分别提交与释放
- 缺点：对应用的侵入性强。业务逻辑的每个分支都需要实现try、confirm、cancel三个操作，应用侵入性较强，改造成本高。实现难度较大

### 解释一下Seata的工作原理

- TM（事务管理器）向TC(事务协调器)发起开启分布式事务。注册全局事务记录，TC生成XID事务ID返回给TM
- TM拿到XID给到RM(资源管理器)向TC注册本地事务分支，加入全局事务ID(XID)
- RM开启业务逻辑，数据库写入unlog日志，提交分支事务，上报事务状态给TC
- 如果出现某个RM事务分支执行失败，报告失败状态给TC，然后TM事务管理器向TC事务协调器发起全局事务回滚请求。
- TC向RM事务分支发起事务回滚请求，RM(Order, Account)收到回滚指令，然后会解析undo log，指向反向操作，把数据还原到修改之前，删除undo log,提交本地事务。

### 你能简单描述一下你在项目中是如何集成Seata的吗

- 下载Seata事务协调器，安装
- 导入依赖
- 导入config配置文件在resources目录下
- 修改application.yml配置文件 指定seata的事务组名
- 编写一个配置类，注册连接池，读取yml配置文件的mapper-locations映射路径等

### 你说一下什么是分布式锁

分布式锁就是在集群或者分布式环境中使用加锁的手段保证多个服务节点对同一个数据的原子性操作，保证数据的安全性

### 分布式锁有哪些解决方案

- 数据库  （性能不好）
  - 悲观锁For Update 的思想是在查询对象时就要加锁，其他的线程在查询时就必须等待，性能太差
  - 基于数据库主键实现分布式锁：利用主键或唯一索引唯一的特性，如果有多个请求同时提交到数据库的话，数据库会保证只有一个操作可以成功，那么我们就可以认为操作成功的那个线程获得了该方法的锁，当方法执行完毕之后，想要释放锁的话，删除这条数据库记录即可。
- Redis缓存和超时
- zookeeper

### Redis如何实现分布式锁，用什么命令

- 使用Redis的setnx命令实现分布式锁，该命令只会在键key不存在的情况下将key设置为value，如果key已经存在，setnx命令就不做任何操作。但是`setnx`获取锁和`expire`不是原子性操作   如果在获取锁的时候成功了，但是在设置过期时间的时候挂了，锁也永远得不到释放，又变成死锁
- 使用set命令实现分布式锁，该命令可以当做`setnx`和`expire`的组合命令来使用，而且是原子性的

### Redis实现分布式锁可能会出现什么问题，如何解决

- 锁超时/死锁问题   setnx命令获取锁的时候成功了，但是在设置过期时间的时候挂了，锁也永远得不到释放，又变成死锁。`使用set命令实现分布式锁，该命令可以当做setnx和expire的组合命令来使用，而且是原子性的`
- 锁的误删问题    设置了过期时间，在A服务拿到锁了之后，业务代码还没执行完毕，锁就已经过期了。这时B服务又进来拿到锁了，那么等A服务业务执行完毕后，释放删除的锁就是B服务的锁   `可以在删除锁的时候先判断一下要删除的锁是不是自己上的锁，比如可以把锁的值使用一个UUID，在释放锁的时候先获取一下锁的值和当前业务中创建的UUID是不是同一个，如果是才执行·del删除锁，当然也可以使用线程的ID替代`
  - 但是上面的代码依然有问题，就是判断锁的代码和删除锁的代码也不是原子性的，依然可能会导致锁的误删除问题，比如服务A在判断锁成功准备删除锁时，锁自动过期，别的服务B获取到了锁，然后服务A执行DEL就可能会把服务B的锁给删除掉，所以，我们必须保证 获取锁 -> 判断锁 -> 删除锁 的操作是原子性的才可以，解决方案可以使用`Redis+Lua`脚本来解决一致性问题

### 你项目中怎么使用分布式锁的

Redisson实现分布式锁(`底层也用到了Lua脚本保证原子性`)

- Redisson加锁自动有过期时间30s，监控锁的看门狗发现业务没执行完，会自动进行锁的续期(重回30s)，这样做的好处是防止在程序执行期间锁自动过期被删除问题
- 当业务执行完成不再给锁续期，即使没有手动释放锁，锁的过期时间到了也会自动释放锁

### 了解Redission的看门狗原理吗？

- Redisson以 30s 作为锁的默认过期时间，获取锁成功后(底层也用到了Lua脚本保证原子性)会开启一个定时任务定时进行锁过期时间续约，即每次都把过期时间设置成 30s，定时任务 10s执行一次(看门狗)。
- 看门狗能够监听当前业务是否执行完毕，如果还没有执行完毕就会自动延时。执行完毕后会自动释放锁

### 你知道zookeeper实现分布式锁吗？

- 获取分布式锁的时候在locker的节点下创建一个临时顺序节点，释放锁的时候删除该临时节点
- 当多个线程请求的时候，都为其创建一个临时顺序节点，通过subscribeDataChanges方法监听前一个节点
- 判断当前节点是不是第一个节点，如果前一个节点被删除了，自己就是第一个节点了，就拿到锁了就执行

上面就是实现分布式锁的原理，具体一般用封装好的分布式锁的工具curator

### 你在项目中如何使用ZK实现分布式锁的？

工具curator

### 如果没有Redis和zookeeper怎么实现分布式锁？

数据库也可以实现分布式锁。利用数据库主键或唯一索引的特性实现。表中可以加一个版本字段，每次操作数据的时候，判断版本状态，如果正确才进行操作，如果不正确就可以自旋等待操作

其核心目的就是多个服务操作同一条数据的时候，在利用一些中间件等实现一把共享的锁。

### 你们数据库和Redis的数据一致性怎么做的

- 先删除缓存，再更新数据库，更新完后，再将新的数据刷回缓存redis

### 了解缓存击穿，穿透，雪崩吗？怎么处理？

- **缓存击穿**是指缓存中没有但数据库中有的数据（一般是缓存时间到期），这时由于并发用户特别多，同时读缓存没读到数据，又同时去数据库去取数据，引起数据库压力瞬间增大，造成过大压力
  - 解决方案：
  - 设置热点数据永远不过期
  - 加互斥/排他锁
- **缓存穿透**是指缓存和数据库中都没有的数据，而用户不断发起请求，如发起为id为“-1”的数据或id为特别大不存在的数据。这时的用户很可能是攻击者，攻击会导致数据库压力过大。
  - 解决方案：
  - 接口层增加校验，如用户鉴权校验，id做基础校验，id<=0的直接拦截；
  - 从缓存取不到的数据，在数据库中也没有取到，这时也可以将key-value对写为key-null，缓存有效时间可以设置短点，如30秒（设置太长会导致正常情况也没法使用）。这样可以防止攻击用户反复用同一个id暴力攻击
-  **缓存雪崩**是指缓存中数据大批量到过期时间，而查询数据量巨大，引起数据库压力过大甚至down机。和缓存击穿不同的是，    缓存击穿指并发查同一条数据，缓存雪崩是不同数据都过期了，很多数据都查不到从而查数据库。
  - 解决方案：
  - 缓存数据的过期时间设置随机，防止同一时间大量数据过期现象发生。
  - 如果缓存数据库是分布式部署，将热点数据均匀分布在不同搞得缓存数据库中
  - 设置热点数据永远不过期

### 你们ES和数据库的数据一致性怎么做的？

使用阿里巴巴的canal对数据进行同步

MYSQL数据库开启binlog日志，可以记录数据库操作日志，安装canal和MYSQL数据库进行链接，使用canal监听MYSQL数据库的变化，如果数据库有变化可以改变ES中的数据



### 你们这个接口QPS是多少

- 当时开发的时候，老大给我们的需求是能达到2000的QPS

### 如果流量更高，比如：每秒10W请求，应该怎么处理

- 前端可以做一些处理，比如，增加图片验证码，减少每秒的请求数量。也可以做一些丢弃部分请求的策略，比如为每个请求加个随机数，判断随机数小于5的请求直接丢弃。使用Nginx服务器，也可以做集群
- 后台减少与数据库交互，调用链减少。也可以做集群来处理高并发



### 整个秒杀流程你用了几个队列，分别用来存储什么东西

- 延迟队列，存储秒杀到商品支付超时的订单
- 死信队列



### 你们怎么处理超卖，少卖的？

- 使用的是Hystrix的资源隔离的信号量手段来解决。信号量特性永远不会为负数

### 你知道BIO,NIO,AIO么？讲一下你的理解

- BIO 同步并阻塞
- NIO 同步非阻塞
- AIO 异步非阻塞

### 如何提高接口的qps

 一方面：提高并发数

   多线程,尽量用线程池
          (线程个数：CPU核数 / (1 - 阻塞系数(IO密集型接近1，计算密集型接近0)))
   适当调整连接数(Tomcat,Redis，Mysql等连接数)
   集群
 二方面：提高接口响应速度
   减少和数据库交互，使用Redis代替
   使用异步方案，比如MQ
   使用并发编程，多个线程同时工作
   减少服务的调用链
   实在要连数据库，考虑数据库优化

### 创建线程的3种方式，  三种线程的区别？， start() 和 run()方法区别

- 继承Thread类创建线程类

  - 定义Thread类的子类，并重写该类的run方法，该run方法的方法体就代表了线程要完成的任务。因此把run()方法称为执行体
  - 创建Thread子类的实例，即创建了线程对象。
  - 调用线程对象的start()方法来启动该线程。
- 通过实现Runnable接口创建线程类

  - 定义runnable接口的实现类，并重写该接口的run()方法
  - 调用线程对象的start()方法来启动该线程。
- 通过实现Callable接口和Future创建线程

  - 创建Callable接口的实现类，并实现call()方法，该call()方法将作为线程执行体，**并且有返回值**。
  - 创建Callable实现类的实例，使用FutureTask类来包装Callable对象，该FutureTask对象封装了该Callable对象的call()方法的返回值。
  - 使用FutureTask对象作为Thread对象的target创建并启动新线程。
  - 调用FutureTask对象的get()方法来获得子线程执行结束后的返回值
- 三种线程的区别：Thread是一个类，继承，单继承，有局限性。Runnable和Callable是接口，多实现，扩展性强一点。  只有实现Callable才有返回值
- start和run方法的区别
  - 启动一个线程需要调用 Thread 对象的 start() 方法。调用线程的 start() 方法后，**创建一个新的线程线程处于可运行状态，此时它可以由 JVM 调度并执行，这并不意味着线程就会立即运行**
  - run() 方法是线程运行时由 JVM 回调的方法，无需手动写代码调用，**直接调用线程的 run() 方法，相当于在调用线程里继续调用方法，并未启动一个新的线程**

### Synchronized和Lock的区别

- **lock是一个接口，而synchronized是java的一个关键字**，synchronized是内置的语言实现；
- **synchronized在发生异常时候会自动释放占有的锁**，因此不会出现死锁；**而lock发生异常时候，不会主动释放占有的锁，必须手动unlock来释放锁**，可能引起死锁的发生。（所以最好将同步代码块用try catch包起来，finally中写入unlock，避免死锁的发生。
- lock等待锁过程中可以用interrupt来中断等待，而synchronized只能等待锁的释放，不能响应中断；
- Lock可以通过trylock来知道有没有获取锁，而synchronized不能；
- Lock可以提高多个线程进行读操作的效率。（可以通过readwritelock实现读写分离）
- 在性能上来说，如果竞争资源不激烈，两者的性能是差不多的，而当竞争资源非常激烈时（即有大量线程同时竞争），此时Lock的性能要远远优于synchronized。所以说，在具体使用时要根据适当情况选择。
- synchronized使用Object对象本身的wait 、notify、notifyAll调度机制，而Lock可以使用Condition进行线程之间的调度，
- synchronized可以加在方法上，也可以加在特定代码块中，括号中表示需要锁的对象。
- lock：一般使用ReentrantLock类做为锁。在加锁和解锁处需要通过lock()和unlock()显示指出。所以一般会在finally块中写unlock()以防死锁。
- **synchronized是托管给JVM执行的，**
  **而lock是java写的控制锁的代码。**

### 线程的生命周期,  sleep 和 wait区别

- 生命周期：**new**创建一个线程    调用start方法启动线程进入一个**可运行的状态**	当线程争夺到cpu的执行权的时候就会进入到**运行状态**    任务处理完后**销毁线程**      
  - 如果在调用了sleep或者wait方法后，线程会重新进入到可运行状态
- 区别：
  - sleep 是来自Thread类，wait是来自Object类
  - sleep没有释放锁，而wait是释放了锁的
  - 适用范围上sleep可以在任何 地方使用，wait只能在同步的控制方法上或者同步的控制块中使用
  - sleep必须捕获异常，wait是可以不用捕获异常的
  - sleep是Thread类的静态方法。sleep的作用是让线程休眠制定的时间，在时间到达时恢复，也就是说sleep将在接到时间到达事件事恢复线程执行。wait是Object的方法，也就是说可以对任意一个对象调用wait方法，调用wait方法将会将调用者的线程挂起，直到其他线程调用同一个对象的notify方法才会重新激活调用者。

### synchronized 锁的原理，JDK6之后做了什么样的优化?

- 底层是基于JVM内置锁实现的，通过内部对象Monitor（监视器锁）实现，监视器锁实现是依赖于底层操作系统实现的，是一个重量级锁性能较低
- 优化：加入了偏向锁、轻量级锁、重量级锁
- 在大多数的情况下，锁是不会存在竞争的，大多数都是同一个线程多次获得的。偏向锁就是某个线程获得锁之后，会记录下来这个线程的ID在对象的标志位中。
- 当出现了第二个线程加入了锁的竞争的时候，这个时候就会升级到轻量级锁，第二个进来没有拿到锁的线程会进入到一个自旋的过程。默认是自旋10次
- 当锁竞争比较激烈，某个线程自旋次数已经超过10次了，一直自旋就会极大的消耗性能，所以这个时候synchronized 就会升级到重量级锁，把那些自旋超过10次的线程会直接挂起

### 乐观锁的使用场景(数据库,ES)

- 数据库
- ES 全文检索技术

### 什么是CAS

- 乐观锁思想的一种概念，Compare-and-Set   比较并设置。每次操作的时候都会对version版本进行比较，如果版本一致才会进行设置新的数据

### AtomicInterger怎么保证并发安全性的

- Atomic开头的类是基于CAS的乐观锁
- 使用version版本控制

### 什么是乐观锁，什么是悲观锁，什么是重入锁，什么是自旋锁，怎么是阻塞。

- 乐观锁：总是想着好的方面，每次操作数据的时候，总是认为数据没有被更改。就是不加锁，在数据库中使用Version版本控制实现乐观锁思想的
- 悲观锁：总是往坏处想，认为每次操作数据的时候，数据是被更改的。常见的悲观锁思想的锁：synchronized ，ReentrantLock 
- 重入锁：允许同一个线程可以拿到同一把锁。可重入锁就是同一个线程在拿到锁之后执行的代码块中又调用了当前方法，这时就不需要重新等待获取锁
- 自旋锁：当A线程拿到锁在执行业务的时候，B线程进来就拿不到锁，那么B线程就是进入自旋状态，一直尝试获取锁
- 阻塞：当多个线程同时访问的时候，只有一个线程能拿到锁，其他线程就进入阻塞状态，排队等候拿到锁的线程释放锁，再去争夺获取锁。这就叫阻塞

### 你用过JUC中的类吗，说几个：

Lock，ConcurrentHashMap ,AtomicInteger

### ThreadLocal的作用和原理？ThreadLocal的使用场景

- 作用：为每个线程提供一个独立的变量副本解决变量并发访问的冲突问题

- 原理：每一个线程Thread内部有一个ThreadLocalMap，set()的时候这个Map里面存储key就是this当前这个ThreadLocal，value就是线程的设置的变量副本。在get()的时候通过ThreadLocal作为key取出里面的变量副本value

- 使用场景：每个线程内需要保存类似于全局变量的信息（例如在拦截器中获取的用户信息），可以让不同方法直接使用，避免参数传递的麻烦却不想被多线程共享（因为不同线程获取到的用户信息不一样）。

  例如，用 ThreadLocal 保存一些业务内容（用户权限信息、从用户系统获取到的用户名、用户ID 等），这些信息在同一个线程内相同，但是不同的线程使用的业务内容是不相同的。

  比如：在SpringSecurtix的RequestContextHoder中就使用的到了ThreadLocal，还有在springMVC中获取请求的RequestConText上下文中也是使用到了ThreadLocal

### 线程池的作用，常用的线程池有几种，分别是什么意思?

- 作用：以空间换时间的方式，为每一个线程提供一份变量副本，实现同时访问互不干扰。其核心作用就是对多线程中的每个线程之间的数据相互隔离
- 常用的线程池：
  - CachedThreadPool：可缓存的线程池，线程池内部是**没有设置核心线程数的，最大线程数就是integer的最大值21亿+**，空闲时间为60s。适用：执行很多短期异步的小程序或者负载较轻的服务器。
  - FixedThreadPool ：指定长度的线程池，内部**最大线程数就是核心线程数**，空闲时间0S，适用：执行长期的任务，性能好很多
  -  SingleThreadPool ： 单个线程，内部核心线程数和最大线程数为1，只能处理一个线程，适用：一个任务一个任务执行的场景。 如同队列
  - ScheduledThreadPool ： 周期执行线程池，设置核心线程数，最大线程数也是integer的最大值21亿+，过期时间默认是10s，l 适用：周期性执行任务的场景（定期的同步数据）

### 线程池的执行流程

- 当有新的任务来的时候，首先会去用核心线程来处理任务，如果新的任务超出了核心线程数量，那么就会将超出的任务放在队列中排队。当队列中排队的任务也满了之后，那么就会新建线程，新建的线程受线程池中允许的最大线程数所控制。例如，核心线程数为5个，队列里面排队5个，核心线程数为20个，那么还能新建10个非核心线程
- 如果新建了非核心线程来处理任务仍然不能处理完成，那么就会走拒绝策略。拒绝策略分为：丢弃新的任务并报异常，丢弃新的任务不报异常，丢弃旧的任务去处理新的任务，由调用线程方处理业务(调用方的主线程处理)

### 解释一下线程池构造器的7个参数  

- CorePoolSize：核心线程数，保留在线程池中的

- MaximumPoolSize ：线程池中允许的最大线程数

- KeepAliveTime：非核心线程数空闲时间

- Unit：空闲时间单位

- WorkQueue：线程的队列，在执行任务时用来保留任务的队列

  - 是一个BlockingQueue阻塞队列，超过核心线程数的任务会进入队列排队

  - SynchronousQueue：这个队列比较特殊，它不会保存提交的任务，而是将直接新建一个线程来执行新来的任务；

    LinkedBlockingQueue：基于链表的先进先出队列，如果创建时没有指定此队列大小，则默认为Integer.MAX_VALUE；

    ArrayBlockingQueue：基于数组的先进先出队列，此队列创建时必须指定大小

- 线程的工厂模式，执行程序创建线程时要用的工厂

  - 使用ThreadFactory创建新线程。 推荐使用Executors.defaultThreadFactory

- Handler：拒绝策略。任务超过 最大线程数+队列排队数 ，多出来的任务该如何处理取决于Handler。达到线程边界和队列容量而阻止执行所使用的程序（方法）

### EurekaClient拉取注册表&心跳续约用到了什么技术来实现？	

- 定时任务，使用到的是ScheduledThreadPool周期执行任务的线程池。默认是30s为周期

### synchronized 和 volatile 的区别是什么？

- synchronized 关键字是线程同步的轻量级实现，所以volatile性能比 synchronized 好
- volatile 关键字只能用于变量，synchronized 关键字可以用在同步代码块和方法上
- 多线程的场景下volatile 不会是线程阻塞，而synchronized 关键字可能会发生阻塞
- volatile 保证数据的可见性，但不保证原子性。synchronized 两者都能保证
- volatile关键字主要用于解决变量在多个线程之间的可见性，而 synchronized关键字解决的是多个线程之间访问资源的同步性。

### 数据结构有哪几种分类？

按照逻辑结构分类：

- 集合结构。该结构中的所有元素散列存放
- 线性结构。一条线，一对一关系。常见的数组、链表就是线性结构，数组是线性结构中的顺序结构。链表是线性结构的链式结构 生活场景：排队
- 树状结构。一对多关系，一个父节点下面有多个子节点  生活场景：公司组织架构，族谱图
- 图形结构。多对多的关系。生活场景：地图，朋友圈都是图形结构

按照物理结构分类：

- 顺序存储结构。要求内存分配连续，如：数组    特点：查询和修改性能高，插入和删除性能低，因为需要移动元素
- 链式存储结构。不要求内存分配连续，因为查询和修改性能很低，插入和删除性能高。
- 数据索引存储结构。除建立存储结点信息外，还建立附加的索引表来标识结点的地址
- 数据散列存储结构 hash。

### 数组和链表在内存中的存储结构有什么区别？

- 数组在内存中要求连续，链表不要求
- 数组做修改查询时性能比链表更好
- 链表做增加删除性能更好，因为数组内存要求连续，每次增加删除，数组需要移位操作

### 说一下散列存储(Hash存储) ， 什么是Hash冲突 ， 有什么解决方案

- Hash冲突就是两个不同的元素计算出一个相等的hash值，即两个元素计算出同一个下标，这就导致Hash冲突

解决方案：

- 拉链法：把Hash碰撞的元素指向同一个链表  场景：HashMap
- 开放寻址法：当出现冲突的时候，以计算出的hash值为基础再进行hash计算，直到不冲突位置
- 再散列法：准备若干个hash函数，如果第一个函数出现了冲突就使用第二个函数，以此类推
- 建立公共溢出区：把Hash表分为基本表和溢出表

### 举例说说时间复杂度，比如：数组，链表，循环，嵌套循环 ， 2个非嵌套循环 ， 在什么情况下时间复杂度是什么？

- 时间复杂度，意思就是执行一个算法所花费的总时间
- 嵌套循环时间复杂度就是n的2次平方。比如第一层循环10次，第二层循环10次  总共就是100次
- n 访问数组的第 n 个元素是 O(1)  1次
- n 访问链表的第 n 个元素是 O(n)   n次  最小可能是1次  最坏的时候可能就是n次，因为链表是内存不连续的。最坏就需要循环遍历所有的元素进行比较
- 一个循环就是n次
- 2个非嵌套循环就是2n次

### JDK中线性结构的集合有哪些？

- 数组
- 链表
- 队列
- 栈

### 你说一下树形结构和线性结构的优势？

- 树形结构树是连通的，只需要一次搜索就能完成遍历

### 说一下树的分类，以及你对它们的理解（二叉查找树的优缺点，平衡树的优缺点，红黑树的优缺点，B-树的优缺点 ，B+树的优缺点）平衡树 ，红黑树

- 二叉查找树是二叉树衍生的概念，相比于其他数据结构的优势在于查找和插入的时间复杂度更低，二叉查找树是基础性数据结构，用于构建更为抽象的数据结构，如集合、多重集、关联数组等。
- 平衡二叉树：任何节点的两颗子树的高度差不大于1的二叉树就是平衡树。查询和修改性能特别高，增加和删除性能不行
- 红黑树：也是一种平衡二叉树，在平衡二叉树的基础上加了一个颜色的属性，红色和黑色。特点在于根节点和叶子节点必须是黑色。中间的节点是红色黑色相互交替的，并且从根节点到叶子节点的所有路径经过的黑色节点的树木是相同的，保证是一个平衡二叉树。红黑树就是把增删修改查询的性能进行综合了一下。hashmap就用到了红黑树
- B数是自平衡的树，能够保持数据有序。这种数据结构能够让查找数据、顺序访问、插入数据及删除的动作，都在对数时间内完成。特点是每个节点可以存储2个元素，可以超过2个子节点，拥有平衡二叉树的特点，三阶B树最多有3个分叉 ，四阶B树最多拥有4个分叉，B树比较矮，分叉越多，树越矮，IO次数越少，搜索性能越高
- B+树就是基于B树的变种，多用数据库和文件系统，B+树上的叶子结点存储关键字以及相应记录的地址，叶子结点以上各层作为索引使用，    Mysql的索引就是基于B+树实现的。特点：(1) 内部节点只存储KEY，不存储具体数据，(2) 叶子节点存储KEY和具体数据

### 有是二叉树为什么要出现多叉树

- 二叉树在大规模数据存储中，树节点元素存储的数量是有限的，如果元素数量非常多就会退化成节点内部的线性查找了，导致二叉查找树结构由于树的深度太深造成磁盘的I/O读写频繁，导致查询效率低下，而多叉树就能解决这个问题
- 常用的多叉树：B树，B+树

### b-tree和b+tree的区别？

B+树就是基于B树的变种。B+数内部节点只存储KEY，不存储具体数据，- 叶子节点存储KEY和具体数据

B+树相对于B树的优势

- 每个节点存储更多的KEY，树的高度更低，时间复杂度越小，查询越快
- 数据在叶子节点，每次查询都要查询到叶子节点，查询速度比较稳定
- 叶子节点构成构成了链表结构，方便区间查询和排序

### 说一下ES用到了什么数据结构？

- 逻辑结构：线性结构   
- 物理结构：数据索引存储结构

### 常见的算法了解几个？

- 冒泡排序，选择排序，二分查找

### 手写一个冒泡，手写一个二分查找

- 冒泡查询：从第一个元素依次与下一个元素进行比较，取出最小的那个元素放在最左边。伪代码：嵌套for循环，设计一个中间存放值的temp临时变量，每次循环进行比较，如果下标为1的元素比下标为0的元素小，就把下标为0的元素赋值给临时变量，再把下标为1的元素赋值给下标为0。最后再把临时变量的值赋给下标为1

- 二分查找：思路重要的三个参数：low 前位（下标0）   mid中位（下标：（后位+前位）/2）   after后位（下标：数组长度-1）。

  当传入参数的时候，进行比较传入的值是否等于中位的值，如果等于就查询完成了。

  如果传入的值大于中位的值，继续查找中位右边的值，前位的下标移向中位的下标+1 ，重新计算中位的下标再进行比较值

  如果传入的值小于中位的值，继续查找中位左边的值，后位的下标移向中位的下标-1，重新计算中位的下标再进行比较值

### 一个User的List集合，如何实现根据年龄排序？

- 可以让User对象实现Comparable接口，实现compareTo的方法，进行自己定义排序规则，compareTo()方法返回正数表示大，负数表示小0表示相等

- 使用Conllections工具类的sort()方法，在方法里面手动创建一个匿名内部类Comparator接口，实现compare（）方法自定义排序规则，返回正数表示大，负数表示小0表示相等

  

### HashMap底层用到了那些数据结构？

- 数组+链表+红黑树

### 为什么要用到链表结构？

- 因为解决hash冲突问题，当两个不同的元素进行存取的时候，通过hash计算出来的hash值，再经过hash值%数组长度得到该key在数组的索引位置，索引位置相同了，一山不能容二虎，造成了hash冲突问题，就要用到链表结构

### 为什么要用到红黑树？

- 当链表长度挂载的长度太长，就会造成一个性能低下问题，当链表的长度超过8时，就会转为红黑树数据结构，目的就是提高查询的性能

### 链表和红黑树在什么情况下转换的？

- 当链表的长度等于8的时候就会转换为红黑树

### HashMap在什么情况下扩容？HashMap如何扩容的？

- 扩载因子为75，当数组的长度达到扩载因子的时候就会进行2备扩容，将数组的长度x2
- 底层扩容原理就是建立一个新的数组，将老的数组的元素拷贝到新的数组中，然后再将每个元素重新计算hash值，重新获取该元素的索引位置

### HashMap是如何Put一个元素的？

- 将key进行hash计算，得到的hash值再%数组长度，得到该元素的索引位置
- 判断数组的索引位置是否有值，如果为null,就把传入的key-value包装成一个节点node，直接添加到该位置
- 如果不为null,有值，就出现hash冲突问题，那么该node后面就有一个链表或者红黑树。进行比较key是否相等，如果相等说明这个元素已经有了，就直接覆盖旧的value
- 如果不相等，就判断node的类型是不是红黑树类型，如果是就走红黑树添加的流程
- 如果不是红黑树，就使用next进行遍历链表，在遍历的时候，会一一进行比较key是否一致，如果一致就直接覆盖。
- 如果一致循环到next为null，就把传入的新元素存储在链表末尾
- 当链表的长度为8了的时候，就会变成红黑树。当在删除元素，长度为6的时候，红黑树就会变回链表结构

### HashMap是如何Get一个元素的？

- 将key进行hash计算，得到的hash值再%数组长度，得到该元素的索引位置
- 根据索引位置进行查找，如果直接查找到了就进行返回
- 如果索引位置的元素不是要查找的元素，判断node是红黑树还是链表，如果是红黑树就走红黑树的查找流程
- 如果是链表就进行next遍历，一一对比元素，直到查询到了就返回。
- 如果链表全部遍历完都没有要查找的元素，说明这个元素在map中是不存在的，就返回空null

### 什么是Hash冲突

- 当两个不同的元素进行hash计算时，得出的hash值是一样的，意味着hash计算出来的索引值也是一样的。都指向数组中同一个位置。这就说明hash冲突了

### HashMap是如何解决Hash冲突的？

- 当发现hash冲突了，就会进行以链表的形式进行存储。当链表的长度为8，链表存储方式就会变成红黑树的存储方式

### 还有哪些解决Hash冲突的方式？

- 开放寻址法   冲突的hash值再进行hash计算
- 拉链法  （HashMap）  把Hash碰撞的元素指向一个链表，HashMap用的就是这种方法
- 再散列法   准备若干个hash函数，如果使用第一个hash函数发生了冲突，就使用第二个hash函数，第二个也冲突，使用第三个
- 建立公共溢出区     把Hash表分为基本表和溢出表，把和基本表冲突的元素移到溢出表

### 你知道HahsMap死循环问题吗？

- 在jdk8已经解决了死循环问题，在jdk7及以前存在死循环问题。主要原因是因为在之前HashMap链表插入的元素使用的是头插法，当HashMap扩容后，进行元素的重新计算位置排的时候就会出现链表上元素循环指向的问题
- 比如：有链表上元素按照：A -> B -> C 顺序排列，三者Hash值相同 ， 现在HashMap扩容，然后进行元素重新Hash，A,B,C三者由于Hash值相同，在新的数组中依然会计算出相同的存储位置。而重新Hash之后变成了B -> A ，其实这里就出现了元素相互引用的问题，即：死循环

### 介绍一下Java中的集合体系

- Collection体系集合
  - List集合(有序、有下标、元素可重复)  List实现类：ArrayList、Vector、LinkedList
    - ArrayList 类（数组结构实现，查询快、增删慢； 线程不安全	）
    - Vector 类（数组、线程同步安全）数组结构实现，查询快、增删慢；
    - LinkedList 类（链表）链表结构实现，增删快，查询慢；
  - set集合(**无序、无下标、元素不可重复**（当插入新元素时，如果新元素与已有元素进行equals比较，结果为true时，则拒绝新元素插入）)
    - HashSet 类
      - 无参构建初始容量为16（负载因子75，即+75%容量扩容）
      - 底层使用的HashMap类，即将所有需要存储的值，通过HashMap去重存入
      - 先判断hashCode是否相同，再==比较地址是否相同，再equals内容是否相同
    - TreeSet 类（二叉树-自动排序）
    - LinkedHashSet 类（记录插入顺序）底层使用LinkedHashMap（链表结构）存储，节点形式独立存储数据，并可以指向下一个节点，通过顺序访问节点，可保留元素的插入顺序 - 插入顺序
- Map体系集合
  - HashMap（数组+链表+红黑树）
    - \* keySet()  // 遍历键，可以再get(key)获取value * values()  // 遍历值，只能遍历到值 * entrySet() // 遍历键值对，效率最高
  - HashTable(线程安全) 不允许null作为key或者value
  - Properties 类（配置文件读取）
  - ConcurrentHashMap 类（线程安全且高效的Map）

### 如果需要从一个List集合中频繁的删除和添加元素，是选择ArrayList还是LinkedList?为什么？

- LinkedList    因为底层基于链表实现，内存不要求连续，添加和删除只是改变指针指向的位置。而ArrayList，底层是基于数组实现的。要求内存必须连续，即如果频繁的增加和删除元素后，会将删除元素位置的后面元素向前进行移位，造成性能不好

### HashMap是否是线程安全的，如果不是，那么在多线程环境中我们应该使用哪个集合？

- 不是线程安全的。
- 可以使用ConcurrentHashmap: 底层采用分段的数组+链表实现，线程安全

### HashMap扩容机制

- HashMap的扩容阈值是75。也就是说初始化数组的长度是16，在元素达到12的时候，就会触发HashMap的扩容机制，就会新建一个HashMap，长度为之前的2倍，即32。然后将之前数组中的元素遍历取出来重新进行hash计算，重新计算元素的索引位置，然后进行存放在新建的HashMap中

### 常见的设计模式说一下，以及你用过的框架中哪儿用到这些设计模式。

创建型：

- 工厂方法模式、单例模式、建造者模式

机构型：

- 适配器模式、装饰器模式、代理模式

行为型：

- 策略模式、模板方法模式、观察者模式

spring创建bean默认的就是单例模式，AOP思想的原理就是基于动态代理，采用的就是代理模式

### 什么是单例，如何实现

- 单例就是一个类只存在一个实例，spring默认的就是单例模式
- 单例分为，懒汉模式，饿汉模式。饿汉模式，就是在加载的时候，开始就为其创建好实例对象。懒汉模式，使用的时候才为期创建实例对象

实现：

- 私有化构造器，不让外界随意new对象
- 内部提供一个静态方法来获取创建该对象的实例，此方法多次调用获取的都只是用一个实例对象

### 模板模式的作用

- 定义一个操作中的算法骨架，将一些实现步骤延迟到子类中，使得子类可以在不更改算法结构的情况下重新定义某些特定步骤。

### 什么是适配器模式

- 定义一个三方的封装类，将一个类的接口转换成客户期望的一个接口，使得原本不兼容的接口也可以一起工作。比如，电脑的充电器，中间就有一个变压器，也叫适配器。标准电压是220V，通过适配器就转换成电脑需要，支持的电压

### 什么是代理模式？有几种代理？

- 代理模式就是客户端不能直接new被代理的对象，而是通过代理对象来间接的调用实际的代理对象

分类：

- 静态代理
- JDK动态代理   
- CGLIB动态代理

### Spring使用的是哪种代理模式？

- spring的AOP实现原理就是动态代理，默认就是JDK动态代理。当代理对象是一个接口，并有对象对该接口进行了实现，那么该对象就会生成代理对象。当代理的对象不是接口就会采用CGLIB动态代理模式生成代理对象

### JDK动态代理和CGLIB动态代理的区别？

- 默认是JDK动态代理。要求必须是实现了接口的类
- 当代理的对象不是接口，就会采用CGLIG动态代理

### 哪些因素可能会造成数据库性能问题？

硬件方面：

- CPU环境太差
- 网络带宽太差

程序方面（java代码）：

- 代码写的很不好，比如多重嵌套循环查询sql

Mysql数据库方面：

- sql语句太复杂
- 使用select * 等
- join表太多
- 数据量庞大

### Mysql的执行流程是怎么样的？

- 发起请求，建立连接
- 分析sql语句
- 优化sql语句，建立执行步骤
- 执行sql

### 页面上发起的一个查询很慢，你怎么去优化

- 查看cpu使用率，网络宽带。如果cpu太差，网络宽带不行，可以进行提升
- 优化java代码
- 数据库查询慢sql 可以使用 Druid 连接池自带的功能查看慢sql，也可以使用mysql自带的指令开启慢sql日志记录。对相应查询频率特别高的字段建立索引，优化查询速度

### 优化SQL你采用什么样的优化流程？

- 对相应查询频率特别高的字段建立索引，优化查询速度
- 对数据量特别大的表可以做一些垂直分表或者水平分表
- 减少sql语句的join语句，反第三范式，建立冗余字段

### 如何去定位慢SQL

- 使用 Druid 连接池自带的功能查看慢sql

- mysql查看是否开启慢查询，show variables like 'log_slow_queries'; 

- mysql开启慢查询命令：set global log_slow_queries = on; 

- 查看慢查询存放日志，命令： show variables like 'slow_query_log_file';

  去相应目录下查看即可。

### 定位到慢SQL你如何优化？

- 查看硬件，cpu和宽带带宽，提升硬件支持
- sql语句优化，减少join，如果非要使用join尽量采用小表驱动大表
- sql语句不需要的字段不要查询出来
- 涉及批量操作的sql语句尽量使用forech
- 为查询频率高的一些字段建立索引，如果建立了索引，不要使用or >=  !=等语法，防止索引失效
- 适当加入冗余字段

### 你如何看SQL有没有命中索引？

- 查询的sql语句前面加上 explain  关键字

### mysql存储引擎有哪些，有什么区别，如何选择？

- InnoDB  支持事务，查询性能要低一点，不支持全文检索，一般使用ES作为全文检索
- MyIsam  不支持事务  查询性能高  支持全文检索
- Memory

### 一个sql ： select sum(amount) from recharge  ,来查询总充值，recharge  表数据量达到了上千万，怎么优化？

- 表中加入总充值字段
- 建立汇总表，月报表，年报表，周报表，日报表等
- 分表，建立索引等

### 什么是索引？

- 索引是加速数据库表中的数据行检索而创建的一种分散结构

### Mysql索引有哪些类型？索引方式有哪些？

- 主键索引。要求不为null且不可重复，如果没有指定主键，mysql会默认生成一个rowId作为主键索引
- 唯一索引
- 普通索引  可以重复
- 全文索引    全文索引针对MyISAM有用InnoDB不支持全文索引

索引方式：BTREE，HASH  Innoodb和Misam只支持BTREE

### Mysql的索引结构原理?为什么用B+tree

- B+Tree属于多路树，每次查询都要走到叶子节点，查询效率稳定
- 非叶子节点存储的是key，意味着可以存储多个key，减少数的高度，IO次数变少，性能更高
- 每个叶子节点存放的是key和value，并且是有序的，天然支持范围查找

### InnoDB的索引结构和MyIsam的索引结构有什么区别

- InnoDB索引的数据文件分为两个文件，数据结构文件，数据文件（包含主键索引），MyIsam索引的文件分为3个文件，数据结构文件，数据主键索引文件，数据文件
- InnoDB支持事务，MyIsam索引不支持事务
- InnoDB辅助索引存储的是主键索引的键值，MyIsam的辅助索引存储的是数据文件的地址
- InnoDB如果没有设定主键或非空唯一索引，就会自动生成一个6字节的主键，数据是主索引的一部分，附加索引保存的是主索引的值
- InnoDB支持外键，MyIsam索引不支持外键

### 哪些列不适合创建索引

- 不经常查询的字段
- 频繁增删的字段 因为更新表时，Mysql不仅保存了数据，还要保存索引文件。
- 性别这种字段不适合

### 哪些因素会造成索引失效

- sql语句中存在or  >=  != 会失效
- sql语句的where判断中存在运算
- like模糊查询，左侧使用了%  因为在组合索引中满足的是向左原则

### InnoDB辅助索引的叶子节点也存数据吗？

- 存放的是主键索引的键值，不存放数据

### 组合索引的匹配原则 ， 你优选使用单列索引和是组合索引，为什么？

- 组合索引，组合索引对覆盖索引更为支持，命中的几率更高

### 什么是Mysql主从复制

- 一个主(Master)多从(Slave)，主负责写操作，从负责读操作，从库的数据从主库同步复制，这样的集群模式就主从同步

### Mysql主从复制原理是怎么样的？

- 主从复制是通过重放binlog实现主库数据的异步复制
- 将Master的binary-log日志文件打开，mysql会把所有的DDL,DML,TCL，写入BinaryLog日志文件中
- Master会新开一个线程，用来给从库的I/O线程传binlog
- 从库的i/o线程去请求主库的binlog，并将得到的binlog日志写到中继日志（relaylog）中
- 从库的sql线程，会读取relaylog文件中的日志，并解析成具体操作，通过主从的操作一致，而达到最终数据一致

### 

### 什么是辅助索引？什么是覆盖索引

- 除主键索引外的字段创建的索引就是辅助索引
- 如果查询的字段正好包含在辅助索引节点的键值中，就不需要回表，不需要再去扫描主键索引了，叫覆盖索引

### 索引创建的原则有哪些？

- 热点数据查询居多的字段建立索引
- 频繁增加删除的字段不简历索引，因为每次增加/删除后，会额外的消耗性能去维护索引

### 什么是CAP理论 ， 哪些技术用到AP，哪些用到CP

- CAP理论，一般指的是一致性C，可用性A，分区容错性P。一般首先保证分区容错性，在C和A中选其一
- Eureka 使用的就是AP
- Redis使用的就是CP

### 什么是强一致性和最终一致性

- 强一致性：数据操作的同步的，实时的。比如注册用户，保存登录表保存用户信息表就要求强一致性，数据需要同步
- 最终一致性：只需要满足最终数据一致就可以了，不会要求多少时间。比如优惠券，积分等。

### 什么是Base理论

- Base理论就是对CAP理论的AP的一种扩展，加入最终一致性

### Mysql主从解决什么问题，不能解决什么问题？

- 解决读的高并发问题，可以接收更多的读数据请求，提高可用性
- 写数据的性能还是得不到优化，因为写数据还是在主数据库上完成的。不能防止单节点故障

### MySql主从复制原理？

- 主从复制是通过重放binlog实现主库数据的异步复制
- 将Master的binary-log日志文件打开，mysql会把所有的DDL,DML,TCL，写入BinaryLog日志文件中
- Master会新开一个线程，用来给从库的I/O线程传binlog
- 从库的i/o线程去请求主库的binlog，并将得到的binlog日志写到中继日志（relaylog）中
- 从库的sql线程，会读取relaylog文件中的日志，并解析成具体操作，通过主从的操作一致，而达到最终数据一致



### 什么是垂直分表，垂直分库，水平分表，水平分库

- 垂直分表就是对列的操作，当一个表中出现很多字段，可以通过垂直分表将一些字段单独建立一张表，通过外键进行维护关系。比如用户表中存放了用户的登录信息以及用户的基本资料，就可以把登录信息抽一张表，基本资料抽一张表。
- 垂直分库一般在分布式/微服务中使用，一般按照业务或者微服务的模块进行建立不同的数据库
- 水平分表就是对行的操作。一般用于数据量特别多的数据表中，可以按照ID的雪花算法进行分表，或者时间进行分表。比如，QQ用户表数据表多达上亿，就可以按照QQ用户的注册时间进行水平分表，分成QQ用户数据表1，QQ用户数据表2
- 水平分库：当一个数据库中进行了水平分表后，随着数据量越多，分的表也会越多，不利于维护，我们就可以将这些所有的分表再进行分库。比如A数据库中用户数据表分了100张表，我们可以进行水平分库，再建立一个B数据库，将A数据库中的后面50张表放在B数据库中。每个数据库就只有50张表了，维护起来也方便，性能也得到提升。

### 水平分库分表后会出现哪些问题？怎么解决

- 分布式事务问题
- ID重复问题     使用雪花算法，让其ID不重复，也可以单独建立一张自增长的ID表来维护分表的ID

### Mysql的集群有哪些模式？

- 一主一从
- 一主多从
- 多主多从

### 单机优化到极致了，可以怎么优化？

- 多级优化，集群，水平分库，水平分表

### 多机优化有哪些方式？

- 集群，水平分库，水平分表

### 水平分表有哪些分表规则？

- 雪花算法%2取余数确定
- 按照时间分表

### 能简单说一下你怎么使用shardingjdbc做读写分离的嘛

- 项目中导入依赖
- 配置一个propertites配置文件，里面配置master和slave主数据库和从数据库的名称以及连接的信息username和密码

### 能简单说一下你怎么使用shardingjdbc做读分库分表的嘛

- 在多个服务器安装数据库，然后设置配置，安装路径，端口等，在通过一些命令完成分库
- 分表通过雪花算法计算ID水平分表



### 什么情况下Redis集群不可用？

- redis有个16384的哈希槽位，当做了redis集群后，会平均分配到每个集群的redis中，当其中一个redis的主挂掉了，并且没有新的从能够当选主redis，此时当前redis的哈希槽位就不可用了，意味redis集群就不可用了

### Redis五大基本存储结构

- String
- list
- set
- zset
- hash



### Redis如何模拟队列和栈，用什么命令

- list存储结构的lpush,rpush 以及lpop和rpopmini队列和栈

### Redis存储单个对象怎么存，存储对象集合怎么存

- 单个对象  String
- 对象集合  hash

### 你们Redis用来做什么？使用的什么结构？

- String    验证码   登录信息
- zset    赛事排行榜   score分值排序
- hash   购物车  报名的赛事

### 统计全国高考前20名用什么？

Redis的Zrevrangebyscore命令

### 从100个VIP用户中随机抽取5名怎么做？

Redis的Srandmember命令

### 简单说一下你对分布式理解? 

- 分布式就是拆分，在微服务中的分布式就是将一个整体的应用拆分成多个子应用，这些子应用相互协调，相互通信，最终实现用户价值，缺一不可
- 有点在于易与维护，代码解耦

### 简单说一下你对集群理解? 

- 集群就是复制，将一个应用复制成多个应用，一起工作，每个应用拥有独立的完整功能
- 优点，实现高可用，提升处理并发的能力，防止单节点故障，其中一个应用即使宕机了，还有其他的应用继续服务

### 项目中那些地方用到Redis，怎么用的？ 

- 登录信息，使用Redis的String结构
- 赛事排行榜，使用Redis的Zset结构存储
- 赛事报名，使用Redis的Hash结构存储每个赛事信息

### Redis有哪些存储结构？每种结构说4个命令 

- String     set  get   
- list   lpush rpush lpop rpop
- set
- zset
- hash

### Redis怎么实现栈和队列? 

- list存储结构的lpush,rpush 以及lpop和rpopmini队列和栈

### 说一下Redis集群是怎么存储数据的? 

- 当要存储一个数据的时候，会将数据的KEY进行hash计算，得到的值再%16384得到对应的位置，然后再选择对应的Redis进行存储

### Redis内存不够了怎么办? 

- 增加物理内存
- 设置淘汰策略

### Redis集群方式有哪些? 

- 主从
- 哨兵

### 简单说一下主备切换时Redis如何选举master的？ 

- 在哨兵模式中，每个Redis都有一个哨兵，并且在哨兵会选举一个领头哨兵。哨兵会不断的ping连接Redis,查看redis的状况
- 当其中一个哨兵发现redis的master出现故障了，（主观下线：只有一个哨兵发现redis出现故障，客观下线：一半以上发现redis出现故障）领头哨兵会根据优先级->复制的命令偏离量越大（数据越完整）越优先->运行的ID较小的顺序选举新的master，选举成功后，其他的从Redis会认新选举的Redis作为master，然后从Redis会更新内部的数据

### 说一下Redis持久化方案? 

- RDB  记录数据快照的   体积相对AOF要小一点，恢复速度相对快一点，但是不保证百分百之百会持久化到文件，因为在备份的间隔时间内有数据的写入还没来及备份就宕机了，就丢失数据了
- AOF  记录数据命令的   更安全，数据更全，但是体积相对更大，恢复速度相对慢一点
- 两种一般配合使用

### 说一下Redis淘汰策略? 

- 从已经设置过期时间的数据集中淘汰最近很少使用的数据
- 从已经设置过期时间的数据集中淘汰即将要过期的数据
- 从已经设置过期时间的数据集中随机淘汰数据
- 从数据集中淘汰最近很少使用的数据
- 从数据集中随机淘汰数据
- 不设置淘汰策略

### Redis为什么那么快

- 基于内存读写操作，速度更快
- 单线程，避免上下文切换，性能更高
- I/O多路复用模型

### Redis主从有什么优缺点，哨兵有什么优缺点，cluster集群有什么优缺点？

- Redis主从：
  - 优点：提高读的请求并发量性能，读写分离
  - 从是数据的备份，防止数据丢失
  - 缺点：不能提升写的能力，不能分担写的压力
  - 主出现故障后，不能主从自动切换，主宕机了，整个就宕机了
  - 存储得不到扩容，存储数据总量是主的数据总量
- 哨兵：
  - 优点：拥有主从的所有优点
  - 主从可以自动切换，可用性更高
- cluster集群：
  - 优点：防止单节点故障
  - redis的哨兵模式基本已经可以实现高可用，读写分离 ，但是在这种模式下每台redis服务器都存储相同的数据，很浪费内存，所以在redis0上加入了cluster模式，实现的redis的分布式存储，也就是说每台redis节点上存储不同的内容。
  - 底层使用16384的长度的哈希槽，通过哈希计算出存放位置。hash(key)%16384
  - 分担写的压力了
  - 缺点：当一个redis主宕机了，并且没有从Redis作为主Redis服务了，那么就意味着这个Redis集群就不可用了，因为失去了一些hash槽位

### Redis集群有多少个槽位？它是怎么计算一个key该存储到哪个Redis节点上的？

- 16384哈希槽位
- hash(key)%16384

### 简单描述如何实现Redis集群

比如：

- 安装6台Redis服务   3个主  3个从
- 配置每台redis服务的IP端口
- java导入依赖
- 配置文件配置上每个redis服务的IP和端口
- 导入配置文件java类，配置序列化

### 为什么用ES做全文检索比数据库使用 like 快

- 倒排索引，like需要全文扫表

### ES底层用到了什么数据结构

倒排索引

### 说说你理解的ES分片(Shard)机制

- index包含多个shard分片，分片是最小工作单元
- 主分片不能与自己的从分片在一个节点
- replica shard从节点是primary shard主节点的副本，负责容错，以及承担读请求负载 - 读写分离
- primary shard的数量在创建索引的时候就固定了，replica shard的数量可以随时修改

### ES的节点有几种类型？

- 主节点    操作集群相关的内容，比如创建索引或者删除索引，以及决定哪些分片分给相关的节点
- 数据节点    存储索引数据的节点，主要对文档的增删改查，聚合操作等，数据节点对cpu,I/O要求比较高
- 负载均衡节点（协调节点）  负载分发请求路由到哪个节点，分发索引操作等



### ES内部是如何进行并发控制的

version 乐观锁

### Mysql中的数据库，表，行，列 在ES中是怎么对应的

- index  对应mysql中的数据库
- type  对应数据库中的表
- document  对应表中的一行数据
-  field   对应表中的字段

### 如果我要把一个User表中的数据存储到ES中，我应该怎么做

java操作

- 建立一个doc文档对象，类上贴上@Document(indexName = "ymjs",type = "course")注解，指定索引名，以及type
- 根据user表中的字段设计哪些字段分词，哪些字段不分词。在字段上贴@Field（type=FieldType.Keyword）  keyworld不分词，text分词
- 编写一个类去实现ElasticsearchRepository接口，然后在业务层实现存储数据业务

### 描述一下ES添加文档的过程，用到了什么算法

- 客户端请求一个协调节点coordinating node 
- 协调节点根据算法选择一个primary shard: 算法 hash(document_id) % (num_of_primary_shards)
- 对应的primary shard 所在节点保存完数据后，将数据同步到replica node。
- 协调节点coordinating node 发现 primary node 和所有 replica node 都搞定之后返回结果给客户端

Hash算法   hash(document_id) % (num_of_primary_shards)   hash计算出文档的ID%主分片的数量

### 详细描述一下Elasticsearch获取文档的过程

- 客户端请求一个协调节点coordinating node 
- coordinate node 根据算法hash(document_id) % (num_of_primary_shards)，将请求转发到对应的 node，此时会使用 round-robin随机轮询算法，在 primary shard 以及其所有 replica 中随机选择一个，让读请求负载均衡
- 接收到请求的 node 返回 document 给调节点 coordinate node。
- coordinate node 返回 document 给客户端。

### 详细描述一下Elasticsearch搜索过程

- 在初始查询阶段时，查询会广播到索引中每一个分片拷贝（主分片或者副本分片）。 

- 每个分片在本地执行搜索并构建一个匹配文档的大小为 from + size 的优先队列。PS：在搜索的时候是会查询Filesystem Cache的，但是有部分数据还在Memory Buffer，所以搜索是近实时的。

- 每个分片返回各自优先队列中所有文档的 ID 和排序值给协调节点，协调节点它合并这些值到自己的优先队列中来产生一个全局排序后的结果列表。

- 接下来就是 取回阶段，协调节点辨别出哪些文档需要被取回并向相关的分片提交多个 GET 请求。每个分片加载并 丰富 文档，如果有需要的话，接着返回文档给协调节点。一旦所有的文档都被取回了，协调节点返回结果给客户端。





### 说一下一个完整的多表JOIN查询的SQL的关键字的执行顺序（SELECT ,FROM JOIN等关键字的执行顺序）

执行顺序

 FROM  
 ON  筛选器筛选出满足ON的逻辑条件表达式，生成虚拟表2
 JOIN   连接两张表
 WHERE   条件判断
 GROUP BY  分组查询(开始使用select中的别名，后面的语句中都可以使用)
 AVG,SUM...
 HAVING
 SELECT
 ORDER BY  排序，默认升序，降序加上DESC
 LIMIT  分页查询  0,5   0代表从哪里开始查，5代表查询多少条数据
