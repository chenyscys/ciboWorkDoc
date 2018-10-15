#### 配置目录

cd /etc/redis/

### 查看进程

ps -ef\|grep redis

cd /var/run/ \#进程位置

#### 日志位置

cd /var/log/redis

#### 启动/关闭

redis-server /etc/redis/6379.conf 或

service redisd start

service redisd stop

#### 查看详细信息

![](/assets/redis1.png)

redis-cli -h 10.10.10.11 -p 6379

#### 压力测试

redis-benchmark -t set -c 20 -n 1000000 -r 100000000

#### 开机启动

[_http://www.tuicool.com/articles/aQbQ3u_](#)

cp /etc/redis/redis.conf /etc/redis/6379.conf

cp redis\_init\_script /etc/init.d/redisd

#### 需要开放端口

firewall-cmd --add-port=6379/tcp --permanent

firewall-cmd --add-port=26379/tcp --permanent

#### centos7开机启动redis

[https://blog.csdn.net/sjhuangx/article/details/79633112](https://blog.csdn.net/sjhuangx/article/details/79633112)

PS：文章里面创建用户组的方法写错了，应该是`sudo groupadd redis`

同时，设置开机启动的话，要把后台运行改为no

`ps aux | grep redis` 查看redis的运行pid

关于linux上systemctl命令介绍：[http://linux.51yip.com/search/systemctl](http://linux.51yip.com/search/systemctl)，设置开机启动时可以参考，便于理解



