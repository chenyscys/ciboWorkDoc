cento6.5

/sbin/iptables -I INPUT -p tcp --dport 22122 -j ACCEPT

/sbin/iptables -I INPUT -p tcp --dport 23000 -j ACCEPT

/etc/rc.d/init.d/iptables save





centos7.4

firewall-cmd --add-port=8012/tcp --permanent

systemctl restart firewalld.service 

netstat -lnp\|grep 8012



