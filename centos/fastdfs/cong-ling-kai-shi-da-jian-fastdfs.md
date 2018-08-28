## 从零开始在centos上搭建fastdfs文件管理系统

## 前言

最近，在我搞小程序搞的醉生梦死之际，教导主任突然发话了：那个谁，去了解一下fastdfs，搞个centos7搭建一下，然后好好研究一下迁移。

当然一开始我是拒绝的，但在主任的淫威之下，咱还是得老老实实的去看文档学习，并且搭建起来。

---

### 一、安装系统

最先开始的，当然是centos7的本地搭建，没有系统，搞个锤子的fastdfs哦。

安装教程可看本文档的另一篇文章，这里就不再赘述。时光机：[虚拟机上安装centos7](http://192.168.3.29:4000/centos/centos/xu-ni-ji-shang-an-zhuang-centos7.html)。

---

### 二、安装工具，命令，环境，创建文件夹

首先，我们进入local文件夹：`cd /usr/local`

创建一个soft文件夹来存放下载的文件：`mkdir /usr/local/soft`

并进入该文件夹：cd `/usr/local/soft`

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

接下来创建存放文件的文件夹，

进入home文件夹，`cd /home`，创建文件夹fastdfs，`mkdir fastdfs`，然后进入fastdfs，`cd fastdfs`

在fastdfs里面创建2个文件夹，`mkdir tracker`，`mkdir storage`

至此，安装前的准备就差不多结束了~~

---

### 三、安装libfastcommon

1. 进入soft文件夹：`cd /usr/local/soft`
2. 解压libfastcommon： `tar -zxvf V1.0.7.tar.gz`
3. 进入FastDFS：`cd /usr/local/soft/libfastcommon-1.0.7/`
4. 编译：`./make.sh`
5. 安装： `./make.sh install`

注意安装的路径：libfastcommon默认安装到了/usr/lib64/这个位置。

---

### 四、安装FastDFS

1. 进入soft文件夹：`cd /usr/local/soft`
2. 解压FastDFS： `tar -zxvf V5.05.tar.gz`
3. 进入FastDFS：`cd /usr/local/soft/fastdfs-5.05/`
4. 编辑配置文件：`vi make.sh`   将TARGET\_PREFIX=$DESTDIR/usr改成TARGET\_PREFIX=$DESTDIR/usr/local
5. 编译：`./make.sh`
6. 安装：`./make.sh install`

FastDFS主程序设置的目录为/usr/local/lib/，而我们的安装目录为/usr/lib64,所以我们需要创建/usr/lib64/下的一些核心执行程序的软连接文件。

```
命令：ln -s /usr/lib64/libfastcommon.so /usr/local/lib/libfastcommon.so
命令：ln -s /usr/lib64/libfastcommon.so /usr/lib/libfastcommon.so
命令：ln -s /usr/local/lib64/libfdfsclient.so /usr/local/lib/libfdfsclient.so
命令：ln -s /usr/local/lib64/libfdfsclient.so /usr/lib/libfdfsclient.so
```

---

### 五、配置tracker

1. 进入配置目录，`cd /etc/fdfs/`
2. 复制一份 tracker.conf.sample 命名为 tracker.conf，`cp tracker.conf.sample tracker.conf`
3. 编辑修改tracker.conf，修改base_path，store_\_lookup的值：

   ```
   base_path=/home/fastdfs/tracker   //这里的路径就是我们上面创建的tracker文件夹的路径
   store_lookup=1    //0:轮询，1：指定某个组；2：负载均衡策略
   store_group=group1   //当store_lookup为1时，指定的组名
   ```

4. 开放端口22122，操作命令为

   查看端口：firewall-cmd --list-ports

   开放端口：firewall-cmd --zone=public --add-port=22122/tcp --permanent   \(permanent表示永久生效\)

   重启防火墙：firewall-cmd --reload

5. 启动tracker，并检查是否配置成功

   ```
   启动tracker命令：/etc/init.d/fdfs_trackerd start
   查看进程命令：ps -el | grep fdfs
   停止tracker命令：/etc/init.d/fdfs_trackerd stop
   ```

   这里，启动之后查看进程命令可能发现没执行成功，这时可以先执行停止命令，再查看，然后再启动就可以了。启动成功之后，tracker文件夹中就会自动创建data跟logs文件夹。

6. 设置tracker开机启动：

   ```
   cd /etc/init.d/
   chkconfig --add fdfs_strackerd chkconfig fdfs_trackerd on
   ```

7. tracker.conf配置文件参数解释可以找官方文档，地址为：

   [http://bbs.chinaunix.net/thread-1941456-1-1.html](http://bbs.chinaunix.net/thread-1941456-1-1.html)

### 六、配置storage

1. 进入配置目录，`cd /etc/fdfs/`
2. 复制一份 storage.conf.sample 命名为 storage.conf，`cp storage.conf.sample storage.conf`
3. 编辑修改storage.conf：

   ```
   group_name=group1    //这里group_name的值要跟tracker中的store_group统一
   base_path=/home/fastdfs/storage
   store_path0=/home/fastdfs/storage
   store_path_count=1

   //tracker_server对应的是多台tracker的地址
   tracker_server=192.168.30.23:22122
   tracker_server=192.168.30.24:22122

   http.server_port=8888    //这里的端口设置要跟nginx开放的端口一致
   ```

4. 开放端口23000，操作命令为

   ```
   查看端口：firewall-cmd --list-ports
   开放端口：firewall-cmd --zone=public --add-port=23000/tcp --permanent   (permanent表示永久生效)
   重启firewall：firewall-cmd --reload
   ```

5. 启动storage，并检查是否配置成功

   ```
   启动storage命令：/etc/init.d/fdfs_storaged start
   查看进程命令：ps -el | grep fdfs
   停止storage命令：/etc/init.d/fdfs_storaged stop
   ```

   启动成功之后，storage文件夹中就会自动创建data跟logs文件夹。

6. 设置storage开机启动：

   ```
   cd /etc/init.d/ 
   chkconfig --add fdfs_storaged chkconfig fdfs_storaged on
   ```

7. storage.conf配置文件参数解释可以找官方文档，地址为：

   [http://fredlong.iteye.com/blog/2287899](http://fredlong.iteye.com/blog/2287899)

### 七、配置client

1. 进入配置目录，`cd /etc/fdfs/`
2. 复制一份 client.conf.sample 命名为 client.conf，`cp client.conf.sample client.conf`
3. 编辑修改client.conf：

   ```
   base_path=/home/fastdfs/tracker

   //tracker_server对应的是多台tracker的地址
   tracker_server=192.168.30.23:22122
   tracker_server=192.168.30.24:22122
   ```

4. 调用上传命令上传文件，操作命令为

   ```
   /usr/local/bin/fdfs_upload_file /etc/fdfs/client.conf /etc/fdfs/client.conf.sample
   ```

5. 这里上传的时候，假如只开了一台tracker，就会报错，另一个tracker\_server还没有配置的时候，就会出现上传，同步失败的情况。

6. 配置没问题，上传同步成功的话就会出现该文件的路径：  
   `group1/M00/00/00/wKjHglYshRGAfbrTAAAFtTzeg5c.sample`



