##### [http://yanshisan.blog.51cto.com/7879234/1377992](http://yanshisan.blog.51cto.com/7879234/1377992)

#### 集群配置

_集群的前提是redis先做好主从关系_

cd /etc/redis/

![](/assets/sentinal.png)

![](/assets/sentinel2.png)

#### 启动哨兵集群

_开启3个哨兵，当其中有2个哨兵\(三分之二）确认失败后，才切换主redis库_

redis-sentinel /etc/redis/sentinel16.conf

redis-sentinel /etc/redis/sentinel15.conf

redis-sentinel /etc/redis/sentinel11.conf

#### 查看进程/集群信息

ps -ef\|grep sentinel

redis-cli -h 10.10.10.13 info replication

