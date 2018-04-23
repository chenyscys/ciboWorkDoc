> 3.26 Nginx 配置文件：/app/soft/nginx/conf/conf.d/curl\_reload\_config.conf

```
 server {
    listen       7901;
        index index.php index.html index.htm;
        location ~ \.php$ {
            root   /www/nginx_reload_config/;
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
            include        fastcgi_params;
        }
    }
```

> 访问此地址重启Nginx：http://192.168.3.26:7901/reload.php



