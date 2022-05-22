# 9.1 service命令

启动指定服务

```
sudo service 服务名 start
```

停止指定服务

```
sudo service 服务名 stop
```

重启指定服务

```
sudo service 服务名 start
```

查看所有服务

```
sudo service --status-all
```

查看指定服务的状态

```
sudo service 服务名 status
```

注意：所有的服务都存放在/etc/init.d/ 目录下，可以直接操作/etc/init.d/ 下的指定服务，如：

```
sudo service mysql restart
sudo /etc/init.d/mysql restart
```

 两者效果是一致的