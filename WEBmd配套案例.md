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

