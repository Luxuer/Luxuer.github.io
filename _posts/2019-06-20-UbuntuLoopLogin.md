




# Ubuntu 16.04无限循环登录问题解决总结
## 问题描述
Linux图形界面下输入登陆密码正确，但闪回登陆界面. 
## 过往经验
这个问题我遇到过不下3次, 有不知不觉就解决了的(Ubuntu 14.04下), 有解决不了结果重装的(Debian下), 这次装好Ubuntu 16.04没多久就出现这个问题. 因为装好Ubuntu后因为驱动出现了很多问题(比如无法调整背光亮度, 系统挂起后无法通过按power键唤醒), 所以在Google的指导下做了好多莫名其妙的事情, 显然是自己的锅, 因此这次下定决心好好了解一下Debian系Linux的登录机制(Ubuntu继承自Debian). 
### 1. .Xauthority的权限
普通用户home目录下的隐藏文件.Xauthority的拥有者有可能被改成了root, 因此普通用户无法调用此文件进行身份验证. 在这种情况, 一般可以通过按下Ctrl+Alt+F1进入tty1终端, 然后利用普通用户的账号和密码登录终端, 在该用户home文件夹下可以查看.Xauthority的拥有者, 命令如下
``` bash
sudo ls -al .Xauthority
```
如果出现类似下面的
``` bash
-rw------- 1 root root 100  6月 19 17:09 .Xauthority
```
就说明.Xauthority的拥有者变成了root, 但是如果出现下面的
``` bash
-rw------- 1 luxuer luxuer 100  6月 19 17:09 .Xauthority
```
而luxuer是要登录的账户, 就说明.Xauthority的权限没有问题, 需要找其他原因. 
#### 解决办法
按下Ctrl+Alt+F1, 输入普通用户账号和密码登录终端tty1(该用户需要在sudoers组), 终端输入类似下面的命令
``` bash
sudo chown username:username .Xauthority
```
这里的username是指普通用户名字, 比如说
``` bash
sudo chown luxuer:luxuer .Xauthority
```
可以将.Xauthority文件的拥有者改为luxuer, 从而用luxuer账号就可以读取或修改该文件.  
**PS**: 关于.Xauthority文件  
.Xauthority文件可以在每个用户主目录中找到, 用于存储xauth用于X会话的身份验证. 启动X会话后, cookie将用于验证与该特定显示的连接. 您可以在xauth手册页中找到有关X身份验证和X权限的更多信息(在终端中键入`man xauth`).
因此, 如果您不是此文件的所有者, 则无法登录, 因为您无法在此处存储凭据.


### 2. 显卡驱动不兼容
我在出现这个问题的前一个操作应该是安装amd的显卡驱动amdgpu-pro, 然后Ubuntu的Software&Update通知我有东西要更新, 更新完后就关了笔记本, 再开的时候就开始登陆不上了. 因此极有可能是显卡驱动和Ubuntu更新(我比较怀疑Ubuntu更新, 官方的人没有好好测试, 网上很多问题都是它导致的), 于是我卸载了amd显卡驱动
``` bash
amdgpu-pro-uninstall
```
然后更新软件(如果是官方的锅, 他们一般很快会在下一次更新修复)
``` bash
sudo apt update
sudo apt upgrade
```
结果居然好了. 至此我还是没有明白到底是显卡驱动的锅还是Ubuntu更新的错, 所以我决定再安装amd显卡看问题会不会重现. 
在下载并解压好的显卡驱动文件夹下敲
``` bash
amdgpu-pro-install
```
结果....待续



