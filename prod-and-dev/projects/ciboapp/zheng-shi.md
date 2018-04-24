_3.27,3.28,3.32 _[http://service.cibohome.com](http://service.cibohome.com)

#### 发布更新svn

svn update svn://192.168.3.29/svn/ciboapp/branches/201801 /www/ciboapp/branches/201801

#### 设置目录权限

cd /www/ciboapp/branches/201801/

chmod -R 777 public storage

#### laravel缓存清理

php artisan config:cache  --env=production

php artisan route:cache

#### php编译缓存清理

cd /www/ciboapp/branches/201801/

rm -rf storage

更新项目svn

chmod -R 777 storage

