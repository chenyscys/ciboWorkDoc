## 从零开始搭建fastdfs——nginx篇章

### 前言

上一篇文章，我们一起学习了fastdfs的安装，接下来，我们一起来学习一下跟nginx相关的配置与安装吧。

### 八、安装和配置fastdfs-nginx-module

1. 进入之前软件下载的文件夹：`cd /usr/local/soft`
2. 解压fastdfs-nginx-module\_v1.16.tar.gz文件：`tar -zxvf fastdfs-nginx-module_v1.16.tar.gz`
3. 这里要查看一下/usr/include跟/usr/local/include，看看fastdfs跟fastcommon两个文件夹的在哪，再修改配置。

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
   `ln -s /home/fastdfs/storage/data/ /home/fastdfs/storage/data/M00`这里的软链接不配置好像也不影响，建议先不配置~

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

### 十一、缩略图，代理转发，缓存，缓存删除配置：

1、查看nginx装了那些模块：

```
/usr/local/nginx/sbin/nginx -V
```

2、如果按照文章安装的话，我们需要加载安装nginx以及对应模块：

```
./configure --prefix=/app/soft/nginx  --add-module=/home/app/fastdfs-nginx-module/src --add-module=/home/app/ngx_cache_purge-2.3 --with-http_image_filter_module
```

这里一共有三个模块：fastdfs-nginx-module，ngx\_cache\_purge，http\_image\_filter\_module；

其中缩略图模块是nginx自带的。

3、编译

```
make && make install
```

如果不想重新安装覆盖nginx，请看文章：[nginx添加新模块](https://www.cnblogs.com/654wangzai321/p/8000780.html)

```
4、修改nginx配置
```

首先为了方便管理，我们把每个站点的配置单独抽离出来，放到conf.d文件夹里面，在nginx.conf中全部引入，以下是nginx.conf的配置：

```
events {
    use epoll;
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    server_tokens  off;
    client_max_body_size 500M;
    proxy_headers_hash_max_size 51200;
    proxy_headers_hash_bucket_size 6400;
    fastcgi_intercept_errors on;
    include /app/soft/nginx/conf/conf.d/*.conf; //就是引入全部配置文件

    proxy_connect_timeout 5;
    proxy_read_timeout 60;
    proxy_send_timeout 5;
    proxy_buffer_size 16k;
    proxy_buffers 4 64k;
    proxy_busy_buffers_size 128k;
    proxy_temp_file_write_size 128k;
    proxy_temp_path /home/temp_dir;
    proxy_cache_path /home/cache/fastdfs levels=1:2 keys_zone=fastdfs:200m inactive=7d max_size=30g;
}
```

关于proxy\_cache的配置相关可查看文章：[利用Proxy Cache使Nginx对静态资源进行缓存](https://blog.csdn.net/czp11210/article/details/28596649)

5、在conf.d文件夹中创建fastdfs.conf跟7011.fastdfs.conf配置文件：

```
#fastdfs服务配置以及缩略图如下：

#server_name  localhost;

    #charset koi8-r;

    #access_log  logs/host.access.log  main;

#缩略图配置开始
    limit_rate_after 5m;
    limit_rate 1m;

    location ~ /g1/M00/(.*)\.(jpg|gif|png|jpeg)_([0-9]+)x([0-9]+)_([0-9]+){
        ngx_fastdfs_module;

        set $w $3;
        set $h $4;

        if ($w != “0”) {
            rewrite /g1/M00/(.+)\.(jpg|gif|png|jpeg)_(\d+)x(\d+)_(\d+)$ /g1/M00/$1.$2 break;
        }

        if ($h != "0") {
            rewrite g1/M00/(.+)\.(jpg|gif|png|jpeg)_(\d+)x(\d+)_(\d+)$ g1/M00/$1.$2 break;
        }

        image_filter resize $w $h;
        image_filter_buffer 2M;
        image_filter_jpeg_quality 95;
        image_filter_sharpen $5;
    }


    location ~ /g1/M01/(.*)\.(jpg|gif|png|jpeg)_([0-9]+)x([0-9]+)_([0-9]+){
        ngx_fastdfs_module;

        set $w $3;
        set $h $4;

        if ($w != “0”) {
            rewrite /g1/M01/(.+)\.(jpg|gif|png|jpeg)_(\d+)x(\d+)_(\d+)$ /g1/M01/$1.$2 break;
        }

        if ($h != "0") {
            rewrite g1/M01/(.+)\.(jpg|gif|png|jpeg)_(\d+)x(\d+)_(\d+)$ g1/M01/$1.$2 break;
        }

        image_filter resize $w $h;
        image_filter_buffer 2M;
        image_filter_jpeg_quality 95;
        image_filter_sharpen $5;
    }

#缩略图配置结束，fastdfs配置开始

    location ~/g([0-9])/M00 {
        ngx_fastdfs_module;
    }

    location ~/g([0-9])/M01 {
        ngx_fastdfs_module;
    }
```

关于缩略图配置，请看文档：[nginx使用image\_filter生成缩略图 -- fasdfs海量图片缩略图整合](https://blog.csdn.net/clevercode/article/details/52278482)

```
#这是代理转发以及缓存与删除缓存的配置：

upstream fdfs_7011_backserver { //负载均衡
  server 10.10.10.15:7001 weight=1 max_fails=2 fail_timeout=30s;
  server 10.10.10.16:7001 weight=1 max_fails=2 fail_timeout=30s;
}


server {
    client_body_timeout 5s;
    client_header_timeout 5s;

    listen 7011;
#    server_name www1.zhsumarc.com;

    location ~ /purge(/.*) {  //删除缓存文件配置
      allow     192.168.5.144;
      deny      all;
      proxy_cache_purge  fastdfs $host$1$is_args$args;
    }
    location / {
      add_header X-Cache $upstream_cache_status;
      proxy_cache fastdfs;
      proxy_cache_valid  200 206 304 301 302 10d;
      proxy_cache_key $host$uri$is_args$args;
      proxy_set_header Host $host;
      proxy_set_header X-Forwarded-For $remote_addr;
      proxy_set_header X-Forwarded-Host $server_name;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header   Cookie $http_cookie;
      proxy_pass http://fdfs_7011_backserver;
  }
}
```

关于缓存删除ngx\_cache\_purge模块的文章：[Nginx缓存配置及nginx ngx\_cache\_purge模块的使用](https://www.cnblogs.com/Eivll0m/p/4921829.html)

### 十、参考文档：

1. [手把手教你搭建FastDFS集群（上）](https://blog.csdn.net/u012453843/article/details/68957209)

2. [手把手教你搭建FastDFS集群（中）](https://blog.csdn.net/u012453843/article/details/69055570)

3. [手把手教你搭建FastDFS集群（下）](https://blog.csdn.net/u012453843/article/details/69172423)

4. [fastdfs+nginx安装配置](https://blog.csdn.net/ricciozhang/article/details/49402273)

5. [FastDFS教程Ⅰ-文件服务器安装与Nginx配置](https://www.cnblogs.com/wlandwl/p/fastdfs.html)

6. [nginx添加新模块](https://www.cnblogs.com/654wangzai321/p/8000780.html)

7. [利用Proxy Cache使Nginx对静态资源进行缓存](https://blog.csdn.net/czp11210/article/details/28596649)

8. [nginx使用image\_filter生成缩略图 -- fasdfs海量图片缩略图整合](https://blog.csdn.net/clevercode/article/details/52278482)

9. [Nginx缓存配置及nginx ngx\_cache\_purge模块的使用](https://www.cnblogs.com/Eivll0m/p/4921829.html)


