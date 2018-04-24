_centos 6.5_

#### php配置

vi /etc/php.ini

#### fpm配置

cd /etc/php-fpm.d/

#### 编译模块

phpize

* centos6.5

./configure  --with-php-config=/usr/bin/php-config

* centos7.4

./configure --with-php-config=/app/soft/php/bin/php-config

#### 启动

* centos6.5

/etc/init.d/php-fpm restart 或service php-fpm restart

* centos7.4

systemctl restart php-fpm

systemctl start php-fpm

systemctl stop php-fpm

#### 开机启动

chkconfig --add /etc/init.d/php-fpm

chkconfig php-fpm on

#### 查看php版本、模块、进程

php -v

php --modules

ps -ef\|grep php-fpm

