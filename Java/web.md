# java Web

## servlet
java Servlet用作HTTP客户端与服务器端之间的请求处理，数据库与应用程序之间的中间层。
生命周期
1. init 初始化
2. service
	1. doGet
	2. doPost
	3. doPut
	.....
3. destroy回收销毁

使用Servlet读取表单数据
- getParameter 调用request.getParameter()方法来获取表单参数的值。
- getParameterValues如果参数返回多个值（例如复选框），则调用此方法。
- getParameterNames  当前请求中的所有参数的完整列表，则调用此方法。

@service() 处理url请求
@doGet/@doPost接受service的处理请求
getServletConfig() 获取在web.xml中的配置信息
getServletContext() 获取共享全局web.xml中的配置信息




-----
webapp
	css
	js
	images
	html
	META-INF
	WEB-INF
		lib
		classes
		web.xml


### Cookie
保存在浏览器端的标识用户信息

缺点：
1. 大小和数量的限制
2. 数据安全问题
setMaxAge 设置最大有效时间
getMaxAge 返回最大值
addCookie 添加Cookie对象数组
getCookies 返回Cookie对象的数组
getName 返回Cookie name
setValue 设置Cookie关联值
getValue 返回Cookie值
''' java
Cookie userNameCookie = new Cookie("userName", userName);
Cookie pwdCookie = new Cookie ("pwd",password);
response.addCookie(userNameCookie);
response.addCookie(pedCookie);
'''

### Session
服务器端保存用户标识数据

setMaxInactiveInterval设置有效期
getSession创建Session
getAttribute("userName")获取session值
invalidate()失效Session

### 过滤
- public void init（FilterConfig filterConfig）
- public void doFilter（ServletRequest，ServletResponse，FilterChain）
- public void destroy（）

''' java

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.util.*;


public class LogFilter implements Filter  {
   public void  init(FilterConfig config) throws ServletException {
      
      // Get init parameter 
      String testParam = config.getInitParameter("test-param"); 

      //Print the init parameter 
      System.out.println("Test Param: " + testParam); 
   }
   
   public void  doFilter(ServletRequest request, ServletResponse response,
      FilterChain chain) throws java.io.IOException, ServletException {

      // Get the IP address of client machine.
      String ipAddress = request.getRemoteAddr();

      // Log the IP address and current timestamp.
      System.out.println("IP "+ ipAddress + ", Time " + new Date().toString());

      // Pass request back down the filter chain
      chain.doFilter(request,response);
   }

   public void destroy( ) {
      /* Called before the Filter instance is removed from service by the web container*/
   }
}
'''
### error异常
当一个servlet抛出一个异常时，Web容器会搜索web.xml中使用异常类型元素的配置，使其与抛出的异常类型相匹配。
web.xml中的error-page元素来指​​定响应某些异常或HTTP 状态代码的servlet的调用。

### JDBC
