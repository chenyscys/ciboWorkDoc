centos 6.5

php配置

vi /etc/php.ini 



fpm配置

cd /etc/php-fpm.d/  



编译模块

phpize

./configure  --with-php-config=/usr/bin/php-config



重启php

/etc/init.d/php-fpm restart

service php-fpm restart

