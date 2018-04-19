#### centos 6.5

* php配置

vi /etc/php.ini

* fpm配置

cd /etc/php-fpm.d/

* 编译模块

phpize

./configure  --with-php-config=/usr/bin/php-config

* 重启php

/etc/init.d/php-fpm restart 或service php-fpm restart

* 开机启动

chkconfig --add /etc/init.d/php-fpm

chkconfig php-fpm on

* 查看php版本、模块、进程

php -v

php --modules

ps -ef\|grep php-fpm

* 


