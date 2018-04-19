vi /etc/php-fpm.d/www.conf



修改配置

pm=dynamic

pm.max\_children=100

pm.start\_servers=10

pm.min\_spare\_servers=10

pm.max\_spare\_servers=100

pm.max\_requests = 500

