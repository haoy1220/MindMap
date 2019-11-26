# Mysql问题解决方案

#### mysql:1153 Got a packet bigger than ‘max_allowed_packet’ bytes的解决方法

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



