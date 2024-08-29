# Spring6基础

**Spring6章节**





## 1.概述

笔记小结：

> 1. 含义：Spring 是一款主流的 Java EE **轻量级开源框架**，包含Spring MVC、Spring Boot、Spring Cloud等
> 2. 作用：**简化** Java 企业级应用的**开发难度**和开发周期，提供了整合其他技术和框架的能力
> 3. 简介：核心功能是**控制反转(IoC)\**和\**面向切面(AOP)**
> 4. 组成：
>    - Spring **Core**（核心容器）
>    - Spring **AOP**（面向切面编程）
>    - Spring **Data Access（**数据访问）
>    - Spring **Web**（应用程序）
>    - Spring **Message**（消息传递）
>    - Spring **test**（测试）
> 5. Spring Framework（框架）
>    1. 概述：Spring Framework是Spring项目的**核心框架**
>    2. 作用：Spring Framework**实现IOC容器**和**AOP技术**的功能模块
>    3. 特点：
>       - 非侵入式
>       - 控制反转
>       - 面向切面编程
>       - 容器
>       - 组件化
> 6. 特点：
>    - 轻：**框架轻量**级，**不依赖**其余Spring的对象
>    - 控制反转（IOC）：实现了对象之间的**松耦合**
>    - 面向切面（AOP）：**分离**应用的**业务逻辑**与**系统级服务**
>    - 容器：Spring包含并**管理应用对象的配置和生命周期**

