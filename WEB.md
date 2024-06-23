# WEB



一点小提示把。

对于java项目而言，很多人电脑会有很多不同版本的java。Ubuntu可以不必要通过`sudo vim /etc/environment`或者`sudo vim ~/.profile` 来修改环境变量的方式来选择jdk。其实linux下`sudo update-alternatives --config java`即可

如果你非要很掘的添加系统路径的方法的话，请使用`which java`让他返回路径，再一直使用`file [path]`，一直查找下去。直到最后显示出bin目录，其实可以提前结束了。





<hr>

### JDBC

> JDBC 需要对应的数据库驱动，我使用的是mysql，所以我需要mysql-connector-java.jar，
>
> 我这里使用的是maven添加的，没有试过导入jar包的方式使用。

非常原始的JDBC的java代码，后面我们会用**MyBatis简化**

```java
Class.forName("com.mysql....")/*如果你是用Maven添加依赖的话，这句话不要写*/
connection = DriverManager.getconnection("jdbc:mysql//localhost:3306/myDB","root","1234")
sql="SELECT ...";
pstmt = connection.prepareStatement(sql);
pstmt.setString(1,studentName);
rs = pstmt.executeQuery();
while(rs.next()){
    param1=rs.getString("");
    object=new xxx();
    object.setparam1(param1);
}
rs.close();
pstmt.close();
connection.close();
```









<hr>

### Druid(DBCP、C3P0)

> 用于原始的JDBC
>

1. `druid.properties`是必须要的文件

   ```xml
   driverClassName=com.mysql.jdbc.Driver
   url=jdbc:mysql///db1?useSSL=false&&useServerPrepStmts=true
   username=root
   password=123
   initialSize=5
   maxActive=10
   maxWait=3000
   ```

3. ```java
   Properties prop = new Properties();
   prop.load(new FileInputStream(""));
   DataSource dataSource = DruidDataSourceFactory.createDataSource(prop);
   Connection connection = dataSource.getConnection();
   //System.out.println(System.getProperty("user.dir"));
   ```







<hr>

### Maven

> 一定要自己安装配置一下maven

