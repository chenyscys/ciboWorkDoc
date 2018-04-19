更新svn

svn update svn://192.168.3.29/svn/ciboapp/branches/201801 /www/ciboapp/branches/201801

设置目录权限

cd /www/ciboapp/branches/201801/

chmod -R 777 public storage



清理缓存

php artisan config:cache  --env=production

