2.17，阴天，伴有小雨，仿佛在暗示着什么？

早上9点30，同事告诉我29测试服务器出问题了，经过一番折腾，发现centos6.5系统变成 **只读文件系统**，很是尴尬。

问题：查看硬盘的挂载情况，mount命令后，出现一段warning：

```
mount: warning: /etc/mtab is not writable (e.g. read-only filesystem).
       It's possible that information reported by mount(8) is not
       up to date. For actual information about system mount points
       check the /proc/mounts file.
```

经百度查证，据说是被mount成只读模式了，需要重新mount根目录：

```
mount -o remount,rw /
```

至此，解决只读模式问题，不过出现新的问题，原本的文件盘不见了，用**df -h **一查只有一个盘：

```
Filesystem                     Size  Used Avail Use% Mounted on
/dev/mapper/vg_test36-lv_root   18G   16G  465M  98% /
tmpfs                          3.9G     0  3.9G   0% /dev/shm
/dev/xvda1                      18G   16G  465M  98% /boot
/dev/xvdb1                      18G   16G  465M  98% /mnt/xvdb1
sunrpc                          18G   16G  465M  98% /var/lib/nfs/rpc_pipefs
gvfs-fuse-daemon                18G   16G  465M  98% /root/.gvfs
```

之前的文件都不见了，那怎么办？

也很简单，查看一下盘名：

```
fdisk -l
```

会看到当前服务器的硬盘情况，接着把当前对应的文件夹下，空文件夹删掉，重新挂载一次

比如：我们的物理盘是/dev/xvdb1，此时由于重新mount后，变成了空文件夹。

现在把/mnt/xvdb1空文件夹删掉：

```
rm -rf /mnt/svdb1
```

接着再用 **df -h **查看，会发现，/dev/xvdb1 已经不见了。

这时候我们重新挂载一次：

```
mkdir /mnt/xvdb1   //先建一个空文件夹
mount /dev/xvdb1 /mnt/xvdb1/    //挂载
```

至此，解决。

参考文章：[https://www.jianshu.com/p/f552078d882e](https://www.jianshu.com/p/f552078d882e)

接着，由于重启过服务器，可能我们要重启一下服务：

1、网卡重启+sshd重启（这一步要在重启之后马上做，不然都没法用ssr连接，这一步请找小林哥）

```
service network restart
/etc/init.d/sshd restart
```

2、防火墙重启

```
service iptables restart
```

3、nginx，mysql，php等等的重启

