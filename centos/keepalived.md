keepalived的搭建

安装：[http://www.linuxe.cn/post-266.html](http://www.linuxe.cn/post-266.html)



redis+keepalived配置：[https://blog.csdn.net/kjsayn/article/details/53411625](https://blog.csdn.net/kjsayn/article/details/53411625)



参数配置：[https://blog.csdn.net/mofiu/article/details/76644012](https://blog.csdn.net/mofiu/article/details/76644012)



关于设置了keepalived之后，双机都是master的问题是因为linux或者centos的防火墙阻止了keepalived的组播，此时会出现共享出来的虚拟IP会一直绑定在一台机子上，做不了**备备模式；**



解决方法，开启vrrp的组播：[http://blog.chinaunix.net/uid-20794884-id-5704461.html](http://blog.chinaunix.net/uid-20794884-id-5704461.html)



ps：备备模式，就是双机都为backup，并且设置了不抢占master，也即是当master宕机后，IP切到backup机子上后，master机子重启，自动变为备份，而不是抢占IP。

