## lxrun 
对 LX 子系统执行管理操作(cmd/powershell)

用法:
 -  ` /install` - 安装子系统
        -  可选参数:
            -     /y - 不提示用户接受或创建子系统用户
-  `/uninstall` - 卸载子系统
    - 可选参数:
        -       /full - 执行完全卸载
        -       /y - 不提示用户确认
-  `/setdefaultuser` - 配置将用于启动 bash 的子系统用户。如果该用户不存在，则会创建该用户。
    - 可选参数:
        -       username - 提供用户名
        -       /y - 如果提供了用户名，则不提示创建密码
- `/update` - 更新子系统的包索引