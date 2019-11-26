# Tomcat



### 一、什么是Tomcat

 Tomcat简单的说就是一个**运行JAVA的网络服务器**，**底层是Socket**的一个程序，它也是**JSP和Serlvet的一个容器**。 

**总结三个功能：**

- web服务器；
- jsp容器；
- servlet容器。



### 二、为什么我们需要用到Tomcat

它可以提供网络服务，让别人可以访问我们的网站页面。

![](.\images\微信图片_20191124164035.jpg)



### 三、Tomcat目录结构

- bin：存放启动和关闭Tomcat的一系列脚本文件。
- conf：存放Tomcat服务器的各种配置文件。
  -  `server.xml`该文件用于配置server相关的信息，比如tomcat启动的端口号，配置主机(Host) 
  -  `web.xml`文件配置与web应用（web应用相当于一个web站点） 
  -  `tomcat-user.xml`配置用户名密码和相关权限. 
- lib：存放Tomcat服务器的支撑jar包。
- logs：存放Tomcat的日志文件。
- temp：存放Tomcat运行时产生的临时脚本。
- webapps：web应用所在的目录。
- work：Tomcat的工作文件，用于存放**jsp被访问后生成对应的server文件和.class文件** 。



### 四、Tomcat的web站点目录规范

![](.\images\微信图片_20191124164947.jpg)



#### 设置站点首页

在WEB-INF/web.xml文件中加入：

```xml
<welcome-file-list>       
		<welcome-file>xxxx.html</welcome-file>
</welcome-file-list>
```



### 五、Tomcat配置虚拟目录

#### 为什么要配置

- 如果把所有web站点的目录都放在webapps下，可能导致**磁盘空间不够用**，也**不利于对web站点目录的管理**【如果存在非常多的web站点目录】
- 把**web站点的目录分散到其他磁盘管理就需要配置虚拟目录【默认情况下，只有webapps下的目录才能被Tomcat自动管理成一个web站点】**
- 把web应用所在目录交给web服务器管理，这个过程称之为虚拟目录的映射。

#### 配置方法一：

1. 找到Tomcat目录下/conf/server.xml文件 ；
2.  在server.xml中的节点下添加如下代码。

```xml
<Context path="/访问时输入的web项目名" docBase="站点目录的绝对路径" />
```



#### 配置方法二：

- 进入到conf\Catalina\localhost文件下，创建一个xml文件，**该文件的名字就是站点的名字。** 





