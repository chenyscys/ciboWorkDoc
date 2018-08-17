# 配置http的header自定义参数

以下，以29服务器的企划网站为例子。

通过Xshell连上服务器，进入`/app/soft/nginx/conf/conf.d/dev1.cibohome.conf`

编辑该文件：

![](/assets/nginx_http.png)

如上图，红色框那一行，这样我们在前端请求的header中，假如sessionKey字段，服务端就可以获取到该字段的值了。

```
fastcgi_param sessionKey $http_sessionKey;
```

不过，这里有两点要注意：

1、字段名不要带下横线“ - ”，不然很可能会失效；

2、配置完之后记得重启该网站；

