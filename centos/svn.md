_3.29_

#### 安装

yum install subversion

yum install -y git

#### 启动、关闭

svnserve -d -r /mnt/xvdb1/svndata

killall svnserve

#### 清理

svn cleanup 目录

#### svn账号管理

cd /mnt/xvdb1/svndata/svn/conf

![](/assets/svn.png)

修改authz、passwd文件

![](/assets/svn1.png)![](/assets/svn2.png)

