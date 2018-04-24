

cd /app/soft/php/etc/php-fpm.d/

/app/soft/php/etc/php-fpm.conf

\#\#/usr/local/php/etc/php-fpm.conf

systemctl restart php-fpm



./configure --with-php-config=/app/soft/php/bin/php-config

php --modules

ps -ef\|grep php-fpm

