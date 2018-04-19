_3.29_

* 更新命令

update svn://192.168.3.29/svn/ciboapp/trunk /mnt/xvdb1/www/composer/ciboapp

* 设置目录权限

cd /mnt/xvdb1/www/composer/ciboapp

chmod -R 777 public storage

* laravel缓存清理

php artisan config:cache  --env=production

php artisan route:cache

* php编译缓存清理

cd /mnt/xvdb1/www/composer/ciboapp

rm -rf storage

更新项目svn

chmod -R 777 storage

