yum -y  install autoconf

#### 下载phpredis 并解压

#### 编译安装

cd phpredis-3.1.1

make clean

phpize

./configure --with-php-config=/usr/bin/php-config

make && make install

