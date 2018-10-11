### redis cluster配置安装

1、首先安装redis，本次我们安装的redis版本是4.0.11，安装步骤也比较简单，请自行上网搜索~

---

2、模拟配置，我们用2台虚拟机来模拟集群，分别在每台虚拟机上开启三个redis服务以及三个端口+三个集群总线端口，

原因：

redis集群不仅需要开通redis客户端连接的端口，而且需要开通集群总线端口

集群总线端口为redis客户端连接的端口 + 10000

如redis端口为6379

则集群总线端口为16379

故，所有服务器的点需要开通redis的客户端连接端口和集群总线端口。

---

3、至于redis的配置，可以参考以下文章[https://blog.csdn.net/u010963948/article/details/78963572](https://blog.csdn.net/u010963948/article/details/78963572)，

[http://www.redis.cn/topics/cluster-tutorial.html](http://www.redis.cn/topics/cluster-tutorial.html)，这里要注意一点：配置文件加一句daemonize yes，设置为后台运行，这样，你才可以运行多个redis~而不用多开shell窗口了。

4、完成多个redis的配置后，在集群前我们要安装ruby，文章中的安装方法只适合3.X的redis，而我们是高大上的4.x版本，所以会有版本不适应的问题，所以我们要安装最新的ruby跟gem，可参考文章

[https://www.cnblogs.com/ding2016/p/7903147.html](https://www.cnblogs.com/ding2016/p/7903147.html)

注意：每次重启系统后，要使用ruby命令前要执行 `scl  enable  rh-ruby23 bash`

文章装的是2.3版本，我们可以装2.5版本，直接把`rh-ruby23`改成 `rh-ruby25`就可以了

5、进入服务器的redis服务时，如果用get方法获取不同服务上保存的字段，用常规的打开启动方法是不行，

要在 进入某个redis服务时 加上-c参数来启动集群模式：

`./redis-cli -c -p 7000`

6、创建集群时失败，可能是因为某个redis服务配置错了或者含有旧数据，此时可以进入该redis服务，执行2条命令：

```
flushall
cluster reset
```

这样就可以清除了。