### 1.1定义

 [Spring](https://so.csdn.net/so/search?q=Spring&spm=1001.2101.3001.7020) 是一款主流的 Java EE **轻量级开源框架** ，由于其轻便、易用和高效，被广泛应用于企业级Java应用开发中。

 Spring包含了很多子框架和扩展，如Spring [MVC](https://so.csdn.net/so/search?q=MVC&spm=1001.2101.3001.7020)、Spring Boot、Spring Cloud等。

 Spring的主要特点是IOC容器和AOP技术，它们使得Java应用的开发和管理更加简单和高效。

### 1.2作用

 Spring 目的是用于简化 Java 企业级应用的开发难度和开发周期。Spring 框架除了自己提供功能外，还提供整合其他技术和框架的能力

### 1.3简介

 自 2004 年 4 月，Spring 1.0 版本正式发布以来，Spring 已经步入到了第 6 个大版本，也就是 Spring 6。

![在这里插入图片描述](https://img-blog.csdnimg.cn/ab6950f30c86442cb45c0ad58293be7f.png#pic_center)

说明：

>  参考链接：[Spring Framework](https://spring.io/projects/spring-framework#learn)

- Spring是一个轻量级的控制反转(IoC)和面向切面(AOP)的容器框架。
- Spring最初的出现是为了解决EJB臃肿的设计，以及难以测试等问题。
- Spring为简化开发而生，让程序员只需关注核心业务的实现，尽可能的不再关注非业务逻辑代码（事务控制，安全日志等）。

### 1.4狭义和广义

- **广义的 Spring：Spring 技术栈**

 广义上的 Spring 泛指以 Spring Framework 为核心的 Spring 技术栈。

 经过十多年的发展，Spring 已经不再是一个单纯的应用框架，而是逐渐发展成为一个由多个不同子项目（模块）组成的成熟技术，例如 Spring Framework、Spring MVC、SpringBoot、Spring Cloud、Spring Data、Spring Security 等，其中 Spring Framework 是其他子项目的基础。

 这些子项目涵盖了从企业级应用开发到云计算等各方面的内容，能够帮助开发人员解决软件发展过程中不断产生的各种实际问题，给开发人员带来了更好的开发体验。

- **狭义的 Spring：Spring Framework**

 狭义的 Spring 特指 Spring Framework，通常我们将它称为 Spring 框架。

 Spring 框架是一个分层的、面向切面的 Java 应用程序的一站式[轻量级](https://so.csdn.net/so/search?q=轻量级&spm=1001.2101.3001.7020)解决方案，它是 Spring 技术栈的核心和基础，是为了解决企业级应用开发的复杂性而创建的。

Spring 有两个最核心模块： IoC 和 AOP。

- **IoC**：Inverse of Control 的简写，译为“控制反转”，指把创建对象过程交给 Spring 进行管理。
- **AOP**：Aspect Oriented Programming 的简写，译为“面向切面编程”。AOP 用来封装多个类的公共行为，将那些与业务无关，却为业务模块所共同调用的逻辑封装起来，减少系统的重复代码，降低模块间的耦合度。另外，AOP 还解决一些系统层面上的问题，比如日志、事务、权限等。

### 1.5模块组成

![在这里插入图片描述](https://img-blog.csdnimg.cn/c6811a272f494026bb22783f5a6979a3.png#pic_center)

说明：

>  上图中包含了 Spring 框架的所有模块，这些模块可以满足一切企业级应用开发的需求，在开发过程中可以根据需求有选择性地使用所需要的模块。下面分别对这些模块的作用进行简单介绍。

#### 1.5.1Spring Core（核心容器）

 spring core提供了IOC,DI,Bean配置装载创建的核心实现。核心概念： Beans、BeanFactory、BeanDefinitions、ApplicationContext。

- spring-core ：IOC和DI的基本实现
- spring-beans：BeanFactory和Bean的装配管理(BeanFactory)
- spring-context：Spring context上下文，即IOC容器(AppliactionContext)
- spring-expression：spring表达式语言

#### 1.5.2Spring AOP（面向切面编程）

- spring-aop：面向切面编程的应用模块，整合ASM，CGLib，JDK Proxy
- spring-aspects：集成AspectJ，AOP应用框架
- spring-instrument：动态Class Loading模块

#### 1.5.3Spring Data Access（数据访问）

- spring-jdbc：spring对JDBC的封装，用于简化jdbc操作
- spring-orm：java对象与数据库数据的映射框架
- spring-oxm：对象与xml文件的映射框架
- spring-jms： Spring对Java Message Service(java消息服务)的封装，用于服务之间相互通信
- spring-tx：spring jdbc事务管理

#### 1.5.4Spring Web（应用程序）

- spring-web：最基础的web支持，建立于spring-context之上，通过servlet或listener来初始化IOC容器
- spring-webmvc：实现web mvc
- spring-websocket：与前端的全双工通信协议
- spring-webflux：Spring 5.0提供的，用于取代传统java servlet，非阻塞式Reactive Web框架，异步，非阻塞，事件驱动的服务

#### 1.5.5Spring Message（消息传递）

- Spring-messaging：spring 4.0提供的，为Spring集成一些基础的报文传送服务

#### 1.5.6Spring test（测试）

- spring-test：集成测试支持，主要是对junit的封装

### 1.6Spring Framework（框架）

#### 1.6.1概述

 Spring Framework是Spring项目的核心框架，而Spring是整个Spring项目的总称，包括了Spring Framework和其他相关的子项目和扩展

![在这里插入图片描述](https://img-blog.csdnimg.cn/e2ff05d1f20742b0997bb92f047dc8e8.png#pic_center)

#### 1.6.2作用

 Spring Framework实现IOC容器和AOP技术的功能模块

 Spring Framework包含了许多模块，如Core模块、Beans模块、Context模块、AOP模块、Web模块等，每个模块都提供了不同的功能，可以灵活地选择使用。Spring Framework的目标是为了简化企业级Java开发，提高开发效率和质量。

#### 1.6.3特点

- **非侵入式**：使用 Spring Framework 开发应用程序时，Spring 对应用程序本身的结构影响非常小。对领域模型可以做到零污染；对功能性组件也只需要使用几个简单的注解进行标记，完全不会破坏原有结构，反而能将组件结构进一步简化。这就使得基于 Spring Framework 开发应用程序时结构清晰、简洁优雅。
- **控制反转**：IoC——Inversion of Control，翻转资源获取方向。把自己创建资源、向环境索取资源变成环境将资源准备好，我们享受资源注入。
- **面向切面编程**：AOP——Aspect Oriented Programming，在不修改源代码的基础上增强代码功能。
- **容器**：Spring IoC 是一个容器，因为它包含并且管理组件对象的生命周期。组件享受到了容器化的管理，替程序员屏蔽了组件创建过程中的大量细节，极大的降低了使用门槛，大幅度提高了开发效率。
- **组件化**：Spring 实现了使用简单的组件配置组合成一个复杂的应用。在 Spring 中可以使用 XML 和 Java 注解组合这些对象。这使得我们可以基于一个个功能明确、边界清晰的组件有条不紊的搭建超大型复杂应用系统。
- **一站式**：在 IoC 和 AOP 的基础上可以整合各种企业应用的开源框架和优秀的第三方类库。而且 Spring 旗下的项目已经覆盖了广泛领域，很多方面的功能性需求可以在 Spring Framework 的基础上全部使用 Spring 来实现。

### 1.7 特点

1. 轻
   - **从大小与开销两方面而言Spring都是轻量的**。完整的Spring框架可以在一个大小只有1MB多的JAR文件里发布。并且Spring所需的处理开销也是微不足道的。
   - Spring是非侵入式的：Spring应用中的对象**不依赖**于Spring的特定类。
2. 控制反转
   - Spring通过一种称作控制反转（IoC）的技术促进了**松耦合**。当应用了IoC，一个对象依赖的其它对象会通过被动的方式传递进来，而不是这个对象自己创建或者查找依赖对象。你可以认为IoC与JNDI相反——不是对象从容器中查找依赖，而是容器在对象初始化时不等对象请求就主动将依赖传递给它。
3. 面向切面
   - Spring提供了面向切面编程的丰富支持，允许通过**分离应用的业务逻辑与系统级服务**（例如审计（auditing）和事务（transaction）管理）进行内聚性的开发。应用对象只实现它们应该做的——完成业务逻辑——仅此而已。它们并不负责（甚至是意识）其它的系统级关注点，例如日志或事务支持。
4. 容器
   - Spring包含并**管理应用对象的配置和生命周期**，在这个意义上它是一种容器，你可以配置你的每个bean如何被创建——基于一个可配置原型（prototype），你的bean可以创建一个单独的实例或者每次需要时都生成一个新的实例——以及它们是如何相互关联的。然而，Spring不应该被混同于传统的重量级的EJB容器，它们经常是庞大与笨重的，难以使用。
5. 框架
   - Spring可以将简单的**组件配置**、**组合**成为复杂的**应用**。在Spring中，应用对象被声明式地组合，典型地是在一个XML文件里。Spring也提供了很多基础功能（事务管理、持久化框架集成等等），将应用逻辑的开发留给了你。

说明：

>  所有Spring的这些特征使你能够编写更干净、更可管理、并且更易于测试的代码。它们也为Spring中的各种模块提供了基础支持。

- Spring6要求JDK最低版本是JDK17

<img src="https://img-blog.csdnimg.cn/img_convert/b8ce3b19d8839f9b7761b1034c203e3d.png" alt="image-20230507141836940" style="zoom:67%;" />

## 2.基本用例-Spring框架基本使用

说明：

>  本基本用例演示，通过XML方式，实现**Bean的自动注入**

补充：环境

> - JDK：Java17+**（Spring6要求JDK最低版本是Java17）**
> - Maven：3.6+
> - Spring：6.0.2

步骤一：构建模块

- 通过Idea开发工具，创建空项目后创建子模块

<img src="https://img-blog.csdnimg.cn/img_convert/3d0ff691b67d22f2a9f5880899c62d0f.png" alt="image-20230507145548414" style="zoom: 50%;" />

说明：

>  在空项目中，创建子模块

步骤二：导入依赖

- 修改模块的`pom.xml`文件

```xml
<dependencies>
    <!--spring context依赖-->
    <!--当你引入Spring Context依赖之后，表示将Spring的基础依赖引入了-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>6.0.2</version>
    </dependency>

    <!--junit5测试-->
    <!--此依赖可选，主要便于junit进行测试使用-->
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.3.1</version>
    </dependency>
</dependencies>
1234567891011121314151617
```

说明：

>  在pom.xml文件中，添加如上依赖

补充：

> - 添加完成后，可在IDEA工具中的最右侧点击`Maven`进行查看
>
> <img src="https://img-blog.csdnimg.cn/16af0c184c39400a986ce00ca1ad52af.png#pic_center" alt="在这里插入图片描述" style="zoom: 50%;" />

步骤三：创建实体

```java
package org.example.entity;

public class User {
    public void add() {
        System.out.println("add……");
    }
}
```

说明：

>  在org.example.entity包下，创建User实体

步骤四：创建配置文件

- 在模块的`resources`目录下，创建`beans.xml`文件

说明：

>  创建`beans.xml`文件，是为了完成通过`xml`的方式实现**依赖的自动注入**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--id是该bean的唯一标识符，在整个应用程序上下文中用于获取该bean实例-->
    <!--class是该bean所属的Java类的全限定名（包括包名），它告诉Spring需要实例化哪个类-->
    <bean id="user" class="org.example.entity.User"/>
</beans>
```

说明：

> - 在beans,xml文件中，有bean标签
> - 在beans,xml文件中，bean标签有Id属性，与class属性

**步骤五：演示**

- 在模块中的`test.java`包下，创建`UserTest`类

```java
public class UserTest {
    @Test
    void newTest() {
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("beans.xml");
        User user = (User) applicationContext.getBean("user");
        user.add(); // add……
    }
}
12345678
```

补充：

> `@Test` 是 JUnit 框架中的一个注解，表示该方法是一个测试方法，会被 JUnit 框架执行。

## 3.原理

笔记小结：通过XML方式，实现Bean的自动注入的基本用例原理

> 1. 创建对象时，会调用**无参构造**方法
> 2. Spring 是通过**反射机制**调用无参构造方法**创建对象**
> 3. Spring 创建的对象（Bean对象），最终存储在**Spring容器**中

1.创建对象时，会调用**无参构造**方法

```java
public class HelloWorld {
    public HelloWorld() {
        System.out.println("无参数构造方法执行");
    }
    public void sayHello(){
        System.out.println("helloworld");
    }
}
12345678
```

说明：

> ![在这里插入图片描述](https://img-blog.csdnimg.cn/061faf16ac224d03ada17ec96b82db22.png#pic_center)

2.Spring 是通过**反射机制**调用无参构造方法创建对象

```java
// dom4j解析beans.xml文件，从中获取class属性值，类的全类名
// 通过反射机制调用无参数构造方法创建对象
Class clazz = Class.forName("com.atguigu.spring6.bean.HelloWorld");
//Object obj = clazz.newInstance();
Object object = clazz.getDeclaredConstructor().newInstance();
12345
```

3.Spring 创建的对象（Bean对象），最终存储在**Spring容器**中

```java
private final Map<String, BeanDefinition> beanDefinitionMap = new ConcurrentHashMap<>(256);
1
```

说明：

> - Spring容器底层就是一个**map集合**
> - 存储bean的map在**DefaultListableBeanFactory**类中
> - Spring容器加载到Bean类时 , 会把这个类的描述信息, 以包名加类名的方式存到**beanDefinitionMap** 中
> - Map<String,BeanDefinition> , 其中 String是Key , 默认是**类名首字母小写** 。BeanDefinition , 存的是类的定义(**描述信息)** , 我们通常叫BeanDefinition接口为 : **bean的定义对象**。![image-20230507193753242](https://img-blog.csdnimg.cn/img_convert/10b8c31578ac2252bf41ccf049fe8d14.png)

## 4.启用日志框架

笔记小结：

> 1. 概述：**Log4j2**是一个开源的Java日志框架，帮助Java开发人员在应用程序中实现灵活和可配置的日志记录
>
> 2. 组成：
>
>    - 日志信息的优先级：**TRACE < DEBUG < INFO < WARN < ERROR < FATAL**
>    - 日志信息的**输出目的地**：**控制台**或者**本地文件**
>    - 日志信息的**输出格式**：日志信息的**显示内容**
>
> 3. 基本用例：
>
>    1. 导入依赖：
>
>    ```xml
>    <!--log4j2的依赖-->
>    <dependency>
>      <groupId>org.apache.logging.log4j</groupId>
>      <artifactId>log4j-core</artifactId>
>      <version>2.19.0</version>
>    </dependency>
>    <dependency>
>      <groupId>org.apache.logging.log4j</groupId>
>      <artifactId>log4j-slf4j2-impl</artifactId>
>      <version>2.19.0</version>
>    </dependency>
>    1234567891011
>    ```
>
>    1. 创建日志配置文件：建议复制**根据需求修改**
>    2. 使用日志
>
>    ```java
>    private Logger logger = LoggerFactory.getLogger(HelloWorldTest.class);
>    ……
>    logger.info("执行成功");
>    123
>    ```
>
>    1. 结果：
>
>       ![image-20230814214839493](https://img-blog.csdnimg.cn/img_convert/de243617e723026159b33071e570b035.png)

### 4.1概述

 **Log4j2**是一个开源的Java日志框架，是Log4j的升级版。它可以帮助Java开发人员在应用程序中实现灵活和可配置的日志记录，支持异步日志记录、多线程安全等特性

### 4.2组成

1. **日志信息的优先级**，日志信息的优先级从高到低有**TRACE < DEBUG < INFO < WARN < ERROR < FATAL**

   说明：

   > 1. TRACE：追踪，是最低的日志级别，相当于追踪程序的执行
   > 2. DEBUG：调试，一般在开发中，都将其设置为最低的日志级别
   > 3. INFO：信息，输出重要的信息，使用较多
   > 4. WARN：警告，输出警告的信息
   > 5. ERROR：错误，输出错误信息
   > 6. FATAL：严重错误

2. **日志信息的输出目的地**，日志信息的输出目的地指定了日志将打印到**控制台**还是**文件中**；

3. **日志信息的输出格式**，而输出格式则控制了日志信息的显示内容。

### 4.3基本用例-Log4j2基本使用

步骤一：引入Log4j2依赖

- 修改模块中的`pom.xml`文件

```xml
<!--log4j2的依赖-->
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-core</artifactId>
    <version>2.19.0</version>
</dependency>
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-slf4j2-impl</artifactId>
    <version>2.19.0</version>
</dependency>
1234567891011
```

说明：

>  log4j的Maven使用光有核心core依赖不够，还需要有实现impl依赖

步骤二：创建日志配置文件

- 在模块文件路径在resource的根路径下，配置文件名为**log4j2.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <loggers>
        <!--
            level指定日志级别，从低到高的优先级：
                TRACE < DEBUG < INFO < WARN < ERROR < FATAL
                trace：追踪，是最低的日志级别，相当于追踪程序的执行
                debug：调试，一般在开发中，都将其设置为最低的日志级别
                info：信息，输出重要的信息，使用较多
                warn：警告，输出警告的信息
                error：错误，输出错误信息
                fatal：严重错误
        -->
        <root level="DEBUG">
            <appender-ref ref="spring6log"/>
            <appender-ref ref="RollingFile"/>
            <appender-ref ref="log"/>
        </root>
    </loggers>

    <appenders>
        <!--输出日志信息到控制台-->
        <console name="spring6log" target="SYSTEM_OUT">
            <!--控制日志输出的格式-->
            <PatternLayout pattern="%d{yyyy-MM-dd HH:mm:ss SSS} [%t] %-3level %logger{1024} - %msg%n"/>
        </console>

        <!--文件会打印出所有信息，这个log每次运行程序会自动清空，由append属性决定，适合临时测试用-->
        <File name="log" fileName="d:/spring6_log/test.log" append="false">
            <PatternLayout pattern="%d{HH:mm:ss.SSS} %-5level %class{36} %L %M - %msg%xEx%n"/>
        </File>

        <!-- 这个会打印出所有的信息，
            每次大小超过size，
            则这size大小的日志会自动存入按年份-月份建立的文件夹下面并进行压缩，
            作为存档-->
        <RollingFile name="RollingFile" fileName="d:/spring6_log/app.log"
                     filePattern="log/$${date:yyyy-MM}/app-%d{MM-dd-yyyy}-%i.log.gz">
            <PatternLayout pattern="%d{yyyy-MM-dd 'at' HH:mm:ss z} %-5level %class{36} %L %M - %msg%xEx%n"/>
            <SizeBasedTriggeringPolicy size="50MB"/>
            <!-- DefaultRolloverStrategy属性如不设置，
            则默认为最多同一文件夹下7个文件，这里设置了20 -->
            <DefaultRolloverStrategy max="20"/>
        </RollingFile>
    </appenders>
</configuration>
12345678910111213141516171819202122232425262728293031323334353637383940414243444546
```

步骤三：日常使用

- 在日常中，只用log4j2，此处创建`HelloWorldTest`使用

```java
public class HelloWorldTest {

    // 1.通过日志工程获取日志对象记录器
    private Logger logger = LoggerFactory.getLogger(HelloWorldTest.class);
 
    @Test
    public void testHelloWorld(){
        ApplicationContext ac = new ClassPathXmlApplicationContext("beans.xml");
        HelloWorld helloworld = (HelloWorld) ac.getBean("helloWorld");
        helloworld.sayHello();
        // 2.记录日志
        logger.info("执行成功");
    }
}
1234567891011121314
```

说明：

>  创建日志记录器

步骤四：演示

![image-20230507195508176](https://img-blog.csdnimg.cn/img_convert/4775f41b0937363fbb7ad10615ab3010.png)

说明：

>  当完成以上步骤后，运行，日志就会输出在控制台

## 5.容器：IoC（重点）

笔记小结：见各个小节

### 5.1概述

笔记小结：

> 1. 定义：IoC (Inversion of Control)，即控制反转，是一种设计模式或者说**设计思想**
> 2. 简介：Spring 通过 IoC 容器来**管理**所有 **Java 对象的实例化和初始化**，控制对象与对象之间的依赖关系
> 3. 作用：通过容器来**管理对象**的**创建、销毁、依赖注入**等操作，而应用程序本身只需要使用这些对象即可
> 4. 依赖注入:
>    - 含义：以**解耦**对象之间的依赖关系
>    - 作用：Spring通过依赖注入的方式来完成Bean管理的。换句话说，依赖注入，依赖注入**实现**了控制反转的思想
>    - 实现方式（重点）：
>      1. **setter注入**
>      2. **构造注入**
> 5. 实现接口以及常用类：
>    - **BeanFactory**接口：面向 Spring 本身，不提供给开发人员使用
>    - **ApplicationContext**接口：面向 Spring 的使用者，几乎所有场合（创建、管理Bean实例，支持国际化、资源访问、消息传递）都适用
>    - 常用类：
>      - **FileSystemXmlApplicationContext**：通过**文件系统路径**读取 XML 格式的配置文件创建 IOC 容器对象
>      - **ClassPathXmlApplicationContext**：通过读取**类路径**下的 XML 格式的配置文件创建 IOC 容器对象

#### 5.1.1定义

 IoC (Inversion of Control)，即控制反转，是一种设计模式或者说**设计思想**，它是面向对象编程中的一种概念，用来描述对象之间的依赖关系，指导我们如何设计出松耦合、更优良的程序。

#### 5.1.2简介

 Spring 通过 IoC 容器来管理所有 Java 对象的实例化和初始化，控制对象与对象之间的依赖关系。我们将由 IoC 容器管理的 Java 对象称为 Spring Bean，它与使用关键字 new 创建的 Java 对象没有任何区别。

#### 5.1.3作用

 在 IoC 模式中，**控制权从程序代码中转移到了容器中**，即通过容器来管理对象的创建、销毁、依赖注入等操作，而应用程序本身只需要使用这些对象即可。这样，应用程序就不需要自己管理**对象之间的依赖关系**，而是由容器来管理，从而**实现了代码的解耦和更好的可维护性**，提高程序扩展力。

说明：

> - 将对象的创建权利交出去，交给第三方容器负责
> - 将对象和对象之间关系的维护权交出去，交给第三方容器负责

#### 5.1.4依赖注入

##### 5.1.4.1定义

 依赖注入（Dependency Injection，DI）是一种**设计模式**，其主要思想是在程序运行的过程中，通过外部容器（如Spring容器）动态地将依赖对象注入到程序中，以解耦对象之间的依赖关系，从而提高程序的灵活性、可维护性和可测试性。

##### 5.1.4.2作用

 **Spring通过依赖注入的方式来完成Bean管理的。**换句话说，依赖注入，依赖注入实现了控制反转的思想。依赖指的是对象和对象之间的关联关系。注入指的是一种数据传递行为，通过注入行为来让对象和对象产生关系。

补充：

>  Bean管理说的是：Bean对象的创建，以及Bean对象中属性的赋值（或者叫做Bean对象之间关系的维护）。

##### 5.1.4.3实现方式

- 第一种：set注入
- 第二种：构造注入

#### 5.1.5实现

 Spring 的框架中，IoC 容器是通过 **BeanFactory** 和 **ApplicationContext** 接口实现的。BeanFactory 接口是 Spring 框架最底层的接口，提供了基本的 IoC 功能；ApplicationContext 接口是 BeanFactory 接口的子接口，提供了更高级的特性和功能，如 AOP、国际化、事件驱动等。其中BeanFactory 接口，最重要的方法是getBean()方法，用于从容器中获取对象。

 Spring 的 IoC 容器就是 IoC思想的一个落地的产品实现。IoC容器中管理的组件也叫做 bean。在创建 bean 之前，首先需要创建IoC 容器。Spring 提供了IoC 容器的两种实现方式：

- BeanFactory：这是 IoC 容器的基本实现，是 Spring 内部使用的接口。面向 Spring 本身，不提供给开发人员使用。
- ApplicationContext：BeanFactory 的子接口，提供了更多高级特性。面向 Spring 的使用者，几乎所有场合都使用 ApplicationContext 而不是底层的 BeanFactory

**ApplicationContext的主要实现类**:

| 类型名                          | 简介                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| ClassPathXmlApplicationContext  | 通过读取类路径下的 XML 格式的配置文件创建 IOC 容器对象       |
| FileSystemXmlApplicationContext | 通过文件系统路径读取 XML 格式的配置文件创建 IOC 容器对象     |
| ConfigurableApplicationContext  | ApplicationContext 的子接口，包含一些扩展方法 refresh() 和 close() ，让 ApplicationContext 具有启动、关闭和刷新上下文的能力。 |
| WebApplicationContext           | 专门为 Web 应用准备，基于 Web 环境创建 IOC 容器对象，并将对象引入存入 ServletContext 域中。 |

![image-20230507205115192](https://img-blog.csdnimg.cn/img_convert/95bf03c0abca280424b866bf38d33ea3.png)

说明：

>  ApplicationContext有众多的实现类，其中最常用的就是ClassPathXmlApplicationContext与FileSystemXmlApplicationContext实现类

### 5.2基于XML管理Bean（了解）

笔记小结：

> 1. 获取Bean的方式：
>
>    - 根据**ID**：
>
>      ```java
>      User user = (User) applicationContext.getBean("user");
>      1
>      ```
>
>    - 根据**类型**：
>
>      ```
>       User user = (User) applicationContext.getBean(User.class);
>      1
>      ```
>
>    - 根据**Id和类型**:
>
>      ```java
>      User user = (User) applicationContext.getBean("user", User.class);
>      1
>      ```
>
> 2. 依赖注入
>
>    - 根据**Setter**注入：`<property/>`
>    - 根据**构造器**注入：`<constructor-arg/>`
>
> 3. 特殊值处理
>
>    - **字面量**赋值`<property>`
>    - **Null**值`<null>`
>    - Xml**实体**：属性值`value="a < b"`
>    - **CDATA节**：标签内容`<![CDATA[a < b]]>`
>
> 4. 注入对象类型属性值
>
>    1. **引用外部Bean**：属性`ref`
>    2. **引用内部Bean**：bean嵌套
>    3. **级联属性赋值**：引入对象后，级联赋值`name="clazz.clazzId"`
>
> 5. 注入**数组类型**属性值：`<array></array>`
>
> 6. 注入**集合类型**属性值：
>
>    1. 注入**List集合类型**属性值：` <list> </list>`
>
>    2. 注入**Map集合类型**属性值：`<map><entry><<key>/key><value></value></entry></map>`
>
>    3. 注入
>
>       引用集合类型
>
>       属性值：
>
>       ```
>       <util></util>
>       ```
>
>       - 注意：使用前，需要引入util命名空间
>
> 7. 引入P命名空间属性值：属性`p:`
>
>    - 注意：使用前，需要引入p命名空间
>
> 8. 引入**外部属性**文件：`<context:property-placeholder location="classpath:jdbc.properties"/>`
>
> 9. 引入**Bean的作用域**：属性`scope`属性值`prototype（多例）、singleton（单例）`
>
> 10. Bean的生命周期：
>
>     1. bean**对象创建**（调用无参构造器）
>     2. bean**对象设置属性**
>     3. bean的**后置处理器**（初始化之前）
>     4. bean**对象初始化**（需在配置bean时指定初始化方法）
>     5. bean的**后置处理器**（初始化之后）
>     6. bean**对象就绪可以使用**
>     7. bean**对象销毁**（需在配置bean时指定销毁方法）
>     8. IOC**容器关闭**
>
> 11. 引入FactoryBean属性值：实现`FactoryBean<T>`接口
>
> 12. 引入**自动装配**：属性值`autowire`属性值`byType、byName`

#### 5.2.1获取Bean的方式

##### 5.2.1.1根据ID获取Bean

```java
public class UserTest {
    @Test
    void newTest() {
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("beans.xml");
        User user = (User) applicationContext.getBean("user");
        user.add(); // add……
    }
}
12345678
```

说明：

>  此获取方式，需要基于第2.基本用例进行查看

##### 5.2.1.2根据类型获取Bean

```java
public class UserTest {
    @Test
    void newTest() {
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("beans.xml");
        User user = (User) applicationContext.getBean(User.class);
        user.add(); // add……
    }
}
12345678
```

注意：

> - 当根据类型获取bean时，要求IOC容器中指定类型的bean有且只能有一个
>
> - ```java
>   org.springframework.beans.factory.NoUniqueBeanDefinitionException: No qualifying bean of type 'com.atguigu.spring6.bean.HelloWorld' available: expected single matching bean but found 2: helloworldOne,helloworldTwo
>   1
>   ```

说明：

>  此获取方式，需要基于第2.基本用例进行查看

##### 5.2.1.3根据Id和类型获取Bean

```java
public class UserTest {
    @Test
    void newTest() {
        ApplicationContext applicationContext = new ClassPathXmlApplicationContext("beans.xml");
        User user = (User) applicationContext.getBean("user", User.class);
        user.add(); // add……
    }
}
12345678
```

补充：

>  如果组件类实现了接口，可以根据接口类型获取Bean，但前提是Bean唯一

说明：

>  此获取方式，需要基于第2.基本用例进行查看

#### 5.2.2依赖注入

##### 5.2.2.1根据setter注入

步骤一：创建学生类Student

```java
package com.atguigu.spring6.bean;

public class Student {

    private Integer id;

    private String name;

    private Integer age;

    private String sex;

    public Student() {
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", age=" + age +
                ", sex='" + sex + '\'' +
                '}';
    }

}
12345678910111213141516171819202122232425262728293031323334353637383940414243444546474849505152535455565758
```

步骤二：配置bean时为属性赋值

```xml
<bean id="studentOne" class="com.atguigu.spring6.bean.Student">
    <!-- property标签：通过组件类的setXxx()方法给组件对象设置属性 -->
    <!-- name属性：指定属性名（这个属性名是getXxx()、setXxx()方法定义的，和成员变量无关） -->
    <!-- value属性：指定属性值 -->
    <property name="id" value="1001"></property>
    <property name="name" value="张三"></property>
    <property name="age" value="23"></property>
    <property name="sex" value="男"></property>
</bean>
123456789
```

说明：

>  当使用标签标签完成对象的属性创建时，name需要跟对象中的成员变量同名

步骤三：演示

```java
@Test
public void testDIBySet(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("spring-di.xml");
    Student studentOne = ac.getBean("studentOne", Student.class);
    System.out.println(studentOne);
}
123456
```

说明：

>  当打印输出是，由于基于XML根据Setter注入方式进行对象的创建，此时输出可获得成员方法tostring的内容

##### 5.2.2.2根据构造器注入

步骤一：在基于根据setter注入的基础上，在Student类中添加有参构造

```java
public Student(Integer id, String name, Integer age, String sex) {
    this.id = id;
    this.name = name;
    this.age = age;
    this.sex = sex;
}
123456
```

步骤二：配置bean

```xml
<bean id="studentTwo" class="com.atguigu.spring6.bean.Student">
    <constructor-arg name="id" value="1002"></constructor-arg>
    <constructor-arg name="name" value="李四"></constructor-arg>
    <constructor-arg name="age"value="33"></constructor-arg>
    <constructor-arg name="sex" value="女"></constructor-arg>
</bean>
123456
```

说明：

> - constructor-arg标签属性描述构造器参数：
>   - index属性：指定参数所在位置的索引（从0开始）
>   - name属性：指定参数名，name需要跟对象中的成员变量同名

步骤三：演示

```java
@Test
public void testDIByConstructor(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("spring-di.xml");
    Student studentOne = ac.getBean("studentTwo", Student.class);
    System.out.println(studentOne);
}
123456
```

说明：

>  当打印输出是，由于基于XML根据构造器注入方式进行对象的创建，此时输出可获得成员方法tostring的内容

#### 5.2.3特殊值处理

##### 5.2.3.1字面量赋值

```xml
<!-- 使用value属性给bean的属性赋值时，Spring会把value属性的值看做字面量 -->
<property name="name" value="张三"/>
12
```

##### 5.2.3.2null值

```xml
<property name="name">
    <null />
</property>
123
```

细节：

> ```xml
> <property name="name" value="null"></property>
> 1
> ```
>
> 以上写法，为name所赋值为字符串null

##### 5.2.3.3xml实体

```xml
<!-- 解决方案一：使用XML实体来代替 -->
<property name="expression" value="a &lt; b"/>
12
```

说明：

>  小于号在XML文档中用来定义标签的开始，不能随便使用

##### 5.2.3.4CDATA节

```xml
<property name="expression">
    <!-- 解决方案二：使用CDATA节 -->
    <value><![CDATA[a < b]]></value>
</property>
1234
```

说明：

> - CDATA中的C代表Character，是文本、字符的含义，CDATA就表示纯文本数据
> - ML解析器看到CDATA节就知道这里是纯文本，就不会当作XML标签或属性来解析
> - 所以CDATA节中写什么符号都随意

#### 5.2.4注入对象类型属性值

##### 5.2.4.1引用外部Bean

步骤一：配置Clazz类型的bean

```xml
<bean id="clazzOne" class="com.atguigu.spring6.bean.Clazz">
    <property name="clazzId" value="1111"></property>
    <property name="clazzName" value="财源滚滚班"></property>
</bean>
1234
```

步骤二：为Student中的clazz属性赋值

```xml
<bean id="studentFour" class="com.atguigu.spring6.bean.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
    <property name="clazz" ref="clazzOne"></property>
</bean>
12345678
```

说明：

>  当引用外部对象时，需要将ref属性变为Value属性。ref属性，值表示引用对象、value属性，值表示字符串

##### 5.2.4.2引用内部Bean

步骤一：在引用外部Bean的基础上

```xml
<bean id="studentFour" class="com.atguigu.spring6.bean.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <property name="clazz">
        <!-- 在一个bean中再声明一个bean就是内部bean -->
        <!-- 内部bean只能用于给属性赋值，不能在外部通过IOC容器获取，因此可以省略id属性 -->
        <bean id="clazzInner" class="com.atguigu.spring6.bean.Clazz">
            <property name="clazzId" value="2222"></property>
            <property name="clazzName" value="远大前程班"></property>
        </bean>
    </property>
</bean>
1234567891011121314
```

说明：

>  将Bean写于属性标签内，即为引用内部Bean

##### 5.2.4.3级联属性赋值

步骤一：在引用内部Bean的基础上

```xml
<bean id="studentFour" class="com.atguigu.spring6.bean.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <property name="clazz" ref="clazzOne"></property>
    <property name="clazz.clazzId" value="3333"></property>
    <property name="clazz.clazzName" value="最强王者班"></property>
</bean>
123456789
```

#### 5.2.5注入数组类型属性值

步骤一：在Student类中中添加成员变量数组和getter于setter方法

```java
private String[] hobbies;

public String[] getHobbies() {
    return hobbies;
}

public void setHobbies(String[] hobbies) {
    this.hobbies = hobbies;
}
123456789
```

步骤二：配置Bean

```xml
<bean id="studentFour" class="com.atguigu.spring.bean6.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
    <property name="clazz" ref="clazzOne"></property>
    <property name="hobbies">
        <array>
            <value>抽烟</value>
            <value>喝酒</value>
            <value>烫头</value>
        </array>
    </property>
</bean>
123456789101112131415
```

说明：

>  当注入数组类型数据时，需要使用标签

#### 5.2.6注入集合类型属性值

##### 5.2.6.1注入List集合类型属性值

步骤一：在Clazz类中添加添加成员变量集合和getter于setter方法

```java
private List<Student> students;

public List<Student> getStudents() {
    return students;
}

public void setStudents(List<Student> students) {
    this.students = students;
}
123456789
```

步骤二：配置Bean

```xml
<bean id="clazzTwo" class="com.atguigu.spring6.bean.Clazz">
    <property name="clazzId" value="4444"></property>
    <property name="clazzName" value="Javaee0222"></property>
    <property name="students">
        <list>
            <ref bean="studentOne"></ref>
            <ref bean="studentTwo"></ref>
            <ref bean="studentThree"></ref>
        </list>
    </property>
</bean>
1234567891011
```

说明：

>  当注入List集合类型数据时，需要使用标签

细节：

>  因为List students，List集合中引用的是Student对象，因此注入时需要使用标签，进行引用对象

##### 5.2.6.2注入Map集合类型属性值

步骤一：创建Student类

```java
package com.atguigu.spring6.bean;
public class Teacher {

    private Integer teacherId;

    private String teacherName;

    public Integer getTeacherId() {
        return teacherId;
    }

    public void setTeacherId(Integer teacherId) {
        this.teacherId = teacherId;
    }

    public String getTeacherName() {
        return teacherName;
    }

    public void setTeacherName(String teacherName) {
        this.teacherName = teacherName;
    }

    public Teacher(Integer teacherId, String teacherName) {
        this.teacherId = teacherId;
        this.teacherName = teacherName;
    }

    public Teacher() {

    }
    
    @Override
    public String toString() {
        return "Teacher{" +
                "teacherId=" + teacherId +
                ", teacherName='" + teacherName + '\'' +
                '}';
    }
}
12345678910111213141516171819202122232425262728293031323334353637383940
```

步骤二：在Student类中添加添加成员变量集合和getter于setter方法

```java
private Map<String, Teacher> teacherMap;

public Map<String, Teacher> getTeacherMap() {
    return teacherMap;
}

public void setTeacherMap(Map<String, Teacher> teacherMap) {
    this.teacherMap = teacherMap;
}
123456789
```

步骤三：配置bean

```xml
<bean id="teacherOne" class="com.atguigu.spring6.bean.Teacher">
    <property name="teacherId" value="10010"></property>
    <property name="teacherName" value="大宝"></property>
</bean>

<bean id="teacherTwo" class="com.atguigu.spring6.bean.Teacher">
    <property name="teacherId" value="10086"></property>
    <property name="teacherName" value="二宝"></property>
</bean>

<bean id="studentFour" class="com.atguigu.spring6.bean.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
    <property name="clazz" ref="clazzOne"></property>
    <property name="hobbies">
        <array>
            <value>抽烟</value>
            <value>喝酒</value>
            <value>烫头</value>
        </array>
    </property>
    <property name="teacherMap">
        <map>
            <entry>
                <key>
                    <value>10010</value>
                </key>
                <ref bean="teacherOne"></ref>
            </entry>
            <entry>
                <key>
                    <value>10086</value>
                </key>
                <ref bean="teacherTwo"></ref>
            </entry>
        </map>
    </property>
</bean>
1234567891011121314151617181920212223242526272829303132333435363738394041
```

说明：

> - 当注入Map集合类型数据时，需要使用标签
> - 需要使用表示键值对
> - 需要使用表示键

细节：

>  因为Map<String, Teacher> teacherMap，Map集合中引用的是Teacher对象，因此注入时需要使用标签，进行引用对象

##### 5.2.6.2注入引用集合类型属性值

步骤一：配置对应的命名空间

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:util="http://www.springframework.org/schema/util"
    xsi:schemaLocation="http://www.springframework.org/schema/util
    http://www.springframework.org/schema/util/spring-util.xsd
    http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">
12345678
```

步骤二：配置Bean

```xml
<!--list集合类型的bean-->
<util:list id="students">
    <ref bean="studentOne"></ref>
    <ref bean="studentTwo"></ref>
    <ref bean="studentThree"></ref>
</util:list>
<!--map集合类型的bean-->
<util:map id="teacherMap">
    <entry>
        <key>
            <value>10010</value>
        </key>
        <ref bean="teacherOne"></ref>
    </entry>
    <entry>
        <key>
            <value>10086</value>
        </key>
        <ref bean="teacherTwo"></ref>
    </entry>
</util:map>
<bean id="clazzTwo" class="com.atguigu.spring6.bean.Clazz">
    <property name="clazzId" value="4444"></property>
    <property name="clazzName" value="Javaee0222"></property>
    <property name="students" ref="students"></property>
</bean>
<bean id="studentFour" class="com.atguigu.spring6.bean.Student">
    <property name="id" value="1004"></property>
    <property name="name" value="赵六"></property>
    <property name="age" value="26"></property>
    <property name="sex" value="女"></property>
    <!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
    <property name="clazz" ref="clazzOne"></property>
    <property name="hobbies">
        <array>
            <value>抽烟</value>
            <value>喝酒</value>
            <value>烫头</value>
        </array>
    </property>
    <property name="teacherMap" ref="teacherMap"></property>
</bean>
123456789101112131415161718192021222324252627282930313233343536373839404142
```

说明：

> - 使用标签，可以将List集合或者Map集合的属性注入变为引用的方式
> - 在使用util标签时，需要引入相应的命名空间

#### 5.2.7引入P命名空间属性值

步骤一：引入P命名空间

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:util="http://www.springframework.org/schema/util"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/util
       http://www.springframework.org/schema/util/spring-util.xsd
       http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd">
123456789
```

步骤二：通过p命名空间方式为bean的各个属性赋值

```xml
<bean id="studentSix" class="com.atguigu.spring6.bean.Student"
    p:id="1006" p:name="小明" p:clazz-ref="clazzOne" p:teacherMap-ref="teacherMap"></bean>
12
```

说明：

>  通过`p:成员属性`，即可完成各个属性的赋值.

#### 5.2.8引入外部属性文件

步骤一：添加依赖

```xml
 <!-- MySQL驱动 -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.30</version>
</dependency>

<!-- 数据源 -->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>1.2.15</version>
</dependency>
12345678910111213
```

步骤二：创建外部属性文件

```properties
jdbc.user=root
jdbc.password=atguigu
jdbc.url=jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC
jdbc.driver=com.mysql.cj.jdbc.Driver
1234
```

说明：

>  在resources文件下创建jdbc.properties文件

步骤三：引入属性文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd
                           http://www.springframework.org/schema/context
                           http://www.springframework.org/schema/context/spring-context.xsd">
    <!-- 引入外部属性文件 -->
    <context:property-placeholder location="classpath:jdbc.properties"/>
</beans>
1234567891011
```

注意：

>  在使用 `<context:property-placeholder> `元素加载外包配置文件功能前，首先需要在 XML 配置的一级标签 中添加 **context** 相关的约束。

步骤四：配置Bean

```xml
<!--完成数据库信息注入-->
<bean id="druidDataSource" class="com.alibaba.druid.pool.DruidDataSource">
    <property name="url" value="${jdbc.url}"/>
    <property name="driverClassName" value="${jdbc.driver}"/>
    <property name="username" value="${jdbc.user}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>
1234567
```

说明：

>  取外部文件中的值时，需要根据外部文件中属性的名字，可以把相应值取得

步骤五：演示

```java
@Test
public void testDataSource() throws SQLException {
    ApplicationContext ac = new ClassPathXmlApplicationContext("spring-datasource.xml");
    DataSource dataSource = ac.getBean(DruidDataSource.class);
    Connection connection = dataSource.getConnection();
    System.out.println(connection);
}
1234567
```

#### 5.2.9引入Bean的作用域

步骤一：创建类User

```java
package com.atguigu.spring6.bean;
public class User {

    private Integer id;

    private String username;

    private String password;

    private Integer age;

    public User() {
    }

    public User(Integer id, String username, String password, Integer age) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.age = age;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", age=" + age +
                '}';
    }
}
123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263
```

步骤二：配置bean

```xml
<!-- scope属性：取值singleton（默认值），bean在IOC容器中只有一个实例，IOC容器初始化时创建对象 -->
<!-- scope属性：取值prototype，bean在IOC容器中可以有多个实例，getBean()时创建对象 -->
<bean class="com.atguigu.spring6.bean.User" scope="prototype"></bean>
123
```

说明：

> - 属性值：
>   - singleton（默认），在IOC容器中，这个bean的对象始终为单实例，当IOC容器初始化时即可创建对象
>   - prototype，在IOC容器中，这个bean在IOC容器中有多个实例，当 获取bean时可创建对象

步骤三：演示

```java
@Test
public void testBeanScope(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("spring-scope.xml");
    User user1 = ac.getBean(User.class);
    User user2 = ac.getBean(User.class);
    System.out.println(user1==user2);
}
1234567
```

#### 5.2.10Bean的生命周期

流程

1. bean对象创建（调用无参构造器）
2. bean对象设置属性
3. bean的后置处理器（初始化之前）
4. bean对象初始化（需在配置bean时指定初始化方法）
5. bean的后置处理器（初始化之后）
6. bean对象就绪可以使用
7. bean对象销毁（需在配置bean时指定销毁方法）
8. IOC容器关闭

步骤一：修改User类

```java
public class User {

    private Integer id;

    private String username;

    private String password;

    private Integer age;

    public User() {
        System.out.println("生命周期：1、创建对象");
    }

    public User(Integer id, String username, String password, Integer age) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.age = age;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        System.out.println("生命周期：2、依赖注入");
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    public void initMethod(){
        System.out.println("生命周期：3、初始化");
    }

    public void destroyMethod(){
        System.out.println("生命周期：5、销毁");
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", password='" + password + '\'' +
                ", age=" + age +
                '}';
    }
}
123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172
```

说明：

>  其中的initMethod()和destroyMethod()，可以通过配置Bean指定为初始化和销毁的方法

步骤二：创建Bean 的后置处理器

```java
package com.atguigu.spring6.process;
    
import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;

public class MyBeanProcessor implements BeanPostProcessor {
    
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("☆☆☆" + beanName + " = " + bean);
        return bean;
    }
    
    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("★★★" + beanName + " = " + bean);
        return bean;
    }
}
12345678910111213141516171819
```

注意：

>  bean的后置处理器会在生命周期的初始化前后添加额外的操作，需要实现BeanPostProcessor接口，且配置到IOC容器中，需要注意的是，bean后置处理器不是单独针对某一个bean生效，而是针对IOC容器中所有bean都会执行

步骤三：配置Bean

```xml
<!-- 使用init-method属性指定初始化方法 -->
<!-- 使用destroy-method属性指定销毁方法 -->
<bean class="com.atguigu.spring6.bean.User" scope="prototype" init-method="initMethod" destroy-method="destroyMethod">
    <property name="id" value="1001"></property>
    <property name="username" value="admin"></property>
    <property name="password" value="123456"></property>
    <property name="age" value="23"></property>
</bean>
<!-- bean的后置处理器要放入IOC容器才能生效 -->
<bean id="myBeanProcessor" class="com.atguigu.spring6.process.MyBeanProcessor"/>
12345678910
```

说明：

> - 在配置Bean时，需要使用init-method属性和destroy-method属性进行配置Bean的初始化方法与销毁的方法
> - 在配置Bean时，需要将Bean的后置处理器放入IOC容器才能生效

步骤四：演示

```java
@Test
public void testLife(){
    ClassPathXmlApplicationContext ac = new ClassPathXmlApplicationContext("spring-lifecycle.xml");
    User bean = ac.getBean(User.class);
    System.out.println("生命周期：4、通过IOC容器获取bean并使用");
    ac.close();
}
1234567
```

#### 5.2.11引入FactoryBean属性值

![在这里插入图片描述](https://img-blog.csdnimg.cn/534b25c1656848e4943d37e1af1f2a7c.png#pic_center)

说明：

>  FactoryBean是Spring提供的一种整合第三方框架的常用机制。和普通的bean不同，配置一个FactoryBean类型的bean，在获取bean的时候得到的并不是class属性中配置的这个类的对象，而是getObject()方法的返回值。通过这种机制，Spring可以帮我们把复杂组件创建的详细过程和繁琐细节都屏蔽起来，只把最简洁的使用界面展示给我们。

步骤一 ：创建类UserFactoryBean

```java
package com.atguigu.spring6.bean;
public class UserFactoryBean implements FactoryBean<User> {
    @Override
    public User getObject() throws Exception {
        return new User();
    }

    @Override
    public Class<?> getObjectType() {
        return User.class;
    }
}
123456789101112
```

步骤二：配置bean

```xml
<bean id="user" class="com.atguigu.spring6.bean.UserFactoryBean"></bean>
1
```

步骤三：演示

```java
@Test
public void testUserFactoryBean(){
    //获取IOC容器
    ApplicationContext ac = new ClassPathXmlApplicationContext("spring-factorybean.xml");
    User user = (User) ac.getBean("user");
    System.out.println(user);
}
1234567
```

说明：

>  此时获取到的容器对象，并不是UserFactoryBean，而是User

#### 5.2.12引入xml自动装配

步骤一：环境准备

1.创建UserController类

```java
package com.atguigu.spring6.autowire.controller
public class UserController {

    private UserService userService;

    public void setUserService(UserService userService) {
        this.userService = userService;
    }

    public void saveUser(){
        userService.saveUser();
    }

}
1234567891011121314
```

2.创建UserService接口

```java
package com.atguigu.spring6.autowire.service
public interface UserService {

    void saveUser();

}
123456
```

3.创建UserServiceImpl类实现UserService接口

```java
package com.atguigu.spring6.autowire.service.impl
public class UserServiceImpl implements UserService {

    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public void saveUser() {
        userDao.saveUser();
    }

}
123456789101112131415
```

4.创建UserDao接口

```java
package com.atguigu.spring6.autowire.dao
public interface UserDao {

    void saveUser();

}
123456
```

5.创建UserDaoImpl类实现UserDao接口

```java
package com.atguigu.spring6.autowire.dao.impl
public class UserDaoImpl implements UserDao {

    @Override
    public void saveUser() {
        System.out.println("保存成功");
    }

}
123456789
```

步骤二：配置bean

```xml
<bean id="userController" class="com.atguigu.spring6.autowire.controller.UserController" autowire="byType"></bean>

<bean id="userService" class="com.atguigu.spring6.autowire.service.impl.UserServiceImpl" autowire="byType"></bean>

<bean id="userDao" class="com.atguigu.spring6.autowire.dao.impl.UserDaoImpl"></bean>
12345
```

说明：

> - 当使用Bean标签的autowire属性是，通过byType的方式进行自动装配
> - byType：根据类型匹配IOC容器中的某个兼容类型的bean，为属性自动赋值
>   - 若在IOC中，**没有**任何一个兼容类型的bean能够为属性赋值，则该**属性不装配**，即值为默认值**null**
>   - 若在IOC中，有**多个**兼容类型的bean能够为属性赋值，则**抛出异常**NoUniqueBeanDefinitionException
> - byName：将自动装配的属性的属性名，作为bean的id在IOC容器中匹配相对应的bean进行赋值

步骤三：演示

```java
@Test
public void testAutoWireByXML(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("autowire-xml.xml");
    UserController userController = ac.getBean(UserController.class);
    userController.saveUser();
}
123456
```

说明：

>  当使用标签中的属性时，使用Autowire属性使用byType的方式即可实现属性的自动注入

### 5.3基于注解管理Bean（重点）

笔记小结：

> 1. 概述：
>
>    - 简介：Java 增加了对**注解**（Annotation）的支持，它是代码中的一种特殊标记，可以在**编译、类加载和运行时被读取**，执行相应的处理。
>    - 使用注解：
>      1. @Component：表示**泛化组件**
>      2. @Repository：表示**数据访问层组件**
>      3. @Service：表示**业务层组件**
>      4. @Controller：：表示**控制层组件**
>
> 2. 开启组件扫描
>
>    1. 概述：通过 `<context:component-scan> `元素开**启 Spring Beans的自动扫描功能**。Spring 会自动从**扫描指定的包**（base-package 属性设置）及其子包下的所有类，如果类上使用了 @Component 注解，就将该类装配到容器中
>
>    2. 基本用例：使用
>
>       标签
>
>       ```
>       <context:component-scan></context:component-scan>
>       ```
>
>       1. 添加conentt约束
>       2. 开启扫描方式
>
>    3. 指定要**排除**的组件：` <context:exclude-filter></context:exclude-filter>`
>
>    4. 仅扫描**指定**组件：` <context:include-filter></context:include-filter`
>
> 3. 使用注解定义Bean
>
>    1. 使用`@Autowired`注入：
>
>       - **属性**注入
>
>         ```java
>         @Autowired
>         private UserDao userDao;
>         12
>         ```
>
>       - **setter**注入
>
>         ```java
>         private UserDao userDao;
>         @Autowired
>         public void setUserDao(UserDao userDao) {
>             this.userDao = userDao;
>         }
>         12345
>         ```
>
>       - **构造方法**注入
>
>         ```java
>         private UserDao userDao;
>         @Autowired
>         public UserServiceImpl(UserDao userDao) {
>         	this.userDao = userDao;
>         }
>         12345
>         ```
>
>       - **形参**注入
>
>         ```java
>         private UserDao userDao;
>         public UserServiceImpl(@Autowired UserDao userDao) {
>             this.userDao = userDao;
>         }
>         1234
>         ```
>
>       - **无注解**注入：当构造函数**仅有一个需要注入的构造参数**时，@Autowired可以省略
>
>         ```java
>         private UserDao userDao;
>         public UserServiceImpl(UserDao userDao) {
>             this.userDao = userDao;
>         }
>         1234
>         ```
>
>       - 联合**@Qualifier**注解注入：适用于一个接口**多个**实现类的**注解区别**
>
>         ```java
>         @Autowired
>         @Qualifier("userDaoImpl") // 指定bean的名字
>         private UserDao userDao;
>         123
>         ```
>
>    2. 使用`@Resource`注入：
>
>       - **Name**注入：在使用注解时，**配置name属性**
>
>         ```java
>         @Resource(name = "myUserDao")
>         1
>         ```
>
>       - **未知Name**注入：不配置name属性，注入属性的**成员变量但需要与Bean** 的名称**同名**
>
>         ```java
>         @Repository("myUserDao")
>         public class UserDaoImpl implements UserDao {
>             ……
>         @Resource
>         private UserDao myUserDao;
>         12345
>         ```
>
>       - **类型**注入：不配置name属性，名称都不同时，注入属性的**成员类型**会**根据Bean**实现的**接口类型**进行**匹配**
>
>         ```java
>         @Repository("myUserDao")
>         public class UserDaoImpl implements UserDao {
>             ……
>         @Resource
>         private UserDao userDao1;
>         12345
>         ```
>
> 4. 全注解开发：不再使用spring配置文件了，写一个**配置类**来代替配置文件
>
>    ```java
>    @Configuration
>    //@ComponentScan({"com.atguigu.spring6.controller", "com.atguigu.spring6.service","com.atguigu.spring6.dao"})
>    @ComponentScan("com.atguigu.spring6") //开启包扫描
>    public class Spring6Config {
>    }
>    12345
>    ```
>
>    说明：用全注解开发方式时，需要指定**包扫描所属的范围**，便于Spring框架确定扫描而注入Bean的范围

#### 5.3.1概述

##### 5.3.1.1简介

 从 Java 5 开始，Java 增加了对注解（Annotation）的支持，它是代码中的一种特殊标记，可以在编译、类加载和运行时被读取，执行相应的处理。开发人员可以通过注解在不改变原有代码和逻辑的情况下，在源代码中嵌入补充信息。

 Spring 从 2.5 版本开始提供了对注解技术的全面支持，我们可以使用注解来实现自动装配，简化 Spring 的 XML 配置。

##### 5.3.1.2步骤

1. 引入依赖
2. 开启组件扫描
3. 使用注解定义 Bean
4. 依赖注入

##### 5.3.1.3使用注解

 Spring 提供了以下多个注解，这些注解可以直接标注在 Java 类上，将它们定义成 Spring Bean

| 注解        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| @Component  | 该注解用于描述 Spring 中的 Bean，它是一个泛化的概念，仅仅表示容器中的一个**组件**（Bean），并且可以作用在应用的任何层次，例如 Service 层、Dao 层等。 使用时只需将该注解标注在相应类上即可。 |
| @Repository | 该注解用于将**数据访问层**（Dao 层）的类标识为 Spring 中的 Bean，其功能与 @Component 相同。 |
| @Service    | 该注解通常作用在**业务层**（Service 层），用于将业务层的类标识为 Spring 中的 Bean，其功能与 @Component 相同。 |
| @Controller | 该注解通常作用在**控制层**（如SpringMVC 的 Controller），用于将控制层的类标识为 Spring 中的 Bean，其功能与 @Component 相同。 |

#### 5.3.2开启组件扫描

##### 5.3.2.1概述

 Spring 默认不使用注解装配 Bean，因此我们需要在 Spring 的 XML 配置中，通过 `<context:component-scan> `元素开**启 Spring Beans的自动扫描功能**。开启此功能后，Spring 会自动从扫描指定的包（base-package 属性设置）及其子包下的所有类，如果类上使用了 @Component 注解，就将该类装配到容器中。

##### 5.3.2.2基本用例-实现组件扫描

步骤一：添加约束

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
    http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd">
</beans>
123456789
```

说明：

>  在 XML 配置的一级标签 中添加 context 相关的约束

步骤二：开启扫描方式

```xml
<context:component-scan base-package="com.atguigu.spring6">
</context:component-scan>
12
```

说明：

>  在Beans.xml文件中，设置开启扫描方式即可

##### 5.3.2.3指定要排除的组件

```xml
<context:component-scan base-package="com.atguigu.spring6">
    <!-- context:exclude-filter标签：指定排除规则 -->
    <!-- 
 		type：设置排除或包含的依据
		type="annotation"，根据注解排除，expression中设置要排除的注解的全类名
		type="assignable"，根据类型排除，expression中设置要排除的类型的全类名
	-->
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
        <!--<context:exclude-filter type="assignable" expression="com.atguigu.spring6.controller.UserController"/>-->
</context:component-scan>
12345678910
```

说明：

> 1. ```
>    <context:exclude-filter></context:exclude-filter>
>    ```
>
>    标签，指定排除规则
>
>    - type属性：设置排除或包含的依据
>      - 属性值：annotation，根据注解排除
>      - 属性值：assignable，根据类型排除
>    - expression属性：设置要排除的注解或类型的全类名

##### 5.3.2.4仅扫描指定组件

```xml
<context:component-scan base-package="com.atguigu" use-default-filters="false">
    <!-- context:include-filter标签：指定在原有扫描规则的基础上追加的规则 -->
    <!-- use-default-filters属性：取值false表示关闭默认扫描规则 -->
    <!-- 此时必须设置use-default-filters="false"，因为默认规则即扫描指定包下所有类 -->
    <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    <!--<context:include-filter type="assignable" expression="com.atguigu.spring6.controller.UserController"/>-->
</context:component-scan>
1234567
```

说明：

> 1. `use-default-filters="false"`，表示关闭默认扫描规则
> 2. `<context:include-filter></context:include-filter>`，表示指定的过滤条件来确定哪些类应该被包含在组件扫描中

#### 5.3.2使用注解定义Bean

#### 5.3.3使用@Autowired注入

##### 5.3.3.1概述

![在这里插入图片描述](https://img-blog.csdnimg.cn/162941a00e8a414db7e732fa08f29fd9.png#pic_center)

说明：

> 1. @Autowired注解可以标注在：构造方法上、方法上、形参上、属性上、注解上
> 2. @Autowired注解的required属性，
>    - 属性值为True：表示注入的时候要求被注入的Bean必须是存在的，如果不存在则报错
>    - 属性值为False：：表示注入的时候要求被注入的Bean不一定是存在的，如果存在的话就注入，不存在的话，也不报错

细节：

> 1. 单独使用@Autowired注解时，**默认是根据类型装配**，默认是"byType"，例如基于XML管理Bean
>
> ```xml
> <bean id="userService" class="com.atguigu.spring6.autowire.service.impl.UserServiceImpl" autowire="byType"></bean>
> 1
> ```

##### 5.3.3.2属性注入

步骤一：搭建环境

1.创建UserDao接口

```java
package com.atguigu.spring6.dao;

public interface UserDao {

    public void print();
}
123456
```

2.创建UserDaoImpl实现

```java
package com.atguigu.spring6.dao.impl;

import com.atguigu.spring6.dao.UserDao;
import org.springframework.stereotype.Repository;

@Repository
public class UserDaoImpl implements UserDao {

    @Override
    public void print() {
        System.out.println("Dao层执行结束");
    }
}
12345678910111213
```

3.创建UserService接口

```java
package com.atguigu.spring6.service;

public interface UserService {

    public void out();
}
123456
```

4.创建UserServiceImpl实现类

```java
package com.atguigu.spring6.service.impl;

import com.atguigu.spring6.dao.UserDao;
import com.atguigu.spring6.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserServiceImpl implements UserService {

    @Autowired
    private UserDao userDao;

    @Override
    public void out() {
        userDao.print();
        System.out.println("Service层执行结束");
    }
}
12345678910111213141516171819
```

5.创建UserController类

```java
package com.atguigu.spring6.controller;

import com.atguigu.spring6.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;

@Controller
public class UserController {

    @Autowired
    private UserService userService;

    public void out() {
        userService.out();
        System.out.println("Controller层执行结束。");
    }
}
1234567891011121314151617
```

步骤二：演示

```java
@Test
public void testAnnotation(){
    ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");
    UserController userController = context.getBean("userController", UserController.class);
    userController.out();
}
123456
```

说明：

> 1. 当使用@Autowired注解注入时，可不提供构造方法喝Setter方法，也可以注入成功
> 2. 结果：![image-20230512102218784](https://img-blog.csdnimg.cn/img_convert/c053582c57ba782720414876cf78dfef.png)

##### 5.3.3.3set注入

步骤一：搭建环境

1.修改UserServiceImpl类

```java
@Service
public class UserServiceImpl implements UserService {

    private UserDao userDao;

    @Autowired
    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public void out() {
        userDao.print();
        System.out.println("Service层执行结束");
    }
}
12345678910111213141516
```

2.修改UserController类

```java
@Controller
public class UserController {

    private UserService userService;

    @Autowired
    public void setUserService(UserService userService) {
        this.userService = userService;
    }

    public void out() {
        userService.out();
        System.out.println("Controller层执行结束。");
    }

}
12345678910111213141516
```

步骤二：演示

```java
@Test
public void testAnnotation(){
    ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");
    UserController userController = context.getBean("userController", UserController.class);
    userController.out();
}
123456
```

说明：

>  通过在需要注入的setter方法上进行添加@Autowired注解

##### 5.3.3.4构造方法注入

步骤一：搭建环境

1.修改UserServiceImpl类

```java
@Service
public class UserServiceImpl implements UserService {

    private UserDao userDao;

    @Autowired
    public UserServiceImpl(UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public void out() {
        userDao.print();
        System.out.println("Service层执行结束");
    }
}
12345678910111213141516
```

2.修改UserController类

```java
@Controller
public class UserController {

    private UserService userService;

    @Autowired
    public UserController(UserService userService) {
        this.userService = userService;
    }

    public void out() {
        userService.out();
        System.out.println("Controller层执行结束。");
    }

}
12345678910111213141516
```

步骤二：演示

```java
@Test
public void testAnnotation(){
    ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");
    UserController userController = context.getBean("userController", UserController.class);
    userController.out();
}
123456
```

说明：

>  通过在需要注入的构造器方法上进行添加@Autowired注解

##### 5.3.3.5形参注入

步骤一：搭建环境

1.修改UserServiceImpl类

```java
@Service
public class UserServiceImpl implements UserService {

    private UserDao userDao;

    public UserServiceImpl(@Autowired UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public void out() {
        userDao.print();
        System.out.println("Service层执行结束");
    }
}
123456789101112131415
```

2.修改UserController类

```java
@Controller
public class UserController {

    private UserService userService;

    public UserController(@Autowired UserService userService) {
        this.userService = userService;
    }

    public void out() {
        userService.out();
        System.out.println("Controller层执行结束。");
    }
}
1234567891011121314
```

步骤二：演示

```java
@Test
public void testAnnotation(){
    ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");
    UserController userController = context.getBean("userController", UserController.class);
    userController.out();
}
123456
```

说明：

>  通过在需要注入的形参上进行添加@Autowired注解

##### 5.3.3.6无注解注入

步骤一：搭建环境

1.修改UserServiceImpl类

```java
@Service
public class UserServiceImpl implements UserService {

 
    private UserDao userDao;

    public UserServiceImpl(UserDao userDao) {
        this.userDao = userDao;
    }

    @Override
    public void out() {
        userDao.print();
        System.out.println("Service层执行结束");
    }
}
12345678910111213141516
```

步骤二：演示

```java
@Test
public void testAnnotation(){
    ApplicationContext context = new ClassPathXmlApplicationContext("Beans.xml");
    UserController userController = context.getBean("userController", UserController.class);
    userController.out();
}
123456
```

说明：

>  当有参数的构造方法只有一个时，@Autowired注解可以省略

##### 5.3.3.7联合@Qualifier注解注入

步骤一：搭建环境

1.添加UserDaoRedisImpl类

```java
@Repository
public class UserDaoRedisImpl implements UserDao {

    @Override
    public void print() {
        System.out.println("Redis Dao层执行结束");
    }
}
12345678
```

说明：

> - 此时，添加实现UserDao接口类，已经造成一个接口对应两个实现类
> - 此时，程序错误，信息中说：不能装配，UserDao这个Bean的数量等于2

步骤二：修改UserServiceImpl类

```java
@Service
public class UserServiceImpl implements UserService {

    @Autowired
    @Qualifier("userDaoImpl") // 指定bean的名字
    private UserDao userDao;

    @Override
    public void out() {
        userDao.print();
        System.out.println("Service层执行结束");
    }
}
12345678910111213
```

说明：

>  当需要注入的接口有多个实现类时，可以联合使用@Qualifier(“userDaoImpl”) 注解，并指定实现类的名字，即可完成属性注入

#### 5.3.4使用@Resource注入

##### 5.3.4.1概述

 @Resource注解是通过名称匹配的方式来实现注入的，默认按照名称进行匹配，如果找不到匹配的名称，则会尝试按照类型匹配。

 @Resource注解是JDK扩展包中的，也就是说属于JDK的一部分。所以该注解是标准注解，更加具有通用性。(JSR-250标准中制定的注解类型。JSR是Java规范提案。)

![image-20230512205825581](https://img-blog.csdnimg.cn/img_convert/33d53390284aca93527aa9ff81bafb65.png)

说明：

> - 如果是JDK8的话不需要额外引入依赖。高于JDK11或低于JDK8需要引入以下依赖
>
> ```xml
> <dependency>
>     <groupId>jakarta.annotation</groupId>
>     <artifactId>jakarta.annotation-api</artifactId>
>     <version>2.1.1</version>
> </dependency>
> 12345
> ```

##### 5.3.4.2Name注入

步骤一：搭建环境

1.修改UserDaoImpl类

```java
package com.atguigu.spring6.dao.impl;

import com.atguigu.spring6.dao.UserDao;
import org.springframework.stereotype.Repository;

@Repository("myUserDao")
public class UserDaoImpl implements UserDao {

    @Override
    public void print() {
        System.out.println("Dao层执行结束");
    }
}
12345678910111213
```

说明：

>  当使用注解时，在小括号内写上属性名称表示为此Bean定义别名

2.修改UserServiceImpl类

```java
package com.atguigu.spring6.service.impl;

import com.atguigu.spring6.dao.UserDao;
import com.atguigu.spring6.service.UserService;
import jakarta.annotation.Resource;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Service;

@Service
public class UserServiceImpl implements UserService {

    @Resource(name = "myUserDao")
    private UserDao myUserDao;

    @Override
    public void out() {
        myUserDao.print();
        System.out.println("Service层执行结束");
    }
}
123456789101112131415161718192021
```

说明：

>  当使用@Resource注解时，可以使用name属性指定属性注入的别名

步骤二：演示

##### 5.3.4.3未知Name注入

步骤一：搭建环境

1.修改UserDaoImpl类

```java
package com.atguigu.spring6.dao.impl;

import com.atguigu.spring6.dao.UserDao;
import org.springframework.stereotype.Repository;

@Repository("myUserDao")
public class UserDaoImpl implements UserDao {

    @Override
    public void print() {
        System.out.println("Dao层执行结束");
    }
}
12345678910111213
```

2.修改UserServiceImpl类

```java
package com.atguigu.spring6.service.impl;

import com.atguigu.spring6.dao.UserDao;
import com.atguigu.spring6.service.UserService;
import jakarta.annotation.Resource;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Service;

@Service
public class UserServiceImpl implements UserService {

    @Resource
    private UserDao myUserDao;

    @Override
    public void out() {
        myUserDao.print();
        System.out.println("Service层执行结束");
    }
}
123456789101112131415161718192021
```

说明：

>  当使用@Resource注解时，在name属性未知的情况下，将属性注入的成员属性变量名定义为与Bean同名，即可完成注入

步骤二：演示

##### 5.3.4.4类型注入

步骤一：搭建环境

1.原UserDaoImpl类

```java
@Repository("myUserDao")
public class UserDaoImpl implements UserDao {

    @Override
    public void print() {
        System.out.println("Dao层执行结束");
    }
}
12345678
```

2.修改UserServiceImpl类

```java
@Service
public class UserServiceImpl implements UserService {

    @Resource
    private UserDao userDao1;

    @Override
    public void out() {
        userDao1.print();
        System.out.println("Service层执行结束");
    }
}
123456789101112
```

说明：

>  当使用@Resource注解时，现在userDao1属性名不存在，但仍然可以注入成功。因为，UserDao他们的类型名相同

#### 5.3.5全注解开发

##### 5.3.5.1概述

 全注解开发就是不再使用spring配置文件了，写一个配置类来代替配置文件

##### 5.3.5.2基本用例-全注解开发实现

步骤一：创建配置类

```java
@Configuration
//@ComponentScan({"com.atguigu.spring6.controller", "com.atguigu.spring6.service","com.atguigu.spring6.dao"})
@ComponentScan("com.atguigu.spring6")
public class Spring6Config {
}
12345
```

说明：

>  使用@ComponentScan注解，进行组件扫描，从而替代了原有在xml文件中的配置

步骤二：演示

```java
@Test
public void testAllAnnotation(){
    ApplicationContext context = new AnnotationConfigApplicationContext(Spring6Config.class);
    UserController userController = context.getBean("userController", UserController.class);
    userController.out();
    logger.info("执行成功");
}
1234567
```

说明：

>  需要使用AnnotationConfigApplicationContext类来获取Spring6Config的字节码文件

### 5.4原理

笔记小结：

> 1. **扫描指定的包**，获取所有需要管理的类的类名。
> 2. 实例化需要管理的类，通过**反射机制**调用构造器来实现。
> 3. 通过反射机制调用**setter方法或者构造器注入**属性值。
> 4. **维护对象之间的依赖关系，实现对象之间的解耦**。
> 5. 将实例化好的对象注册到IOC容器中，便于后续使用。

说明：

> ![在这里插入图片描述](https://img-blog.csdnimg.cn/907f012dacf94f719e54f248b598ac1e.png#pic_center)

步骤一：环境搭建

1.创建注解

- 创建Bean注解

  ```java
  // 此注解用于定义容器对象，类似于@Componet、@Service、@Controller注解等作用
  @Target(ElementType.TYPE)
  @Retention(RetentionPolicy.RUNTIME)
  public @interface Bean {
  }
  12345
  ```

- 创建依赖注入注解

  ```java
  // 此注解用于完成成员属性的依赖注入，类似于@Autoware、@Resource注解等作用
  @Target({ElementType.FIELD})
  @Retention(RetentionPolicy.RUNTIME)
  public @interface Di {
  }
  12345
  ```

2.创建IOC核心逻辑

- 定义bean容器接口

  ```java
  package com.atguigu.spring.core;
  
  public interface ApplicationContext {
  
      Object getBean(Class clazz);
  }
  123456
  ```

- 编写注解bean容器接口实现

  ```java
  public class AnnotationApplicationContext implements ApplicationContext {
  
      // 存储Bean的容器
      private HashMap<Class, Object> beanFactory = new HashMap<>();
  
      // 根据字节码文件获取Bean容器中的对象
      @Override
      public Object getBean(Class clazz) {
          return beanFactory.get(clazz);
      }
  
      /**
       * 根据包扫描加载bean
       * @param basePackage
       */
      public AnnotationApplicationContext(String basePackage) {
          try {
              String packageDirName = basePackage.replaceAll("\\.", "\\\\");
              Enumeration<URL> dirs =Thread.currentThread().getContextClassLoader().getResources(packageDirName);
              while (dirs.hasMoreElements()) {
                  URL url = dirs.nextElement();
                  String filePath = URLDecoder.decode(url.getFile(),"utf-8");
                  rootPath = filePath.substring(0, filePath.length()-packageDirName.length());
                  // 扫描包下的Bean
                  loadBean(new File(filePath));
              }
  
          } catch (Exception e) {
              throw new RuntimeException(e);
          }
          //依赖注入
          loadDi();
      }
  
  
      private  void loadBean(File fileParent) {
          if (fileParent.isDirectory()) {
              File[] childrenFiles = fileParent.listFiles();
              if(childrenFiles == null || childrenFiles.length == 0){
                  return;
              }
              for (File child : childrenFiles) {
                  if (child.isDirectory()) {
                      //如果是个文件夹就继续调用该方法,使用了递归
                      loadBean(child);
                  } else {
                      //通过文件路径转变成全类名,第一步把绝对路径部分去掉
                      String pathWithClass = child.getAbsolutePath().substring(rootPath.length() - 1);
                      //选中class文件
                      if (pathWithClass.contains(".class")) {
                          //    com.xinzhi.dao.UserDao
                          //去掉.class后缀，并且把 \ 替换成 .
                          String fullName = pathWithClass.replaceAll("\\\\", ".").replace(".class", "");
                          try {
                              Class<?> aClass = Class.forName(fullName);
                              //把非接口的类实例化放在map中
                              if(!aClass.isInterface()){
                                  Bean annotation = aClass.getAnnotation(Bean.class);
                                  if(annotation != null){
                                      Object instance = aClass.newInstance();
                                      //判断一下有没有接口
                                      if(aClass.getInterfaces().length > 0) {
                                          //如果有接口把接口的class当成key，实例对象当成value
                                          System.out.println("正在加载【"+ aClass.getInterfaces()[0] +"】,实例对象是：" + instance.getClass().getName());
                                          beanFactory.put(aClass.getInterfaces()[0], instance);
                                      }else{
                                          //如果有接口把自己的class当成key，实例对象当成value
                                          System.out.println("正在加载【"+ aClass.getName() +"】,实例对象是：" + instance.getClass().getName());
                                          beanFactory.put(aClass, instance);
                                      }
                                  }
                              }
                          } catch (ClassNotFoundException | IllegalAccessException | InstantiationException e) {
                              e.printStackTrace();
                          }
                      }
                  }
              }
          }
      }
  
      private void loadDi() {
          for(Map.Entry<Class,Object> entry : beanFactory.entrySet()){
              //就是咱们放在容器的对象
              Object obj = entry.getValue();
              Class<?> aClass = obj.getClass();
              Field[] declaredFields = aClass.getDeclaredFields();
              for (Field field : declaredFields){
                  Di annotation = field.getAnnotation(Di.class);
                  if( annotation != null ){
                      field.setAccessible(true);
                      try {
                          System.out.println("正在给【"+obj.getClass().getName()+"】属性【" + field.getName() + "】注入值【"+ beanFactory.get(field.getType()).getClass().getName() +"】");
                          field.set(obj,beanFactory.get(field.getType()));
                      } catch (IllegalAccessException e) {
                          e.printStackTrace();
                      }
                  }
              }
          }
      }
  }
  123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293949596979899100101102
  ```

  说明：

  > 可将此代码复制到IDEA中查看逻辑更详细

3.创建Dao层

- 创建UserDao接口

```java
public interface UserDao {

    public void print();
}
1234
```

- 创建UserDaoImpl实现

```java
@Bean
public class UserDaoImpl implements UserDao {
    @Override
    public void print() {
        System.out.println("Dao层执行结束");
    }
}

12345678
```

说明：

> - 当此类实现了UserDao这个接口时，会将UserDao这个接口作为容器的Key值，来获取UserDaoImpl这个实现类
>
> - 这也就是为什么一个接口不能对应多个实现类，因为HashMap的Key值不能重复
>
> - ```java
>   // 参数解释，参数1：实现类上实现的第一个接口或者实现类的字节码文件；参数2：实现类实例
>   beanFactory.put(aClass.getInterfaces()[0], instance);
>   // 此处，参数1：接口为UserDao；参数2，实现类实例为UserDaoImpl
>   123
>   ```

4.创建Service层

- 创建UserService接口

  ```java
  public interface UserService {
      public void out();
  }
  123
  ```

- 创建UserServiceImpl实现类

  ```java
  @Bean
  public class UserServiceImpl implements UserService {
  
      @DI
      private UserDao userDao;
  
      @Override
      public void out() {
          userDao.print();
          System.out.println("Service层执行结束");
      }
  }
  123456789101112
  ```

  说明：

  > - 当此类里包含了依赖注入这个接口时，会将UserServiceImpl这个实现类实例作为依赖注入的Key值，并且根据依赖注入的变量名确定所需要依赖注入的实现类实例
  >
  > - ```java
  >   // 参数解释，参数1：设置字段值的对象实例；参数2：需要设置的字段值
  >   field.set(obj, beanFactory.get(field.getType()));
  >   //此处，参数1：实现类实例UserServiceImpl；参数2：实现类实例UserDaoImpl
  >   123
  >   ```

步骤二：演示

```java
ApplicationContext applicationContext = new AnnotationApplicationContext("org.example");
UserService bean = (UserService) applicationContext.getBean(UserService.class);
bean.out();
123
```

## 6.面向切面：AOP (重点)

笔记小结：

> 1. 概述：
>
>    1. 含义：AOP（Aspect Oriented Programming）是一种**设计思想**，是软件设计领域中的面向切面编程
>    2. 作用：
>       - **简化开发**：分离关注点，让各个一些通用的行为（日志、事务、安全）实现重用
>       - **降低**代码**耦合度**：将不同的关注点分离开来，提高代码可复用性和可维护性
>    3. 横切关注点：横切关注点是指跨越应用程序**多个模块的功能或行为**。例如日志记录、安全性等与业务逻辑无关的功能
>    4. 通知：通知（增强）是指在 AOP 中定义的一种特殊类型的方法，它包含要在连接点（join point）执行的一些**行为**。例如在某个方法执行前、中、后需要加上一些输出日志等这样的**逻辑**
>    5. 切面：切面指的是横切关注点和通知的组合，简单的说，**切面就是封装通知方法的类**
>    6. 目标：目标（Target）是指被通知的对象或者被切面所影响的**对象**。例如类、接口、方法这类元素
>    7. 代理：代理是指控制对目标对象的访问，并在访问过程中插入**额外的逻辑**。简单的说，代理就是向目标对象应用通知之后创建的**代理对象**
>    8. 连接点：连接点（Join Point）表示在程序执行过程中能够**插入一个切面的点**。简单的说，连接点就是代理对象中的执行逻辑
>    9. 切入点：切入点（Pointcut）表示在目标对象中定义的一个或多个特定的方法或方法**执行位置**，它表示在何处应该插入切面的逻辑
>
> 2. 代理模式：代理模式是一种结构型设计模式，它使得代理对象可以代表另一个对象进行访问
>
>    1. 静态代理：静态代理是用**代码**的方式实现方法之前或之后执行一些附加操作
>
>    2. 动态代理：它允许在运行时
>
>       动态地创建代理对象
>
>       ，并将
>
>       切面逻辑织入
>
>       到目标对象的方法中
>
>       - 分类：基于接口的代理（有接口情况）、基于类的代理（无接口情况）
>
> 3. 切入点表达式：用于**匹配目标对象中的方法**，并提供切入点的精确定义
>
>    ![image-20230814214853767](https://img-blog.csdnimg.cn/img_convert/50e3aa25c99beb28ca1636100c942a8b.png)
>
> 4. 基于注解的AOP：各个小结模块，请**查看此小结**（重点）
>
> 5. 基于XML的AOP：通过**XML** 的方式来实现切面的定义和应用（了解）

### 6.1概述

#### 6.1.1定义

 AOP（Aspect Oriented Programming）是一种**设计思想**，是软件设计领域中的面向切面编程，它是面向对象编程的一种补充和完善，它以通过**预编译**方式和**运行期动态代理**方式实现，在不修改源代码的情况下，给程序动态统一添加额外功能的一种技术。利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的耦合度降低，提高程序的可重用性，同时提高了开发的效率

#### 6.1.2作用

1. 代码重用和模块化：AOP可以将一些通用的行为（例如日志记录、安全控制、事务管理等）抽象出来，形成可重用的模块，避免在每个业务逻辑中都重复编写这些代码。
2. 分离关注点：AOP将不同的关注点分离开来，使得各个模块间职责更加清晰明确，代码的可读性和可维护性也更强。
3. 简化开发：AOP可以帮助开发人员将关注点从业务逻辑中分离出来，使得开发更加简单明了。
4. 提高系统的可扩展性：在系统需求变化时，只需要修改AOP模块而不是修改业务逻辑，这可以使得系统更加易于扩展和维护。
5. 降低代码耦合度：AOP的作用是将不同的关注点分离开来，这可以避免代码之间的紧耦合，提高代码的可复用性和可维护性。

#### 6.1.3横切关注点

 在 AOP 中，横切关注点指的是在应用程序中影响多个类或对象的横切性质的行为，比如日志记录、性能监控、事务处理等等。这些行为可能分散在整个应用程序中的**不同类和方法**中，而不是与应用程序的核心业务逻辑紧密相关。

 使用 AOP 技术，可以将这些横切关注点从应用程序的核心业务逻辑中分离出来，并将它们模块化为可重用的模块，从而实现更好的代码结构和更好的可维护性。

![在这里插入图片描述](https://img-blog.csdnimg.cn/718d453ae2b04683b3afd785087276f1.png#pic_center)

#### 6.1.4通知（增强）

 通知（advice）也被称为增强（advice），是指在 AOP 中定义的一种**特殊类型的方法**，它包含要在连接点（join point）执行的一些**行为**。通知可以在**目标方法执行之前**、**之后**或**异常时**被执行，也可以在目标方法返回一个结果后被执行。通知的目的是在不修改目标对象的情况下，将增强（如日志、事务管理等）应用于应用程序的特定方法或切入点。通知是实现 AOP 的核心组件之一，通过将通知应用于特定的连接点（join point）来实现面向切面编程

简单来说：通知就是你想要增强的功能，比如 安全，事务，日志等

通知分类：

1. 前置通知：在被代理的目标方法**前**执行
2. 返回通知：在被代理的目标方法**成功结束**后执行（**寿终正寝**）
3. 异常通知：在被代理的目标方法**异常结束**后执行（**死于非命**）
4. 后置通知：在被代理的目标方法**最终结束**后执行（**盖棺定论**）
5. 环绕通知：使用try…catch…finally结构围绕**整个**被代理的目标方法，包括上面四种通知对应的所有位置

![image-20230513233617466](https://img-blog.csdnimg.cn/img_convert/afbfda6de46c07477ce7df111e8d4bbd.png)

#### 6.1.5切面

 在AOP中，切面指的是横切关注点和通知的组合，它是一个模块化的横向分割，可以理解为一个横向的切片。切面是对横切关注点和通知的封装，它包含了一组切点和通知，用于描述在何处、何时、以及如何执行横切逻辑。切面可以在不修改原代码的情况下，对原有的代码进行功能的增强或改变。通常，切面是以一个类的形式存在的，它包含了一个或多个通知和一个或多个切点。

简单来说：**切面就是封装通知方法的类**

![在这里插入图片描述](https://img-blog.csdnimg.cn/c5fe0cb950a64e599f05e8fbbbe5faf3.png#pic_center)

#### 6.1.6目标

 在AOP（Aspect-Oriented Programming）中，目标（Target）是指被通知的对象或者被切面所影响的对象。它是应用程序中的一个**具体元素**，可以是类、接口、方法或者字段等。简单点说，目标就是被代理的**目标对象**

#### 6.1.7代理

 在AOP（Aspect-Oriented Programming）中，代理（Proxy）是一种设计模式，用于控制对目标对象的访问，并在访问过程中插入**额外的逻辑**。简单点说，代理就是向目标对象应用通知之后创建的代理对象

#### 6.1.8连接点

 在 AOP 中，连接点（Join Point）表示在程序执行过程中能够**插入一个切面的点**，例如方法调用、异常处理、字段访问等。连接点定义了在程序中的哪个位置可以应用切面。切面可以在连接点前后增加额外的处理逻辑，从而影响程序的行为。通俗地讲，连接点就是在程序执行中可以被拦截的地方

![image-20230513234310439](https://img-blog.csdnimg.cn/img_convert/1819282411f0e60900d52c3e6da1ecf2.png)

说明：

>  把方法排成一排，每一个横切位置看成x轴方向，把方法从上到下执行的顺序看成y轴，x轴和y轴的交叉点就是连接点。**通俗说，就是spring允许你使用通知的地方**

#### 6.1.9切入点

 在 AOP 中，切入点（Join Point）是指程序执行过程中明确的点，通常是方法调用的时候，也可以是异常处理程序的处理过程。切入点定义了哪些方法是需要被拦截或增强的，是 AOP 中最重要的概念之一。切入点通常以方法的形式被定义，比如某个类的所有方法、某个包下的所有方法等等。在 AOP 中，通常会使用表达式语言定义切入点，如使用 Spring AOP 中的 @Pointcut 注解定义。

### 6.2代理模式

#### 6.2.1概述

 代理模式是一种结构型设计模式，它使得代理对象可以代表另一个对象进行访问。它是二十三种设计模式中的一种，属于结构型模式。它的作用就是通过提供一个代理类，让我们在调用目标方法的时候，不再是直接对目标方法进行调用，而是通过代理类**间接**调用。让不属于目标方法核心逻辑的代码从目标方法中剥离出来——**解耦**。调用目标方法时先调用代理对象的方法，减少对目标方法的调用和打扰，同时让附加功能能够集中在一起也有利于统一维护。

![image-20230814214956482](https://img-blog.csdnimg.cn/img_convert/04cd69780d5df0b39df294d9de654fd1.png)



代理：将非核心逻辑剥离出来以后，**封装这些非核心逻辑的类**、对象、方法

#### 6.2.2静态代理

 在静态代理中，代理类是**在编译时期创建**的，代理类和委托类实现相同的接口或继承相同的类，并在代理类中实现委托类中的方法，在调用委托类的方法之前或之后执行一些附加操作

```java
public class CalculatorStaticProxy implements Calculator {
    
    // 将被代理的目标对象声明为成员变量
    private Calculator target;
    
    public CalculatorStaticProxy(Calculator target) {
        this.target = target;
    }
    
    @Override
    public int add(int i, int j) {
    
        // 附加功能由代理类中的代理方法来实现
        System.out.println("[日志] add 方法开始了，参数是：" + i + "," + j);
    
        // 通过目标对象来实现核心业务逻辑
        int addResult = target.add(i, j);
    
        System.out.println("[日志] add 方法结束了，结果是：" + addResult);
    
        return addResult;
    }
}
1234567891011121314151617181920212223
```

说明：

>  静态代理确实实现了解耦，但是由于代码都写死了，完全不具备任何的灵活性

#### 6.2.3动态代理

##### 6.2.3.1概述

###### 6.2.3.1.1定义

 在动态代理中，代理类是在**运行时期动态创建**的。它不需要事先知道委托类的接口或实现类，而是在运行时期**通过 Java 反射机制动态生成代理类**

![在这里插入图片描述](https://img-blog.csdnimg.cn/5f5062002302430484a2f578b580ff76.png#pic_center)

###### 6.2.3.1.2分类

动态代理分类

- 基于接口的代理（有接口情况）
- 基于类的代理（无接口情况）

![image-20230814215007178](https://img-blog.csdnimg.cn/img_convert/1fb6729e70d3e7d8921dbc13ee4202e4.png)

说明：

>  AspectJ：是AOP思想的一种实现。本质上是静态代理，**将代理逻辑“织入”被代理的目标类编译得到的字节码文件**，所以最终效果是动态的。weaver就是织入器。Spring只是借用了AspectJ中的注解。

![image-20230814215024474](https://img-blog.csdnimg.cn/img_convert/089eb4b761edf24a4f8a4ed82e474ce7.png)

说明：

> - 当动态代理是基于接口的代理情况时，此种方式是JDK原生的实现方式。需要被代理的目标类必须**实现接口**。因为这个技术要求**代理对象和目标对象实现同样的接口**
> - 当动态代理是基于类的代理情况时，通过**继承被代理的目标类**实现代理。因此不需要目标类实现接口

补充：

> - JDK动态代理动态生成的代理类会在com.sun.proxy包下，类名为$proxy1，和目标类实现相同的接口
> - cglib动态代理动态生成的代理类会和目标在在相同的包下，会继承目标类

##### 6.2.3.2基本用例-实现动态代理

步骤一：创建ProxyFactory类

```java
public class ProxyFactory {

    private Object target;

    public ProxyFactory(Object target) {
        this.target = target;
    }

    public Object getProxy(){
        /**
         * newProxyInstance()：创建一个代理实例
         * 其中有三个参数：
         * 1、classLoader：加载动态生成的代理类的类加载器
         * 2、interfaces：目标对象实现的所有接口的class对象所组成的数组
         * 3、invocationHandler：设置代理对象实现目标对象方法的过程，即代理类中如何重写接口中的抽象方法
         */
        ClassLoader classLoader = target.getClass().getClassLoader();
        Class<?>[] interfaces = target.getClass().getInterfaces();
        InvocationHandler invocationHandler = new InvocationHandler() {
            @Override
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
                /**
                 * proxy：代理对象
                 * method：代理对象需要实现的方法，即其中需要重写的方法
                 * args：method所对应方法的参数
                 */
                Object result = null;
                try {
                    System.out.println("[动态代理][日志] "+method.getName()+"，参数："+ Arrays.toString(args));
                    result = method.invoke(target, args);
                    System.out.println("[动态代理][日志] "+method.getName()+"，结果："+ result);
                } catch (Exception e) {
                    e.printStackTrace();
                    System.out.println("[动态代理][日志] "+method.getName()+"，异常："+e.getMessage());
                } finally {
                    System.out.println("[动态代理][日志] "+method.getName()+"，方法执行完毕");
                }
                return result;
            }
        };

        return Proxy.newProxyInstance(classLoader, interfaces, invocationHandler);
    }
}
1234567891011121314151617181920212223242526272829303132333435363738394041424344
```

说明：

> - 动态代理需要使用Proxy.newProxyInstance()方法
> - 需要设置代理对象实现目标对象的方法过程

步骤二：演示

```java
@Test
public void testDynamicProxy(){
    ProxyFactory factory = new ProxyFactory(new CalculatorLogImpl());
    Calculator proxy = (Calculator) factory.getProxy();
    proxy.div(1,0);
    //proxy.div(1,1);
}
1234567
```

### 6.3切入点表达式

 在 AOP 中，切入点表达式指定了哪些方法需要被织入**增强逻辑**。它是一个表达式，用于**匹配目标对象中的方法**，并提供切入点的精确定义

![image-20230514145900081](https://img-blog.csdnimg.cn/img_convert/8578fde55d6dd885a62f6c213c677d93.png)

说明：

>  在切入点表达式语法中，用`*`号代替“权限修饰符”和“返回值”部分表示“权限修饰符”和“返回值”不限

### 6.4基于注解的AOP

笔记小结：

> 1. 概述：在Java类、方法、参数等上添加**注解**的方式来实现切面的定义和应用
>
> 2. 基本用例：
>
>    步骤一：导入依赖
>
>    步骤二：创建切面类（需要选择通知方式）
>
>    步骤三：添加xml配置文件
>
> 3. 通知方式：
>
>    1. **前置**通知：`@Before`
>    2. **异常**通知：`@AfterThrowing`
>    3. **返回**通知：`@AfterReturning`
>    4. **后置**通知：`@After`
>    5. **环绕**通知：`@Around`
>
> 4. 获取通知信息
>
>    1. 获取连接点：在方法中使用**JoinPoint**即可获取连接点信息
>
>       ```java
>       public void beforeMethod(JoinPoint joinPoint)
>       1
>       ```
>
>    2. 获取目标对象的**返回值**：在目标对象的返回通知上添加**returning**属性
>
>       ```java
>       @AfterReturning(value = "execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))", returning = "result")
>       public void afterReturningMethod(JoinPoint joinPoint, Object result)
>       12
>       ```
>
>    3. 获取目标对象的**异常**：在目标对象的异常通知上添加**throwing**属性
>
>       ```java
>       @AfterThrowing(value = "execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))", throwing = "ex")
>       public void afterThrowingMethod(JoinPoint joinPoint, Throwable ex)
>       12
>       ```
>
> 5. 重用切入点表达式
>
>    1. 声明：在空参、空方法体、空返回值的方法上使用**@Pointcut**注解
>
>       ```java
>       @Pointcut("execution(* com.atguigu.aop.annotation.*.*(..))")
>       public void pointCut(){}
>       12
>       ```
>
>    2. **同切面**使用：在同一切面中直接引用即可
>
>       ```java
>       @Before("pointCut()")
>       1
>       ```
>
>    3. **不同切面**使用：在不同切面中
>
>       ```java
>       @Before("com.atguigu.aop.CommonPointCut.pointCut()")
>       1
>       ```

#### 6.4.1概述

 基于注解的AOP是一种AOP的实现方式，它通过在Java类、方法、参数等上**添加注解**的方式来实现切面的定义和应用，相比于传统的XML配置方式更加便捷和灵活

#### 6.4.2基本用例-注解实现AOP

步骤一：导入依赖

```xml
 <!--spring aop依赖-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aop</artifactId>
        <version>6.0.2</version>
    </dependency>
    <!--spring aspects依赖-->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aspects</artifactId>
        <version>6.0.2</version>
    </dependency>
123456789101112
```

步骤二：创建接口以及实现类

1.接口

```java
public interface Calculator {
    int add(int i, int j); 
}
123
```

2.实现类

```java
@Component
public class CalculatorImpl implements Calculator {

    @Override
    public int add(int i, int j) {
        int result = i + j;
        System.out.println("方法内部 result = " + result);
        return result;
    }
}
12345678910
```

说明：

>  此实现类，也需要添加@Component注解，便于Spring容器进行管理

步骤三：创建切面类

```java
@Aspect
@Component
public class LogAspect {
    // 前置通知
    // 异常通知
    // 返回通知
    // 后置通知
    // 环绕通知
    ……
}
12345678910
```

注意：

>  此处需要配置切面类的通知方式！

说明：

> - @Aspect表示这个类是一个切面类
> - @Component注解保证这个切面类能够放入IOC容器

步骤四：配置Spring配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/aop
       http://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--
        基于注解的AOP的实现：
        1、将目标对象和切面交给IOC容器管理（注解+扫描）
        2、开启AspectJ的自动代理，为目标对象自动生成代理
        3、将切面类通过注解@Aspect标识
    -->
    <context:component-scan base-package="com.atguigu.aop.annotation"></context:component-scan>

    <aop:aspectj-autoproxy />
</beans>
123456789101112131415161718192021
```

补充：

>  当学习了SpringBoot后，通过SpringBoot来实现AOP，可省略此文件。因为SpringBoot以实现包扫描和切面标识

步骤五：演示

```java
@Test
public void testAdd(){
    ApplicationContext ac = new ClassPathXmlApplicationContext("beans.xml");
    Calculator calculator = ac.getBean( Calculator.class);
    int add = calculator.add(1, 1);
}
123456
```

说明：

> ![在这里插入图片描述](https://img-blog.csdnimg.cn/68c07d68f7294435bb74737e91dfe08a.png#pic_center)

#### 6.4.3通知方式

##### 6.4.3.1前置通知

使用@Before注解标识，在被代理的目标方法**前**执行

```java
@Before("execution(public int com.atguigu.aop.annotation.CalculatorImpl.*(..))")
public void beforeMethod(JoinPoint joinPoint){
    // getSignature（）获取连接点签名，getName（）获取连接点名称
    String methodName = joinPoint.getSignature().getName();
    String args = Arrays.toString(joinPoint.getArgs());
    System.out.println("Logger-->前置通知，方法名："+methodName+"，参数："+args);
}
1234567
```

说明：

> - @Before注解内为切入点表达式
> - JoinPoint 是指程序执行过程中明确的点，比如方法的调用或异常的处理。JoinPoint 提供了一个可供切面通知获取方法的关键信息的方式

##### 6.4.3.2异常通知

使用@AfterThrowing注解标识，在被代理的目标方法**异常结束**后执行

```java
@AfterThrowing(value = "execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))", throwing = "ex")
public void afterThrowingMethod(JoinPoint joinPoint, Throwable ex){
    String methodName = joinPoint.getSignature().getName();
    System.out.println("Logger-->异常通知，方法名："+methodName+"，异常："+ex);
}

123456
```

说明：

>  @AfterThrowing注解内为切入点表达式

##### 6.4.3.3返回通知

使用@AfterReturning注解标识，在被代理的目标方法**成功结束**后执行

```java
@AfterReturning(value = "execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))", returning = "result")
public void afterReturningMethod(JoinPoint joinPoint, Object result){
    String methodName = joinPoint.getSignature().getName();
    System.out.println("Logger-->返回通知，方法名："+methodName+"，结果："+result);
}

123456
```

说明：

>  @AfterReturning注解内为切入点表达式

##### 6.4.3.4后置通知

使用@After注解标识，在被代理的目标方法**最终结束**后执行

```java
  @After("execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))")
    public void afterMethod(JoinPoint joinPoint){
        String methodName = joinPoint.getSignature().getName();
        System.out.println("Logger-->后置通知，方法名："+methodName);
    }

123456
```

说明：

>  @After注解内为切入点表达式

##### 6.4.3.5环绕通知

使用@Around注解标识，使用try…catch…finally结构围绕**整个**被代理的目标方法，包括上面四种通知对应的所有位置

```java
@Around("execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))")
public Object aroundMethod(ProceedingJoinPoint joinPoint){
    String methodName = joinPoint.getSignature().getName();
    String args = Arrays.toString(joinPoint.getArgs());
    Object result = null;
    try {
        System.out.println("环绕通知-->目标对象方法执行之前");
        //目标对象（连接点）方法的执行
        result = joinPoint.proceed();
        System.out.println("环绕通知-->目标对象方法返回值之后");
    } catch (Throwable throwable) {
        throwable.printStackTrace();
        System.out.println("环绕通知-->目标对象方法出现异常时");
    } finally {
        System.out.println("环绕通知-->目标对象方法执行完毕");
    }
    return result;
}
123456789101112131415161718
```

说明：

> - @Around注解内为切入点表达式
> - ProceedingJoinPoint 继承自 JoinPoint 接口，是用于环绕通知的特殊类型的 JoinPoint，它可以用于在通知中控制目标方法的执行。在环绕通知中，ProceedingJoinPoint 提供了一个 proceed() 方法，该方法会执行目标方法，并返回其结果。

#### 6.4.4获取通知信息

##### 6.4.4.1获取连接点信息

在任何通知方式中，获取连接点信息可以在通知方法的参数位置设置JoinPoint类型的形参

```java
@Before("execution(public int com.atguigu.aop.annotation.CalculatorImpl.*(..))")
public void beforeMethod(JoinPoint joinPoint){
    //获取连接点的签名信息
    String methodName = joinPoint.getSignature().getName();
    //获取目标方法到的实参信息
    String args = Arrays.toString(joinPoint.getArgs());
    System.out.println("Logger-->前置通知，方法名："+methodName+"，参数："+args);
}
12345678
```

##### 6.4.4.2获取目标方法的返回值

@AfterReturning中的属性returning，用来将通知方法的某个形参，接收目标方法的返回值

```java
@AfterReturning(value = "execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))", returning = "result")
public void afterReturningMethod(JoinPoint joinPoint, Object result){
    String methodName = joinPoint.getSignature().getName();
    System.out.println("Logger-->返回通知，方法名："+methodName+"，结果："+result);
}
12345
```

##### 6.4.4.3获取目标方法的异常

@AfterThrowing中的属性throwing，用来将通知方法的某个形参，接收目标方法的异常

```java
@AfterThrowing(value = "execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))", throwing = "ex")
public void afterThrowingMethod(JoinPoint joinPoint, Throwable ex){
    String methodName = joinPoint.getSignature().getName();
    System.out.println("Logger-->异常通知，方法名："+methodName+"，异常："+ex);
}
12345
```

#### 6.4.5重用切入点表达式

说明：

>  切入点表达式可参考本节`面向切面：AOP`中的概述部分

简化切入点的书写

##### 6.4.5.1声明

```java
@Pointcut("execution(* com.atguigu.aop.annotation.*.*(..))")
public void pointCut(){}
12
```

##### 6.4.5.2同切面使用

```java
@Before("pointCut()")
public void beforeMethod(JoinPoint joinPoint){
    String methodName = joinPoint.getSignature().getName();
    String args = Arrays.toString(joinPoint.getArgs());
    System.out.println("Logger-->前置通知，方法名："+methodName+"，参数："+args);
}
123456
```

##### 6.4.5.3不同切面使用

```java
@Before("com.atguigu.aop.CommonPointCut.pointCut()")
public void beforeMethod(JoinPoint joinPoint){
    String methodName = joinPoint.getSignature().getName();
    String args = Arrays.toString(joinPoint.getArgs());
    System.out.println("Logger-->前置通知，方法名："+methodName+"，参数："+args);
}
123456
```

### 6.5基于XML的AOP（了解）

```xml
<context:component-scan base-package="com.atguigu.aop.xml"></context:component-scan>

<aop:config>
    <!--配置切面类-->
    <aop:aspect ref="loggerAspect">
        <aop:pointcut id="pointCut" 
                   expression="execution(* com.atguigu.aop.xml.CalculatorImpl.*(..))"/>
        <aop:before method="beforeMethod" pointcut-ref="pointCut"></aop:before>
        <aop:after method="afterMethod" pointcut-ref="pointCut"></aop:after>
        <aop:after-returning method="afterReturningMethod" returning="result" pointcut-ref="pointCut"></aop:after-returning>
        <aop:after-throwing method="afterThrowingMethod" throwing="ex" pointcut-ref="pointCut"></aop:after-throwing>
        <aop:around method="aroundMethod" pointcut-ref="pointCut"></aop:around>
    </aop:aspect>
</aop:config>
1234567891011121314
```

## 知识加油站

### 1.自动装配和依赖注入的区别与联系

 **依赖注入（Dependency Injection）** 是一种**设计模式**，旨在通过将依赖关系从一个对象传递给另一个对象，来实现对象之间的**解耦**。在Spring中，依赖注入通过容器来管理和传递对象之间的依赖关系，而不是由对象自身来创建或管理它们的依赖。这可以通过构造函数注入、Setter方法注入或字段注入等方式来实现

 **自动装配（Autowired）** 是Spring Framework提供的一种**依赖注入的方式**，用于自动将合适的依赖注入到相应的位置，无需手动指定每个依赖的注入方式。通过使用`@Autowired`注解，Spring会自动在容器中查找**匹配**的**依赖**，并将其**注入**到需要的位置

总结：

- 自动装配是Spring框架的特性，用于自动连接应用程序中的组件。
- 依赖注入是自动装配的一种具体实现方式，使用**@Autowired注解**来标识需要**自动注入**的属性、构造函数或方法参数。

### 2.依赖注入的两种方式

依赖注入（Dependency Injection）有两种常见的方式：

1. **构造函数注入**（Constructor Injection）：通过构造函数来注入依赖对象。在目标类的构造函数中声明参数，并在创建目标对象时通过构造函数传入依赖对象。这种方式可以保证依赖对象在目标对象创建时就被传入，从而确保了目标对象的完整性和一致性。
2. **Setter方法注入**（Setter Injection）：通过Setter方法来注入依赖对象。在目标类中定义对应的Setter方法，并在方法中接收依赖对象作为参数，通过调用Setter方法来注入依赖对象。这种方式可以在目标对象创建后动态地设置依赖对象，灵活性较高。