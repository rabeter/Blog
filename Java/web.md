# java Web

## servlet
生命周期
1. init 初始化
2. service
	1. doGet
	2. doPost
3. destroy回收销毁


@service() 处理url请求
@doGet/@doPost接受service的处理请求
getServletConfig() 获取在web.xml中的配置信息
getServletContext() 获取共享全局web.xml中的配置信息

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
setMaxAge
addCookie
getCookies
getName
getValue
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

