---
title: Windows下Python2和Python3共存的方法——利用Py启动器
---

# Windows下Python2和Python3共存的方法——利用Py启动器

## 0x00 安装Python2和Python3
### 1. 下载安装包
从[官网](https://www.python.org/)下载Python2和Python3(版本必须3.3以上)安装包(本文讨论的Python版本分别为2.7和3.7).  
### 2. 安装
首先双击Python2安装包, 本文的Python2安装目录为`E:/Program Files/Python/Python27/`, 不要添加到环境变量PATH(默认是不添加的, 在这里强调一下, 下同).  
然后双击Python3安装包, 本文的Python3安装目录为`E:/Program Files/Python/Python37/`, 不要添加到环境变量PATH(默认是不添加的), 在Customize istallation中勾选py launcher(默认是勾选的).  
PS: Python2和Python3的安装顺序无所谓.   

## 0x01 启动和简单使用不同版本的Python
### 1. 启动不同版本的Python
#### 启动Python2
```cmd
py -2
```
#### 启动Python3
```cmd
py -3
```
PS: 不妨称同时安装了Python2和Python3的操作系统处于共存状态, 那么共存状态下的`py -2`就相当于只安装了Python2的系统中的`python`命令, 共存状态下的`py -3`就相当于只安装了Python3的系统中的`python`命令, 正如下面所介绍的, 只安装了Pyhon2的系统中的`pip`命令可以用`python -m pip`来替换, 那么在共存状态下对应的命令就是`py -2 -m pip`. 接下来只介绍`py -2`的相关用法, `py -3`的用法类似. 
### 2. 使用pip
说明: 只安装Python2的系统中的`pip`命令, 对应于共存状态的命令就是`py -2 -m pip`, 只要适当使用替换法, pip的相关命令都可以正常使用.  
#### 修改pip的默认下载目录
##### 查看pip模块所在的目录
```cmd
py -2 -m site --user-base
```
PS: 运行与pip有关的命令时, python会从目录USER_BASE中寻找已安装的pip模块, 如果在该目录下找不到, 会抛出错误.  Windows下Python2.7的USER_BASE默认是`%APPDATA%\Python27`. 
##### 查看pip下载第三方包的存放目录
```cmd
py -2 -m site --user-site
```
PS: USER_SITE就是**pip下载第三方包的存放目录**. Windows下Python2.7的USER_SITE默认是`%APPDATA%\Python\Python27\site-packages`. 
##### 查看pip的配置文件所在
```cmd
py -2 -m site -help
```
出现的第一行(类似于`D:\Program Files\Python\Python27\lib\site.py`)就是pip的配置文件所在, 根据该目录找到site.py文件并打开, 修改其中的USER_BASE和USER_SITE, 其中USER_BASE修改为刚刚的Python2安装目录(本文是`E:/Program Files/Python/Python27`), USER_SITE修改为安装目录下的`Lib/site-packages`文件夹(本文为`E:/Program Files/Python/Python27/Lib/site-packages`): 
```py -2
USER_SITE = "D:\Program Files\Python\Python27\Lib\site-packages"
USER_BASE = "D:\Program Files\Python\Python27"
```
#### 修改pip源为清华源
```cmd
:: 临时使用清华镜像源来更新pip到最新版本
py -2 -m pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pip -U
:: 设置pip源为清华源
py -2 -m pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```
#### 使用Python2的pip下载matplotlib模块
```cmd
py -2 -m pip install matplotlib
```















