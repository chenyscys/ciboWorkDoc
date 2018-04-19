[http://www.cleey.com/blog/single/id/753.html](http://www.cleey.com/blog/single/id/753.html)

1、安装fastdfs模块，参考网址

2、php安装fastdfs扩展

* 安装扩展到php

phpize

./configure --with-php-config=/usr/bin/php-config

make

make install

cat fastdfs\_client.ini &gt;&gt; /etc/php.ini

* 连接客户端client

cd /etc/fdfs/

vi client.conf

