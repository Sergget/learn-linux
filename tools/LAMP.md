# 搭建LAMP环境

### L==>Linux

### A==>Apache
*** 安装： ***
> apt install apache2

### P==>PHP
*** 安装： ***
> apt install php5

### M==>Mysql
*** 安装： ***
> apt install mysql-server

查看是否正确加载`mysql.so`(16.10需要)

> cat /etc/php/7.0/mods-available/mysqlnd.ini

才可以看到`extension=mysqlnd.so`

如果上调命令执行无结果，则安装php-mysql扩展：

> apt install php5-mysql

#### 流行的mysql管理工具
### `phpmyadmin`
