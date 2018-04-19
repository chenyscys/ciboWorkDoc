svn update svn://192.168.3.29/svn/ciboapp/branches/201801 /www/ciboapp/branches/201801

chmod -R 777 /www/ciboapp/branches/201801/storage/

chmod -R 777 /www/ciboapp/branches/201801/public/uploads/

chmod -R 777 public storage

php artisan config:cache  --env=production

