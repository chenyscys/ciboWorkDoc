_3.26_

#### 服务上下线

cd /app/soft/nginx/conf/conf.d

vi service.cibohome.conf

![](/assets/3.26反向代理.png)

_注释\#为下线_

/app/soft/nginx/sbin/nginx -s reload

#### 配置错误页面

在反向代理服务器配置统一的错误页面：

1、首先统一配置 40x，50x，的页面路径

```

error_page 404 /error.html;
location = /error.html {
        root   /home/www;
}
```

2、开启proxy\_intercept\_errors

```
proxy_intercept_errors on；
```

一 般在server中加上面一句或者 location中加都可以， 然后重启即可



