_centos 6.5_

#### php配置

#### 配置

vi /etc/php.ini

* centos6.5

cd /etc/php-fpm.d/

* centos7.4

cd /app/soft/php/etc/php-fpm.d/

vi /app/soft/php/etc/php-fpm.conf

#### 编译模块

phpize

* centos6.5

./configure  --with-php-config=/usr/bin/php-config

* centos7.4

./configure --with-php-config=/app/soft/php/bin/php-config

#### 启动

/etc/init.d/php-fpm restart

service php-fpm restart



#### 开机启动

chkconfig --add /etc/init.d/php-fpm

chkconfig php-fpm on

#### 查看php版本、模块、进程

php -v

php --modules

ps -ef\|grep php-fpm

