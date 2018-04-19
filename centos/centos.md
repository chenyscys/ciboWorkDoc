* 重启

shutdown -r now

* 端口

_centos6.5_

新增 /sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT

保存生效 /etc/rc.d/init.d/iptables save

查看端口 /etc/init.d/iptables status

* CPU

grep 'physical id' /proc/cpuinfo \| sort -u \| wc -l   \#查看 CPU 物理个数

grep 'core id' /proc/cpuinfo \| sort -u \| wc -l \#查看 CPU 核心数量

grep 'processor' /proc/cpuinfo \| sort -u \| wc -l \#查看 CPU 线程数

dmidecode -s processor-version \#查看 CPU  型号

cat /proc/cpuinfo \#查看 CPU 的详细信息

* 磁盘空间

df -lh

du -sh \*

* 查找文件

find / -name

* 拷贝目录

cp -Rf x1 x2 

