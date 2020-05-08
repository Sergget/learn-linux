# 7.3 搭建一个webdav服务器

## 简介
webdav是“Web-based Distributed Authoring and Versioning”的简称。作为FTP的代替，在局域网内便捷地共享、传输文件。本文简单介绍在ubuntu/debian上搭建webdav服务器。

## 安装
1. 安装Apache2服务器
   ```
   sudo apt install apache2
   ```
2. 测试工具cadaver*:
   
    cadaver是一款命令行下的webdav工具
   ```
   sudo apt install cadaver
   ```

## 配置
1. 启用相关模块
   ```
   sudo a2enmod dav_fs
   //启用dav_fs时会自动启用dav模块
   sudo a2enmod dav_lock
   ```
2. 重启 Apache2 服务:
   ```
   sudo service apache2 restart
   ```
3. 创建虚拟主机目录:
   ```
   mkdir /media/data
   chown www-data:www-data /media/data
   ```
4. 创建用户:
   ```
   sudo htpasswd -c /media/me.dav sergget
   // 这里会要求你设置密码，后面登录时会用到，用户名即为 sergget
   sudo chown root:www-data /media/me.dav
   sudo chmod 640 /media/me.dav
   ```
5. 配置虚拟主机:
   ```
   sudo vim /etc/apache2/sites-available/webdav.conf
   ```
   在文件中插入以下内容并保存
   ```xml
   <VirtualHost *:80>
           ServerAdmin webmaster@localhost
           DocumentRoot /media/data/
           <Directory /media/data/>
                   Options Indexes MultiViews
                   AllowOverride None
                   Require all granted
           </Directory>
    
           Alias /webdav /media/data
    
           <Location /webdav>
              DAV On
              AuthType Basic
              AuthName "webdav"
              AuthUserFile /media/me.dav
              Require valid-user
          </Location>
   </VirtualHost>
   ```
   到Apache2下链接配置文件：
   ```
   cd /etc/apache2/sites-enabled/
   sudo ln -s ../sites-available/webdav.conf webdav.conf
   sudo rm 000-default.conf
   ```
   配置完成后重启apache2服务使配置生效
   ```
   sudo service apache2 restart
   ```

## 验证
使用命令行 cadaver 进入登录
```
cadaver http://127.0.0.1/webdav/
```