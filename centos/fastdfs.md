_3.34,3.35_

#### 安装

[http://blog.csdn.net/ricciozhang/article/details/49402273](http://blog.csdn.net/ricciozhang/article/details/49402273)

[http://369369.blog.51cto.com/319630/771169/](http://369369.blog.51cto.com/319630/771169/)

#### 配置目录

cd /etc/fdfs/

#### 启动命令

/usr/bin/fdfs\_trackerd /etc/fdfs/tracker.conf restart

/usr/bin/fdfs\_storaged /etc/fdfs/storage.conf restart

关闭

killall fdfs\_storaged

killall fdfs\_trackerd

#### 进程查看

netstat -tupln \| grep storaged

netstat -tupln \| grep trackerd

#### 开放端口

* cento6.5

/sbin/iptables -I INPUT -p tcp --dport 22122 -j ACCEPT

/sbin/iptables -I INPUT -p tcp --dport 23000 -j ACCEPT

/etc/rc.d/init.d/iptables save

#### 开机启动

echo "/usr/bin/fdfs\_storaged /etc/fdfs/storage.conf restart" &gt;&gt; /etc/rc.local

echo "/usr/bin/fdfs\_trackerd /etc/fdfs/tracker.conf restart" &gt;&gt; /etc/rc.local

chkconfig --add /etc/init.d/fdfs\_storaged

chkconfig --add /etc/init.d/fdfs\_trackerd

#### 日志查看

cat /home/data/fastdfs/base4storage/logs/storaged.log

cat /home/data/fastdfs/tracker/logs/trackerd.log

