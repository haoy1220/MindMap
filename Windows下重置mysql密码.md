# Windows下重置mysql密码

1. 在任务管理器中关闭mysql服务；

2. 在mysql安装bin目录下启动cmd，`mysqld -nt --skip-grant-tables`；

3. 另外开启一个cmd，无密码方式进入mysql，开始修改密码：

   ```mysql
   update mysql.user set password=PASSWORD('新密码') where User='root';
   
   flush privileges; 
   
   quit;
   ```

4. 重启mysql服务就好了。

