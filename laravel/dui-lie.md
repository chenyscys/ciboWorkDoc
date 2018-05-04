#### 服务端监听

```
# 测试
php artisan queue:listen redis --queue=default,jobs.test,listeners.user,broadcast --delay=3 --sleep=3 --tries=3

# 正式
php artisan queue:work redis --queue=default,listeners,listeners.customEvent_log,broadcast --delay=3 --sleep=3 --tries=3
```

> 用 queue:work 方式启用队列，如果修改了相关代码，需要到3.50重启队列才能生效。

#### 前端监听

laravel-echo-server start

