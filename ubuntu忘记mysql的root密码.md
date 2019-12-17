# ubuntu忘记mysql的root密码

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

