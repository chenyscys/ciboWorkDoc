## 从零开始搭建fastdfs——nginx篇章

### 前言

上一篇文章，我们一起学习了fastdfs的安装，接下来，我们一起来学习一下跟nginx相关的配置与安装吧。

### 八、安装和配置fastdfs-nginx-module

1. 进入之前软件下载的文件夹：`cd /usr/local/soft`
2. 解压fastdfs-nginx-module\_v1.16.tar.gz文件：`tar -zxvf fastdfs-nginx-module_v1.16.tar.gz`
3. 这里要注意，假如按照上一篇的文章安装fastdfs，这里就不用修改配置了，因为fastdfs跟fastcommon安装在/usr/local/include/中，假如修改了这个配置，会导致下面的nginx编译安装失败。

   如把fastdfs跟fastcommon安装在/usr/include，那么请修改配置config：

   ```
    cd /usr/local/soft/fastdfs-nginx-module/src
    vim config
    修改配置，在config找到下面这行
    CORE_INCS="$CORE_INCS /usr/local/include/fastdfs /usr/local/include/fastcommon/"
    改成
    CORE_INCS="$CORE_INCS /usr/include/fastdfs /usr/include/fastcommon/"
   ```

4. 复制一份mod\_fastdfs.conf 到 /etc/fdfs 目录下，并修改它：

   ```
   cd /usr/local/soft/fastdfs-nginx-module/src
   cp mod_fastdfs.conf /etc/fdfs/

   vim /etc/fdfs/mod_fastdfs.conf
   connect_timeout=10    //超时时长
   tracker_server=192.168.30.23:22122
   tracker_server=192.168.30.24:22122
   storage_server_port=23000
   url_have_group_name=true    //是否允许从地址栏访问
   group_name=group1
   base_path=/home/fastdfs/storage
   store_path_count=1
   store_path0=/home/fastdfs/storage
   group_count = 0  //这里0代表只有单个组

   最后
   [group1]
   group_name=group1
   storage_server_port=23000
   store_path_count=1
   store_path0=/home/fastdfs/storage
   ```

5. 复制FastDFS里的2个文件http.conf和mime.types，到/etc/fdfs目录中。  
   `cp /usr/local/soft/fastdfs-5.05/conf/http.conf /etc/fdfs/                  
    cp /usr/local/soft/fastdfs-5.05/conf/mime.types /etc/fdfs/`

6. 创建一个软连接：在/fastdfs/storage文件存储目录下创建软连接，将其链接到实际存放数据的目录。  
   `ln -s /home/fastdfs/storage/data/ /home/fastdfs/storage/data/M00`

### 九、nginx安装及绑定

在每台storage上安装Nginx，而这里我们的tracker跟storage是同一台服务器，这点跟网上别人的文章不同，请注意~

安装步骤：

1. 进入软件目录：`cd /usr/local/soft`
2. 解压nginx：`tar -zxvf nginx-1.8.0.tar.gz`
3. 进入目录：`cd nginx-1.8.0`
4. 设置配置：`./configure --add-module=/usr/local/soft/fastdfs-nginx-module/src/`
5. 编译安装：`make && make install`
6. 配置nginx：

   ```
   cd /usr/local/nginx/conf
   vim nginx.conf
   ```

   将server中的listen监听端口改为8888：`listen  8888`; 这里要注意端口号要跟storage.conf的配置一样；

   另外在server新增一个location：

   ```
   location ~/group([0-9])/M00 {
       ngx_fastdfs_module;
   }
   ```

7. 开放端口8888，操作命令为

   ```
   查看端口：firewall-cmd --list-ports
   开放端口：firewall-cmd --zone=public --add-port=8888/tcp --permanent   (permanent表示永久生效)
   重启防火墙：firewall-cmd --reload
   ```

8. 启动命令：`/usr/local/nginx/sbin/nginx`

9. 重启命令：`/usr/local/nginx/sbin/nginx -s reload`

10. 在这里，启动nginx可能会遇到一个报错：

    ```
    /usr/local/nginx/sbin/nginx: error while loading shared libraries: libfdfsclient.so: cannot open shared object file: No such file or directory
    ```

    这是因为找不到libfdfsclient.so，解决方法：

    ```
    cp /usr/lib/libfdfsclient.so /usr/lib64/
    ```

    将/usr/lib中的该文件复制一份到lib64中就可以解决了

### 十、参考文档：

1. [手把手教你搭建FastDFS集群（上）](https://blog.csdn.net/u012453843/article/details/68957209)

2. [手把手教你搭建FastDFS集群（中）](https://blog.csdn.net/u012453843/article/details/69055570)

3. [手把手教你搭建FastDFS集群（下）](https://blog.csdn.net/u012453843/article/details/69172423)

4. [fastdfs+nginx安装配置](https://blog.csdn.net/ricciozhang/article/details/49402273)

5. [FastDFS教程Ⅰ-文件服务器安装与Nginx配置](https://www.cnblogs.com/wlandwl/p/fastdfs.html)



