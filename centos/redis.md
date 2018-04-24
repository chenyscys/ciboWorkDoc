

http://yanshisan.blog.51cto.com/7879234/1377992

配置目录

cd /etc/redis/



\#启动redis

redis-server /etc/redis/6379.conf



启动哨兵集群

redis-sentinel /etc/redis/sentinel16.conf

redis-sentinel /etc/redis/sentinel15.conf

redis-sentinel /etc/redis/sentinel11.conf

