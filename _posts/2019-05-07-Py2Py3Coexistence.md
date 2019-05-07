# Windows下Python2和Python3共存的方法————利用Py启动器

## 0x00 安装Python2和Python3
### 1. 下载安装包
从[官网](https://www.python.org/)下载Python2和Python3(版本必须3.3以上)安装包.  
### 2. 安装
首先双击Python2安装包, 本文安装目录为E:/Program Files/Python/Python2/, 不要添加到环境变量PATH(默认是不添加的, 在这里强调一下, 下同).  
然后双击Python3安装包, 本文安装目录为E:/Program Files/Python/Python3/, 不要添加到环境变量PATH(默认是不添加的), 在Customize istallation中勾选py launcher(默认是勾选的).  
  
PS: Python2和Python3的先后顺序无所谓.   

## 0x01 启动和简单使用不同版本的Python
### 1. 启动不同版本的Python
#### 启动Python2
···cmd
py -2
···
#### 启动Python3
···cmd
py -3
···
PS: 不妨称同时安装了Python2和Python3的操作系统处于共存状态, 共存状态下的py -2就相当于只安装了Python2的系统中的python命令, 共存状态下的py -3就相当于只安装了Python3的系统中的python命令, 正如下面所介绍的, 
### 2. 使用不同版本的pip
#### 修改pip源为清华源

#### 使用Python2的pip下载matplotlib
···cmd
py -2 -m pip install matplotlib
















