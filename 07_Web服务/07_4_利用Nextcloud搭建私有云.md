# 7.4 利用Nextcloud搭建私有云

## 简介
本文中Nextcloud服务器安装在ubuntu-server上， 使用snap打包安装。snap包使用方便，权限相较于apt较为复杂，本文中一并介绍使用nextcloud的snap包时遇到的一系列问题。

## 安装
```
sudo snap install nextcloud
```

安装完成后，在浏览器内输入服务器地址即可访问，nextcloud默认的http运行在80，https运行在443端口

## 更改数据存储位置

### 思路
考虑到数据存储硬盘和系统盘往往是分开的，因此我们往往使用另一块硬盘存储数据，而且考虑使用方便，数据盘的挂载点往往在不在nextcloud默认的目录下。但是正常安装的snap包是无法访问其他位置的。考虑到数据存取的问题，snap包往往提供connect接口，允许snap包访问特定的位置。而nextcloud的snap包仅提供了一个media的接口，用于访问系统下`/media`下的内容，因此我们在挂载数据盘时，务必挂载到`/media`目录下，并且正确配置数据文件夹的权限。

### 步骤
#### 创建文件夹、配置权限
cd 到数据盘挂载点下（如*/media/sdb*），
```
mkdir data && sudo chown -R root:root data
```

#### 连接snap权限
```
sudo snap connect nextcloud:removable-media
```

#### 更改数据文件夹位置配置
1. 如果还没有创建第一个账户：

```
sudo vim /var/snap/nextcloud/current/nextcloud/config/autoconfig.php
```

将directory的值更改为
```
 // ...
 'directory' => '/media/sdb/data',
 // ...
```

2. 如果已经创建了第一个账户：

```
sudo vim /var/snap/nextcloud/current/nextcloud/config/config.php
```

将directory的值更改为
```
 // ...
 'directory' => '/media/sdb/data',
 // ...
```

停止nextcloud包运行：
```
sudo snap disable nextcloud
```

将数据文件夹转移到新的位置：
```
sudo mv /var/snap/nextcloud/common/nextcloud/data /media/sdb/data
```

重新启动nextcloud包的运行：
```
sudo snap enable nextcloud
```

## 更改运行端口

查看当前nextcloud包的运行端口：
```
sudo snap get nextcloud ports
```

输出：
```
Key          Value
ports.http   80
ports.https  443
```

设定nextcloud包的运行端口：
```
sudo snap set nextcloud ports.http=81 ports.https=445
```