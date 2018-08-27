## 从零开始搭建fastdfs——nginx篇章

### 前言

上一篇文章，我们一起学习了fastdfs的安装，接下来，我们一起来学习一下跟nginx相关的配置与安装吧。

### 八、安装和配置fastdfs-nginx-module

1. 进入之前软件下载的文件夹：`cd /usr/local/soft`
2. 解压fastdfs-nginx-module\_v1.16.tar.gz文件：`tar -zxvf fastdfs-nginx-module_v1.16.tar.gz`
3. 修改配置config：
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



