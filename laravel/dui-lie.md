#### 服务端监听

php artisan queue:listen redis --queue=default,jobs.test,listeners.user,broadcast --delay=3 --sleep=3 --tries=3

#### 前端监听

laravel-echo-server start

