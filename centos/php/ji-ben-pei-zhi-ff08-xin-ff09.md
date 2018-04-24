_centos7.4_

#### 配置目录、文件

cd /app/soft/php/etc/php-fpm.d/

vi /app/soft/php/etc/php-fpm.conf

#### 启动命令

systemctl restart php-fpm

systemctl start php-fpm

systemctl stop php-fpm

#### 编译模块

phpize

./configure --with-php-config=/app/soft/php/bin/php-config

#### 查看命令

php --modules

ps -ef\|grep php-fpm

