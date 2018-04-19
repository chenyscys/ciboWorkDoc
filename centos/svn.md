* 安装

yum install subversion 

yum install -y git

* 启动  、关闭

svnserve -d -r /mnt/xvdb1/svndata

killall svnserve



* 清理

svn cleanup /www/cibowe/release1.0.1

