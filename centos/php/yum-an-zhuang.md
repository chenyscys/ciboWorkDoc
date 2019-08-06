> 安装源

```
$ yum install epel-release -y
$ rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
```

> 清除历史版本

```
$ yum -y remove php*
```

> 安装扩展包

```
# 可根据实际需要安装，本项目用到以下扩展
$ yum -y install php72w php72w-cli php72w-fpm php72w-common php72w-devel php72w-embedded php72w-gd php72w-mbstring php72w-mysqlnd php72w-opcache php72w-pdo php72w-xml php72w-pecl-redis php72w-mssql php72w-bcmath php72w-process php72w-soap
```

> 安装 fastdfs\_client 扩展

参考本教程：http://192.168.3.29:4000/centos/php/fastdfskuo-zhan-an-zhuang.html

> 安装完成以后，启动服务

```
$ systemctl enable php-fpm.service # 设置开机自启动
$ systemctl start php-fpm.service # 启动服务
```

> 其它命令

```
$ systemctl stop php-fpm.service # 关闭服务
$ systemctl restart php-fpm.service # 重启服务
```



