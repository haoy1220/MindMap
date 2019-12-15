# Mysql问题解决方案

#### 1、mysql:1153 Got a packet bigger than ‘max_allowed_packet’ bytes的解决方法

备份还原或数据导入报错1153：Got a packet bigger than‘max_allowed_packet’bytes的问题

这个问题可以有2个解决方法：

1.临时修改：

```
mysql>set global max_allowed_packet=524288000; #修改 512M
```

2.修改my.cnf(windows下my.ini)，需重启mysql。
在 [MySQLd] 部分添加一句（如果存在，调整其值就可以）：
max_allowed_packet=256M （根据实际情况调整数值）

可通过命令：

```
show VARIABLES like '%max_allowed_packet%’;
```

查看是否修改成功！



#### 2、ubuntu忘记mysql的root密码--解决方案

1. 安全模式登陆

   ```shell
   sudo /etc/init.d/mysql stop # 停止mysql服务
   
   #[ ok ] Stopping mysql (via systemctl): mysql.service.
   
   sudo /usr/bin/mysqld_safe --skip-grant-tables --skip-networking & #这里可能会出错
   
   #出错就执行下面两行
   sudo mkdir -p /var/run/mysqld
   sudo chown mysql:mysql /var/run/mysqld
   #然后重新输入
   sudo /usr/bin/mysqld_safe --skip-grant-tables --skip-networking &
   
   #不出错直接往下进行
   mysql -u root #无密码进入
   
   ```

2. 修改密码

   ```mysql
   use mysql;
   
   update user set authentication_string=PASSWORD("这里输入你要改的密码") where User='root'; #修改密码
   
   update user set plugin="mysql_native_password"; #如果没这一行可能也会报一个错误，因此需要运行这一行
   
   flush privileges; #更新所有操作权限
   
   quit; #退出
   ```

3. 重新登录

   ```shell
   sudo /etc/init.d/mysql stop
   sudo /etc/init.d/mysql start # reset mysql
    
   mysql -u root -p
   ```





#### 3、Windows下重置mysql密码

1. 在任务管理器中关闭mysql服务；

2. 在mysql安装bin目录下启动cmd，`mysqld -nt --skip-grant-tables`；

3. 另外开启一个cmd，无密码方式进入mysql，开始修改密码：

   ```mysql
   update mysql.user set password=PASSWORD('新密码') where User='root';
   
   flush privileges; 
   
   quit;
   ```

4. 重启mysql服务就好了。



#### 4、MySQL命令执行sql文件的两种方法

##### 方法一，在 Windows 下使用 cmd 命令执行（或 [Unix](http://www.lezhu99.com/list-10-71.html) 或 [Linux](http://www.lezhu99.com/list-10-72.html) 控制台下）

【Mysql的bin目录】\mysql –u用户名 –p密码 –D数据库<【sql脚本文件路径全名】，示例：

```shell
C:\MySQL\bin\mysql –uroot –p123456 -Dtest<C:\test.sql
```

注意：
A、如果在 sql 脚本文件中使用了 use 数据库，则 -D数据库 选项可以忽略
B、如果【Mysql的bin目录】中包含空格，则需要使用“”包含，如：“C:\Program Files\MySQL\bin\mysql” –u用户名 –p密码 –D数据库<【sql脚本文件路径全名】
C、如果 sql 没有创建数据库的语句，而且数据库管理中也没有该数据库，那么必须先用命令创建一个空的数据库。

##### 方法二，进入 MySQL 控制台（如：MySQL 5.5 Command Line Client），使用 source 命令执行

```mysql
Mysql>source 【sql脚本文件的路径全名】 或 Mysql>\. 【sql脚本文件的路径全名】

# 示例：

source C:\test.sql 或者 \. C:\test.sql
```


打开 MySQL Command Line Client，输入数据库密码进行登录，然后使用 source 命令或者 \.



