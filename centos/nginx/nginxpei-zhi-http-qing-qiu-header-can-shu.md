# nginx配置http请求header参数

最近，在折腾小程序，需要小程序请求的header参数里面添加一个sessionKey的参数，然后后端通过这个值来做登录校验，身份获取等等。

不过，由于本地环境与服务器环境不同，本地是apache，服务器是nginx，两个环境对于header头部的定义跟规则不同，导致了在 nginx服务器上，获取不到header中的sessionKey。

那怎么办呢？只能求助我们伟大的教导主任——村长，在村长的深厚的nginx功力下，啪啪啪几下，就把这个问题解决了，顺带丢给我一个https，请收下我的膝盖~~~

那么村长是怎么解决这个问题呢？让我来为你们一一解答：

首先用Xshell连上服务器，抵达我们这个网站的nginx配置文件，路径如下：/app/soft/nginx/conf/conf.d/dev1.cibohome.conf，

![](/assets/nginx_http.png)

上面红色框那一行就是新增参数sessionKey的语句。

```
fastcgi_param sessionKey $http_sessionKey;
```

这里有几个注意点：

1、参数名不要带下横线，否则不行；

2、配置完之后要重启；

到此，就解决了~~



