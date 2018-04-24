安装

[_https://www.linuxidc.com/Linux/2015-05/117378.htm_](#)

yum install -y rpcbind nfs-utils

启动、关闭

service nfs restart

service nfs stop

service rpcbind stop

service rpcbind restart

开机启动

chkconfig rpcbind on

chkconfig nfs on

配置

源服务器加入目标机器

vi /etc/exports

/home/www/ciboapp/ 192.168.3.29\(rw,sync,no\_root\_squash\)

目标机器挂载源服务器

showmount -e 10.10.10.12

mount -t nfs 10.10.10.12:/home/www/ciboapp/ /home/www/ciboapp/  -o proto=tcp -o nolock

umount /home/www/ciboapp/

开放端口

firewall-cmd --permanent --add-service=rpc-bind

firewall-cmd --permanent --add-service=mountd

firewall-cmd --permanent --add-port=2049/tcp

firewall-cmd --permanent --add-port=2049/udp

firewall-cmd --reload