[这是阿里云maven仓库配置的文档：https://developer.aliyun.com/mvn/guide?spm=a2c6h.12873639.article-detail.7.10bb51edaWiok6](https://developer.aliyun.com/mvn/guide?spm=a2c6h.12873639.article-detail.7.10bb51edaWiok6)

1. `pom.xml` 和 `setting.xml`我们最常用的两个配置文件，前一个一般用于添加dependency，后面设置镜像下载源。使用方法自己用。
   idea推荐使用maven-helper插件。

2. **添加依赖**去[maven repository](https://mvnrepository.com/)搜索，然后如果要选择版本，选择**最多人用**的那个就好。

3. idea配置maven，千万注意要全局配置，每次创建项目都要重新配置maven是很麻烦的。

   ```tex
   File - Settings（如果你是从这里设置的，很不幸，你是局部设置）
   1.close project - customize -settings
   2.maven
   3.maven_home和maven_setting.xml和local repository
   4.（选择）安装idea的MavenHelper插件
   ```





<hr>

### MyBatis



> apache开发的一个简化我们写JDBC的语句的工具，并且让项目更好维护

 [入门_MyBatis中文网.pdf](../Documents/入门_MyBatis中文网.pdf) 
 [配置_MyBatis中文网.pdf](../Documents/配置_MyBatis中文网.pdf) 
 [动态 SQL_MyBatis中文网.pdf](../Documents/动态 SQL_MyBatis中文网.pdf) 



1. https://mybatis.net.cn/getting-started.html
   
   **入门**
   
   里面有无mapper代理代码，
   也有**mapper代理开发**的java代码（有代码补全，常用）
   
   **XML配置**
   可以看看吧
   
   
   
2. idea**配置数据库**，你写的sql语句不会报红了

   ```txt
   右边toolbar有database
   ```

   

3. 其实**maven编译**项目下，

   如果resources的文件会**按照resources的结构**目录放入java文件夹中。
   这样你可以优雅的xml配置文件放入resources，java文件就放在java文件夹下。


   另外改了路径，别忘了在mybatis配置文件改路径。
   这里建议使用包扫描的方法

   ```xml
   <package name="com.ljt.mapper"/>
   ```

   

4. idea安装**myBatisX**插件，提高代码跳转和补充效率

   

5. 解决获取到的对象有的属性是null的问题。

   因为数据库的属性和实体类的属性名字不一样。

   **使用resultmap**，不用resultType

   ```xml
   <!--
   	type可以使用别名
   	之后的<select>需要加上resultmap属性
   -->
   <resultmap id="a" type="">
       <result column="" property=""/>
   </resultmap>
   
   <select id="" resultMap="a">
       ...
   </select>
   ```

   

6. 注意一些**符号**
   #{}，sql里面替换成?，防止sql注入。
   ${}，我们不用。
   <，xml里面不能使用，用"**\&lt;**"替换，或者用CDATA区
   &，xml里面应该写"\&amp;"
   
   
   
7. SQL语句设置多个参数
   a）散装设计，**@Param注解**
   b）**封装成对象**（我喜欢这个）
   c）放入HashMap中

   

8. 动态SQL

   \-  可以巧用恒等式1=1，然后保证后面所有语句开头加了and

   

9. **MyBatis事务**
   sqlSession.commit();
   或者openSqlSession(true);

   

10. MyBatis底层封装简单解释

    ```tex
    单个参数：
    1.POJO类型：直接使用，property和参数参数占位符
    2.Map类型：直接使用
    3.Colletcion类型：封装成map，参数名collection
    4.Array类型：封装成map，参数名arary
    5.List类型：封装成map，参数名list
    6.其他类型：直接使用
    
    多个参数：
    封装成map对象，arg0或者param1都是第一个参数。
    ```

    

11. 简单语句注解开发，复杂语句写XML配置文件



<hr>



### HTML



[HTML标签讲解，你一定能学会HTML表格：https://developer.mozilla.org/zh-CN/docs/Learn](https://developer.mozilla.org/zh-CN/docs/Learn)



1. 注意一下合并单元格的操作
2. 要用div和span标签调整布局
3. 表单标签
   a）method="get"和"post"区别在于get有url长度有限制，用post要在请求体看参数
   b）使用label加上for属性，可以让鼠标操作地更加优雅

```html
<label for="password_id"></label>
<input type="password" id="password_id"/>
```









<hr>

### CSS



[你忘记了CSS属性有什么值，来看这里：https://www.w3school.com.cn/cssref/index.asp](https://www.w3school.com.cn/cssref/index.asp)





<hr>

### JavaScript



[javascript里面的对象，HTML DOM对象属性，一些常见的DOM_EVEN，你也许要知道：https://www.w3school.com.cn/jsref/index.asp](https://www.w3school.com.cn/jsref/index.asp)



1. 一些注意

   ```javascript
   js代码一般放在body的底部，用户使用会更好。
   
   输出语句
   window.alert();
   document.write();
   console.log();
   
   var和let，var是老大
   ==会先类型转换再比较，===全等于就不一样
   
   转换成数字
   var number1 = +"123"
   var number2 = parseInt("123");
   var number3 = +true;
   
   各种数据类型放在if条件判断中，会转换成布尔，这个很好用。
   if(str !=null && str.length >0); //java写法
   if(str)；//javascript可以利用这个特点，简化写法
       
   js很弱类型，这个写法很新颖。像lambda表达式一样的函数写法。
   var add=function(a,b){
       return a + b;
   }
   ```

   

2. BOM对象

   ```javascript
   window对象
   window.confirm();
   window.setTimeout(function(){
   	alert("welcome!");
   	},1000);
   window.setInterval(tip,1000);
   
   history对象
   history.back();
   history.forward();
   
   location对象
   loaction.href="www.baidu.com";
   ```

   

3. js能利用html DOM对象对html进行操作了

   ```javascript
   获取element
   getElementsByTagName();
   
   每个DOM对象中，别忘了style和innerHTML属性
   ```

   

4. js事件监听很被需要

   ```javascript
   onclick=""属性绑定事件
   document.getElementsById().onclick=""来绑定
   onfocus=""
   onblur=""
   onload=""
   onsubmit=""//返回true才会提交表单,表单验证好好试试
   ```

   

5. 福利：正则表达式

   ```javascript
   idea插件自动生成正则表达式
   var regex=/^\w{6,12}$/;
   var regex2=/^[1]\d{10}$/;
   str.test(regex1);
   ```

   

<hr>

### HTTP

> 从此处开始后面都是Web核心技术

基于TCP协议，不能共享数据。

常见的请求行和请求头

```tex
Host主机名
User-Agent浏览器版本
Accept-Language浏览器偏好语言
```

常见的响应行和响应体

```tex
Cache-Control:max-age=300，给这个响应缓存300秒
1xx响应中
2xx成功（200）
3xx重定向
4xx用户端错误（404）
5xx服务器端错误（500）
```



<hr>

### Tomcat

> jetty、IBM WebSpherer、WebLogic 



1. 既能封装HTTP协议，简化开发，又能够部署服务器。

   

2. 福利：控制台中文乱码，修改conf/logging.properties，
   windows改为GBK，linux就不用改

   

3. 基本使用

   ```xml
   改端口号：conf/server.xml
   <Connector port="8080" ... ... .../>
   
   war包放在./webapps/目录下会自动解压
   ```

   

4. idea部署Tomcat
   a）Edit Configuration集成本地的tomcat来配置
   b）tomcat maven插件（名字就叫这个）









<hr>

### Servlet

1. servlet由tomcat创建，service方法也是tomcat来调用

   

2. servlet其实可以在不访问的时候就被创建

   ```java
   @WebService(urlPatterns="/demo",loadOnStartup=1);
   默认负数，正数越小越优先
   ```

   

3. urlPattern有很多种写法来访问Servlet

   ```java
   @WebServlet(urlPatterns={"/demo7","/demo8"})
   @WebServlet(urlPatterns="/user/select")/* 越精确优先级越高 */
   @WebServlet(urlPatterns={"/user/*")
   @WebServlet(urlPatterns={"*.do")/* 不能加/ */
   @WebServlet(urlPatterns={"/")/* 会覆盖DefaultServlet（处理静态资源的Servlet，像a.html）*/
   @WebServlet(urlPatterns={"/*")/* 上一种和这一种写法很危险 */
   ```

   

4. 老版本Servlet3.0以前只能使用XML配置Servlet（现在不用了）

   ```xml
   //web.xml
   <servlet>
       <servlet-name>demo13</servlet-name>
       <servlet-class>com.ljt.web.LoginServlet</servlet-class>
   </servlet>
   
   <servlet-mapping>
       <servlet-name>demo13</servlet-name>
       <url-pattern>/demo13</url-pattern>
   </servlet-mapping>
   ```

   

5. 福利：使用request遇到中文乱码怎么办？你也许要知道URL编码。（据说tomcat8以后解决了这个问题）

   ```java
   post请求的解决方案
   request.setCharacterEncoding("UTF-8");//设置字符输入流的编码,需要放在代码最前面。
   解决
   get请求的解决方案/*post也可以这样解决*/
   - 解释一下，浏览器使用utf8字符集，解释成URL编码发出，
     但是tomcat在给发过来URL编码中没有用utf8解码。
     （tomcat默认用ISO-8859-1解码）。
   所以我们只需要把乱码的数据，打碎成字节，再转换。
   Byte bytes[]=str.getBytes("ISO-8859-1");//getBytes(StandardCharsets.ISO_8859_1);
   String s=new String(bytes,"utf8");
   /* 熟练一点，直接合起来 */
   str=new String(str.getBytes(StandardCharsets.ISO_8859_1),"utf8");
   ```

   

6. request除了一堆get方法，也可以forward请求转发

   ```java
   request.getRequestDispatcher("/servlet1").forward(request,response);
   ```

   

7. 福利：让你搞懂如何写url路径。
   如果是浏览器根据url找路径，url里面要写内部还是外部。
   如果是服务器的话，就不需要了。（response就是浏览器去找路径，请求转发不是）。

   ```java
   String contentPath=request.getcontentPath();
   response.sendRedirect(contentPath+"/demo1")
   ```

   

8. 福利：往浏览器写标签，不按照html显示。而且写中文会乱码。

   ```java
   response.setHeader("content-type","text/html");
   response.setContentType("text/html;charset=utf-8");
   ```

   

9. 福利：往浏览器写字节时，可以用点小工具，一行代码完成流的拷贝

   ```java
   apache开发的commons-io
   
   IOUtils.copy(fls,os);
   
   /*古早的写法
   byte[] buff=new byte[1024];
   int len=0;
   while((len = fis.read(buff) != -1)){
       os.write(buff,0,len);
   }*/
   ```

   

10. 福利：自己抽取工具类加上静态代码块，代码优化SqlSessionFactory的多次创建

    ```java
    首先是，同样的代码创建同样的SqlSessionFactory，代码重复了。
    另外，一个SqlSessionFactory其实就对应一个线程池，重复的工厂对于资源来说是浪费的。
    public class SqlSessionFactoryUtils{
        private static SqlSessionFactory sqlSessionFactory;
        static{
            src="mybatis-config.xml";
            InputStream is = Resources.getResourceAsStream(src);
            sqlSessionFactory =new SqlSessionFactoryBuilder().build(is);
        }
        
        public static SqlSessionFactory getSqlSessionFactory(){
            return this.sqlSessionFactory;
        }
    }
    ```





<hr>

### JSP

> 本质就是一个Servlet
>
> 随着jsp缺点逐渐被大家吐槽，jsp已经退出历史舞台了......（老的公司还在使用，还是要入门）
>
> Servlet  -  JSP  -  Servlet+JSP  -  Servlet+html+ajax(才是真正的前后端分离)

1. java中比如for循环截断，就可以写html了

2. 我们要使用${brands==1?"启用":"禁止"}，EL表达式

3. JSTL标签（需要导入jar包）

   ```jsp
   <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
   <c:if test=""></c:if>
   <c:forEach items="${...}" var="brand" varStatus="index">
       <td>${index.count}</td>
   </c:forEach>
   <c:forEach begin="1" end="10" step="1" var="1">
       <a href="#">${i}</a>
   </c:forEach>
   ```






<hr>

### MVC和三层架构

> Model View Controller
>
> 刚才我们就是使用这个架构
>
> M=JavaBean(Pojo、Domain、entity) V=JSP C=Servlet

> 三层架构（clean architecture）和MVC又有点不一样
>
> 表现层、业务逻辑层、数据访问层，分别对应下面的包名
>
> web或Controller、service、dao或mapper（和MyBatis的mapper不一样的）

后面的三大**框架**就是对三层**架构**的层层封装
表现层的**`SpringMVC`** / `Struts2`
业务逻辑层的**`Spring`**
数据访问层的**`MyBatis`** / `Hibername`

总结一下：MVC是一个大的概念，三层架构就是对MVC的具体实现。
Controller+View其实就是表现层。
Model（JavaBean）就是业务逻辑层和数据访问层。





<hr>

### 会话跟踪技术深入了解

> 后段注重发送cookie和获取浏览器发送给服务器的cookie



览器存储数据使用`cookie`

- `cookie`的实现是基于`HTTP`协议的。
- 让cookie有保质期，使用`setMaxAge();`。
- `cookie`不能存中文，我们使用URL编码把中文处理一下，`str = URLEncoder.encode(str,"utf8");`与`str = URLDecoder.decode(str,"utf8");`。



服务器存储数据使用`session`

- `session`是基于`cookie`实现的。(`JSESSIONID`)。
  正常关闭服务器，tomcat会自动把session序列化写入磁盘。

- `web.xml`决定session存活(100分钟后销毁session)

  ```xml
  <session-config>
      <session-timeout>100</session-timeout>
  </session-config>
  ```

- `session.invalidate()`，session能够自行销毁，登出账号可以使用。





<hr>

### Filter

> JavaWeb三大组件（`Servlet`、`Filter`、`Listener`）
>
> filter拦截请求和放行，也可以通用操作
>
> 登陆验证需要使用filter

放行前要对request进行处理，放行后对response进行处理。





<hr>

### Listener

可以对application、request、session的各个行为进行监听

我们一般只用`ServletContextListener`





<hr>

### AJAX

> Asynchronous JavaScript And XML，异步的JavaScript和XML。
>
> HTML和AJAX是属于前端的内容，在AJAX写xhttp.open时候要写最全的路径。
>
> 我们开发时，前后端一定是分离开发的。

[忘记怎么写了：https://www.w3school.com.cn/js/js_ajax_intro.asp](https://www.w3school.com.cn/js/js_ajax_intro.asp)

[AXIOS异步框架的使用：https://www.axios-http.cn/](https://www.axios-http.cn/)

异步交互案例：搜索联想、注册页面的用户名已存在了。

一般看到的js源码全部压缩成一行，就意味着可以少传输字符。

可以试着用axios的框架来验证用户名是否存在，与其用原生的ajax





<hr>

### JSON

> JavaScript Object Notation。JavaScript对象表示。
>
> 和js对象非常相似

`fastjson`可以将json转换Java对象





<hr>

### Vue

> 简化前端DOM
>
> idea配置`Vue`代码补全，可以下载`Vue.js`插件





<hr>

### Element UI

> 饿了么eleme出品的基于Vue的网站组建库
>
> 或者用bootstrap







### 福利

postman





