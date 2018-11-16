keepalived的搭建

安装：[http://www.linuxe.cn/post-266.html](http://www.linuxe.cn/post-266.html)

yum安装：[http://blog.51cto.com/afterdawn/1888682](http://blog.51cto.com/afterdawn/1888682)

建议用yum安装，可以用命令启动，停止，重启keepalived，不过要注意添加一个新的用户 keepalived\_script；

redis+keepalived配置：[https://blog.csdn.net/kjsayn/article/details/53411625](https://blog.csdn.net/kjsayn/article/details/53411625)

参数配置：[https://blog.csdn.net/mofiu/article/details/76644012](https://blog.csdn.net/mofiu/article/details/76644012)

关于设置了keepalived之后，双机都是master的问题是因为linux或者centos的防火墙阻止了keepalived的组播，此时会出现共享出来的虚拟IP会一直绑定在一台机子上，做不了**备备模式；**

解决方法，开启vrrp的组播：[http://blog.chinaunix.net/uid-20794884-id-5704461.html](http://blog.chinaunix.net/uid-20794884-id-5704461.html)

ps：备备模式，就是双机都为backup，并且设置了不抢占master，也即是当master宕机后，IP切到backup机子上后，master机子重启，自动变为备份，而不是抢占IP。

另外，要注意的是一台服务器不能开启多个keepalived进程，

[http://www.mamicode.com/info-detail-313367.html](http://www.mamicode.com/info-detail-313367.html)

