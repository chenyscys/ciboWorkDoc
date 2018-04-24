#### 配置目录

cd /etc/redis/

#### 查看进程

ps -ef\|grep redis

cd /var/run/ \#进程位置

日志位置

cd /var/log/redis

启动/关闭

redis-server /etc/redis/6379.conf

service redisd start

service redisd stop

查看详细信息

![](/assets/redis1.png)

redis-cli -h 10.10.10.11 -p 6379

压力测试

redis-benchmark -t set -c 20 -n 1000000 -r 100000000

开机启动

[_http://www.tuicool.com/articles/aQbQ3u_](#)

cp /etc/redis/redis.conf /etc/redis/6379.conf

cp redis\_init\_script /etc/init.d/redisd

开放端口

firewall-cmd --add-port=6379/tcp --permanent

firewall-cmd --add-port=26379/tcp --permanent

