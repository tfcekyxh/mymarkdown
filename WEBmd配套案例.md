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

