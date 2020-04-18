# 将源码包编译成deb包 - checkinstall

**翻译自：** https://help.ubuntu.com/community/CheckInstall

## 1.简介

`CheckInstall` 跟踪由`make install`或类似命令生成安装的所有文件，并创建`Slackware`, `RPM`或`Debian`包，将其添加到包的数据库，可以方便地卸载或分发软件包。

使用`CheckInstall`来替代`sudo make install`，由于后者可能将文件安装到文件系统的各种位置，导致在出现问题的情况下卸载困难。而且如果将来你安装的某个软件包中的某些文件和你现在编译安装的某些文件相同，则会导致你编译安装的软件出错甚至停止工作。

（实际上，不仅仅是`make install`，`CheckInstall`能跟踪任何命令所修改的文件，这是得它能够用于`apt`以外的的任何类型的软件包的安装，并使用包管理器跟踪其安装过程。）

`CheckInstall`不适合用于生成用于发形目的的软件包。不要使用该软件来为Ubuntu archive或PPA源的软件打包。请遵循相应的打包方法。

CheckInstall 的README文件："CheckInstall对Debian的支持尚未稳定，请小心使用。对于某些Debian系的操作系统，用户反馈该软件包工作正常，当然它在我的已安装了dpkg的Slackware开发环境下表现良好，但是在你的环境里可能各有不同。"

## 2.安装

执行以下命令从软件仓库进行安装：

```bash
sudo apt-get update && sudo apt-get install checkinstall
```

## 3.使用

编译安装时，不再使用：

```bash 
sudo make install
```

而是：

```bash
sudo checkinstall
```

执行命令时不带任何参数，`checkinstall`则会默认调用`make install`。如果你需要使用其他参数，则可以这样使用：

```bash
sudo checkinstall make install_package
```

The installed package can then also easily be removed via Synaptic or via the terminal: 
安装的包可以非常轻松地使用Synaptic或终端来删除：
```
sudo dpkg -r packagename
```

例如：

```bash 
sudo dpkg -r pidgin
```

**注意：** 生成的`.deb`包也可以在其他地方使用，极大地简化了同一软件包在大量机器上的安装过程。

## 4. 配合auto-apt使用checkinstall

You can use auto-apt when you want to build a simple package from source with checkinstall. You need to have auto-apt installed! 

你也可以配合`auto-apt`与`checkinstall`从源代码创建一个简单的软件包（需要安装`auto-apt`）：

不再使用：
```bash
./configure
```

请使用:

```bash
auto-apt run ./configure
```

如果依赖都可用，一个对话框会被打开，并要求你安装它们，剩下的则保持不变：

```bash 
make
sudo checkinstall
Related Links
CategorySoftware CategoryCommandLine 
```