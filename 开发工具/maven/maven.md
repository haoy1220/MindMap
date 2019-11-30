### 修改maven的下载源地址

1. 在放maven的安装目录conf/文件夹下找到settings.xml；

2. 搜索mirrors，在<mirrors></mirrors>标签下添加：

   ```xml
   <mirror>
       <id>alimaven</id>
       <name>aliyun maven</name>
       <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
   <mirrorOf>central</mirrorOf>
   </mirror>
   <mirror>
       <id>alimaven</id>
       <mirrorOf>central</mirrorOf>
       <name>aliyun maven</name>
       <url>http://maven.aliyun.com/nexus/content/repositories/central/</url>
   </mirror>
   ```

3. 在idea的setting中搜索找到maven，将相应的目录设置完整

   ![image-20191130161405189](.\images\image-20191130161405189.png)

