#### 安装

yum -y install docker

service docker start

systemctl enable docker \#开机启动

#### 卸载

yum list installed \| grep docker

yum -y remove xxxx

#### 进程查看

docker ps

docker ps -a

#### 删除镜像

docker rmi xx

#### 进入容器

docker exec -it 1d4479188964 /bin/bash

#### 国内镜像源

vi /etc/docker/daemon.json

{

"registry-mirrors": \["[https://j5mqvjwe.mirror.aliyuncs.com"\](https://j5mqvjwe.mirror.aliyuncs.com"\)\]

service docker restart

}

