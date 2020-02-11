# shadowsocks 使用指南（Linux）

## GUI版本：shadowsocks-qt5

项目下载地址：https://github.com/shadowsocks/shadowsocks-qt5

官方帮助文档：https://github.com/shadowsocks/shadowsocks-qt5/wiki

![](img/2019-07-24&#32;21-54-57屏幕截图.png)

注意事项：
- 扫描或导入配置成功后注意本地端口是否已经配置了，如果没有，任意指定一个没有使用的端口；
- 配置端口后在系统设置中寻找网络代理配置项，设为手动，IP为127.0.0.1,端口为上一步配置的端口；
- 如果供应商提供的代理类型是SOCKS5，请在系统设置的HTTP代理一栏留空。若代理类型是HTTP(S)，请在SOCKS5代理一栏留空

![全局代理配置](img\2019_07_24_22_01_31屏幕截图.png)