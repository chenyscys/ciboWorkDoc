

* 重启

shutdown -r now

端口

centos6.5

新增 /sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT

保存生效 /etc/rc.d/init.d/iptables save

查看端口 /etc/init.d/iptables status

