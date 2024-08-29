# 过滤器

一：过滤器概述

1.什么是过滤器

二：过滤器详细

1.过滤器的四种拦截方式

三：过滤器的应用场景

1.案例一：分IP统计访问次数
2.案例二：粗粒度权限管理
3.案例三：全站编码问题
4.案例四：页面静态化（图书管理小项目）

## 一：过滤器概述

### 1.什么是过滤器(别看没用)

过滤器是JavaWeb三大组件之一，它与Servlet很相似！不过它是用来拦截请求的，而不是用来处理请求的。
当用户请求某个Servlet时，会先执行部署在这个请求上的Filter，如果Filter“放行”，那么会继续执行用户请求的Servlet；如果Filter不放行，那么就不会执行用户请求的Servlet

Filter是单例的
实现方式：

写一个类实现Filter接口来实现
在web.xml中进行配置**（现在大家都不用了）**

```xml
<filter>
	   <filter-name>AFilter</filter-name>
	   <filter-class>net.xyz.filter.AFilter</filter-class>
  </filter>
  <filter-mapping>
	  <filter-name>AFilter</filter-name>
	  <url-pattern>/AFilter</url-pattern>
  </filter-mapping>
```
三个生命周期方法：
```java
public class AFilter implements Filter {

    /**
     * Default constructor. 
     */
    public AFilter() {
        // TODO Auto-generated constructor stub
    }
    
    /**
     * 销毁之前执行，Filter会在服务器关闭时销毁
     */
    public void destroy() {
    	System.out.println("过滤器死亡了");
    }
    
    /**
     *每次过滤时都会被执行
     */
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
    	// TODO Auto-generated method stub
    	// place your code her
    	// pass the request along the filter chain
    	System.out.println("拦截你");
    }
    
    /**
     * 创建之后马上执行，Filter会在服务器启动时就创建
     */
    public void init(FilterConfig fConfig) throws ServletException {
    	// TODO Auto-generated method stub
    	System.out.println("过滤器出生了");
    }

}
```

FilterCongfig：

获取初始化参数 ：getInitParameter（）
获取过滤器名称：getFilterName（）
获取appliction：getServletContext（）
Filter Chain：
doFilter(ServletRequest,ServletResponse)
放行，相当于调用了目标servlet的service()方法！调用完之后会继续执行后面的代码

## 二：过滤器详细

多过滤器：

doFilter(ServletRequest,ServletResponse)：
当有多个过滤器时，会执行下一个过滤器，如果没有，会执行目标servlet
执行顺序：
有多个Filter时，执行顺序按\<filter-map>的执行顺序执行

### 1.过滤器的四种拦截方式

在\<filter-mapping>中进行配置

```xml
      <dispatcher>REQUEST</dispatcher> ：拦请求。默认配置
      <dispatcher>FORWARD</dispatcher>  ：拦转发
      <dispatcher>INCLUDE</dispatcher>： 拦包含
      <dispatcher>ERROR</dispatcher>：拦错误
```


## 三：过滤器的应用场景

### 1.案例一：分IP统计访问次数

统计工作需要在所有资源之前执行，那么就可以放到Filter中了。这个过程不做拦截操作，用Map来存储数据，用ip做key,用访问次数做value,因为是全局变量，数据存在ServletContext中

Listener用来创建资源：
```java
package ipCount;

import java.util.LinkedHashMap;
import java.util.Map;

import javax.servlet.ServletContext;
import javax.servlet.ServletContextEvent;
import javax.servlet.ServletContextListener;
import javax.servlet.annotation.WebListener;

/**
 * 服务器启动时创建一个map对象用来保存ip,和次数
 *
	 */
	@WebListener
	public class AListener implements ServletContextListener {

    /**
     * Default constructor. 
     */
        public AListener() {
        // TODO Auto-generated constructor stub
        }

	/**
     * @see ServletContextListener#contextDestroyed(ServletContextEvent)
     */
        public void contextDestroyed(ServletContextEvent sce)  { 
        
    
	}
	
    /**
     * @see ServletContextListener#contextInitialized(ServletContextEvent)
     */
        public void contextInitialized(ServletContextEvent sce)  { 
         // TODO Auto-generated method stub
    	ServletContext application= sce.getServletContext();
        Map<String,Integer>map=new LinkedHashMap<String,Integer>();
        application.setAttribute("map", map);
	    }
}
```


