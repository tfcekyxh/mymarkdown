### 会话技术案例（登陆记住我、注册验证码）

##### 登陆

登陆成功user存储在session里面

错误信息就是在div用EL表达式

记住就是写cookie

##### 注册

转发

请求验证码防止浏览器缓存，就直接使用时间。时间一去不复返。

请求的验证码存session里面

checkcode工具类自己找一下。

### filter案例（登陆验证）

implements Filter

跟登陆注册有关的在filter之前也要放行（login.jsp的css等）；

```java
String[] urls = {"/login.jsp","/imgs/","/css/","/loginServlet","register.jsp","registerServlet"};
String url=request.getRequestURL().toString();
for(String u : urls){
    if(url.contains(u)){
        chain.doFilter(request,response);
        return;
    }
}
......
```

### Ajax案例（验证用户是否存在）

onblur失去焦点事件

style.display='';

### AXIOS+JSON案例（查询所有）

##### 查询所有

页面加载之后再获取所有

```javascript
window.onload =function (){
    axios({
        method:"",
        url:""
    }).then(function (resp){
        
    });
}
```

json数据有中文

```java
response.setContentTye("text/json;charset=utf-8");
response.getWriter().write(jsonString);
```

innerHTML拼接字符串

##### 新增品牌（异步操作）

不需要用submit了，submit只能同步

### Vue案例（简化列表数据的查询和添加功能）

_this提高作用域

mouted（）执行异步查询

### Element案例（综合案例前的网页做好）

### 综合案例

##### 环境搭建

模块导入idea

sql构建数据库

前端做好了

##### 功能列表

一般都是Mapper - Service - html 

注意service我们也不仅仅是写死的，把service做成接口，然后用impl实现类就好了。



###### Servlet优化（手写springmvc）（或者SSM框架）

像Service的实现一样，@WebServlet("/brand/*")通配符目录映射，对字符串反射。但是我们不能用HttpSerlvet接口了。

```java
public class BaseServlet extends HttpServlet{
    protected void service()......{
        uri=req.getURI();
        index=lastIndexOf(url);
        methodName=subString(index);
        
        
        /*这里的this你要好好想想，应该是BrandServlet会使用service，所以这个this就是BrandServlet.0*/
        cls=this.getClass();
        cls.getMethod(methodName,HttpServletRequest.class,HttpServletResponse.class);
        cls.invoke(this,req,resp);
    }
}
```



万物皆可以对象



分页查询，有的时候我们用到面向对象创建PageBean，为了提升复用性可以采用泛型\<T>，（手写分页插件的代码）



条件查询，三个关系用AND，动态sql，需要带分页。既有url的参数，也有请求体的参数。



前端关于this和_this的优化，ES6提供了箭头函数`resp =>{}`会根据上下文自动找this





























