## 从零开始在centos上搭建fastdfs文件管理系统

## 前言

最近，在我搞小程序搞的醉生梦死之际，教导主任突然发话了：那个谁，去了解一下fastdfs，搞个centos7搭建一下，然后好好研究一下迁移。当然一开始我是拒绝的，但在主任的淫威之下，咱还是得老老实实的去看文档学习，并且搭建起来。

---

### 一、安装系统

最先开始的，当然是centos7的本地搭建，没有系统，搞个锤子的fastdfs哦。

安装教程可看本文档的另一篇文章，这里就不再赘述。时光机：[虚拟机上安装centos7](http://192.168.3.29:4000/centos/centos/xu-ni-ji-shang-an-zhuang-centos7.html)。

### 二、安装工具，命令，环境

由于安装的是最小化版本，所以有很多命令是没有的，所以我们要手动安装~~

```
yum install zip unzip                   安装解压，压缩命令

yum install make cmake gcc gcc-c++      安装gcc环境

yum install vim-enhanced                安装vim会自动帮我们安装perl

yum install lrzsz                       上传下载功能

yum install net-tools                   安装netstat 和 ifconfig命令

yum -y install wget                     安装wget下载命令

安装nginx依赖包
yum install pcre
yum install pcre-devel
yum install zlib
yum install zlib-devel

wget https://github.com/happyfish100/libfastcommon/archive/V1.0.7.tar.gz  下载libfastcommon源码
wget http://jaist.dl.sourceforge.net/project/fastdfs/FastDFS%20Nginx%20Module%20Source%20Code/fastdfs-nginx-module_v1.16.tar.gz   fastdfs-nginx-module源代码
wget https://github.com/happyfish100/fastdfs/archive/V5.05.tar.gz    下载FastDFS源代码
wget http://nginx.org/download/nginx-1.8.0.tar.gz    下载nginx服务器源代码
```



