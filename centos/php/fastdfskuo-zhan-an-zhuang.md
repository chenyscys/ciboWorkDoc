[http://www.cleey.com/blog/single/id/753.html](http://www.cleey.com/blog/single/id/753.html)

#### 安装fastdfs

cd /etc/fdfs

cp client.conf.sample client.conf

vi client.conf

#### php安装fastdfs扩展

phpize

./configure --with-php-config=/usr/bin/php-config

make

make install

cat fastdfs\_client.ini &gt;&gt; /etc/php.ini

#### 连接客户端client

cd /etc/fdfs/

vi client.conf

