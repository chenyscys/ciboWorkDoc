# 虚拟机上安装centos7并配置好静态IP

这里，我们使用VMware14虚拟机软件来创建多个虚拟服务器。

以下是网上找的几个激活码：

```
1、CG54H-D8D0H-H8DHY-C6X7X-N2KG6
2、ZC3WK-AFXEK-488JP-A7MQX-XL8YF
3、AC5XK-0ZD4H-088HP-9NQZV-ZG2R4
4、ZC5XK-A6E0M-080XQ-04ZZG-YF08D
5、ZY5H0-D3Y8K-M89EZ-AYPEG-MYUA8
```

然后centos7我们安装的是最新的最小化版本。

下载链接：[http://mirrors.163.com/centos/7/isos/x86\_64/CentOS-7-x86\_64-Minimal-1804.iso](http://mirrors.163.com/centos/7/isos/x86_64/CentOS-7-x86_64-Minimal-1804.iso)

安装教程：[https://blog.csdn.net/guo\_ridgepole/article/details/78973763](https://blog.csdn.net/guo_ridgepole/article/details/78973763)

---

不过这里要注意的是，部分机子装不上64位系统原因如下：

1、本机系统是32位的，所以装不了64位的虚拟机系统；

2、主机的bios没有开虚拟化技术，intel的vt-d,或者vt-x，amd的amd-v等，不同主板的对应位置不同；

3、开启了虚拟化之后，没有关闭Hyper-V的功能；

关闭方式：右键开始菜单→程序与功能→启用或关闭Windows功能（左边菜单列表），然后会弹出一个小窗口，在里面找到Hyper-V,把前面的勾去掉就可以了，这里是win10的关闭方式，其余系统请自行寻找或百度~~

---

另外，装完系统之后，我们需要配置一下虚拟机的静态IP，步骤如下：

进入centos，登录账户后，首先我们编辑ip配置文件，vi /etc/sysconfig/network-scripts/ifcfg-ens33，这里的ifcfg-ens33文件可能都不一样，我这机子默认就是这个，各自看情况编辑吧~~，要修改的内容如下：

```
BOOTPROTO=dchp  修改为  BOOTPROTO=static
ONBOOT=no       修改为  ONBOOT=yes

新增内容
IPADDR=192.168.30.21        这里是虚拟机的ip，最后一位可自定义，不重复即可，前面三字段需根据虚拟机配置而定
GATEWAY=192.168.30.2        这不能修改，根据虚拟机而定。
NETMASK=255.255.255.0       这不能修改，根据虚拟机而定。
DNS1=101.198.199.200        正常的DNS配置即可
```

![](/assets/centos.png)

![](/assets/vmware.png)

上图中，1、首先我们要把DHCP服务将IP分配给虚拟机一项前面的勾去掉，

2、子网掩码就是上面说的ifcfg-ens33文件中要新增的NETMASK的值；

3、点进去右边NAT设置，进入下图，该网关IP就是要新增的GATEWAY的值。

![](/assets/vmware1.png)

最后，保存修改之后，重启服务：`service network restart`

此时，可以尝试一下ping百度等外网，是可以ping通，在本地的cmd中ping虚拟机的的ip，也是可以ping通的~