Filter用来统计访问次数：

```java
public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        /*
         * 1.得到context中的map
         * 2.获取当前请求的IP ,如果map中存在，则数量加1并保存到map中
         * 3.如果不存在，将当前IP添加到map中并设置访问次数为1
         * */
         request.setCharacterEncoding("utf-8");
         response.setContentType("text/html;charset=utf-8");
         Map<String,Integer> map=(Map<String, Integer>) application.getAttribute("map");
         String ip=request.getRemoteAddr();
         if(map.containsKey(ip)) {
            int num=map.get(ip);
            System.out.println(ip);
            System.out.println(1);
            map.put(ip, num+1);
        }else {
            map.put(ip,1);
        }
        application.setAttribute("map", map);//更新map      
        chain.doFilter(request, response);//不要拦截请求
}
```


### 2.案例二：粗粒度权限管理

该应用分为三个角色，游客，会员，和管理员，每个人的角色默认是游客，而登录时使用用户名的话是会员，名字中包含xyz的则是管理员。现在使用filter控制user界面和admin界面的访问。
实现：

通过session存储用户名
在Filter中获取后判断是否允许通过还是拦截
Servlet：

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		/*
		 * 1.获取用户名判断用户名是否包含xyz
		 * 2.如果包含，就是管理员
		 * 3.如果不包含，就是普通用户
		 * 要把登录的用户保存到session中
		 */
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/htmll;charset=utf-8");
		String name=request.getParameter("username");
		if(name.contains("xyz")) {//是管理员
			request.getSession().setAttribute("admin", name);
		}else {//就是普通会员
			request.getSession().setAttribute("user", name);
		}
		request.getRequestDispatcher("/index.jsp").forward(request,response);
}
```

userFilter：

```java
public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html;charset=utf-8");
		/*
		/*
		 * 只有管理员和会员才可以进入
		 */
		HttpServletRequest req=(HttpServletRequest) request;
		String name;
		name=(String) req.getSession().getAttribute("admin");
		if(name!=null) {
			chain.doFilter(request, response);//是管理员直接放行
			return;
		}
		name=(String) req.getSession().getAttribute("user");
		if(name!=null) {
			chain.doFilter(request, response);//是普通会员直接放行
		}else {
			response.getWriter().write("你就是个普通游客，速走");
			
		}
		
	}
```

adminFilter:

```java
	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		request.setCharacterEncoding("utf-8");
		response.setContentType("text/html;charset=utf-8");
		/*
		 * 只有管理员才可以进入
		 */
		HttpServletRequest req=(HttpServletRequest) request;
		String name;
		name=(String) req.getSession().getAttribute("admin");
		if(name!=null) {
			chain.doFilter(request, response);//是管理员直接放行
			
		}else {
			response.getWriter().write("反正你不是管理员");
			req.getRequestDispatcher("/login.jsp").forward(request, response);
		}
		
	}
```
### 3.案例三：全站编码问题

```java
public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
	    request.setCharacterEncoding("utf-8");
	    response.setContentType("text/html;charset=utf-8");
		chain.doFilter(request, response);
}
```
### 4.案例四：页面静态化（图书管理小项目）

第一步 ：写一个小项目:图书管理
页面：

> 链接页面 :link.jsp
>
> 查询所有
>
> 查看SE分类
>
> 查看EE分类
>
> 查看框架分类
>
> 查询结果页面：show.jsp

Servlet:
-BookServlet
findAll()–>查看所有图书
findByCategoary（）–>按分类进行查询

BookDao:
Linst<Book> findAll()
List findByCategoary(int categoary)

domain:Book类

第二步： 什么是页面静态化！
首次访问去数据库获取数据，然后把数据保存到一个html页面中，二次访问，就不再去数据库获取了，而是直接显示html。
好处：直接加载html页面速度会快很多，但是只适合长时间数据保持不变的东西