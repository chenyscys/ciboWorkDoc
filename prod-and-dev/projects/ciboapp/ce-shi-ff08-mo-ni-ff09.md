_3.29 http://192.168.3.29:8001/_

* 更新命令

update svn://192.168.3.29/svn/ciboapp/trunk /mnt/xvdb1/www/composer/ciboapp1

* 开启微信模拟授权

cd /mnt/xvdb1/www/composer/ciboapp1

vi .env.development

![](/assets/laravel微信模拟授权.png)

php artisan config:cache  --env=development

