## 如何在centos上搭建自动化部署gitbook？

最近在村长的带领下，准备在测试服务器上搭建了一个gitbook来让大伙发布在敲码中遇到的bug处理方法以及一些程序的搭建过程，于是呢，我就风风火火的去搞了起来，折腾了几天，终于把这玩意给搞起来了。

首先，安装gitbook这个就很简单了，只要服务器上有npm环境，那就只要简单的`npm install -g gitbook-cli`就可以安装成功了。

不过有时候可能会遇到找不到命令的情况，那这时候注意一下安装成功时指定的路径，然后创建一个软链接，把路径指引到`/usr/local/bin/gitbook` 或者 `/usr/bin/gitbook` 就可以运行gitbook命令了。

网上很多文章都说要`gitbook -v`出来版本号，不过我是打不出来，用`gitbook --version`这个命令才能出来版本号，也不知道是为何~~

接下来，就是新建一个文件夹，然后开始简单的gitbook几个命令的瞎玩：

* `gitbook init` ——环境注入，搭建，一个新的gitbook的开始；
* `gitbook serve` ——跑起你的gitbook，可以看到你当前的gitbook效果；
* `gitbook build`  ——打包gitbook，默认html模式，开放个端口或者域名指向打包好的文件夹就可以访问啦

---

好了，gitbook的简单介绍就到这，本文的主要内容并不是这些哈，关于gitbook的搭建，网上教程很多，大家可以去搜搜，我还是来说说我是如何把这玩意搞成自动化部署的！

#### 自动化部署的目的

要达到的目的就是在Gitbook Editor上编辑后，保存推送到git上，实现服务器自动拉取git服务器的最新内容并进行打包，这样就不用每次修改增添内容的时候都要ssh连上服务器去更新以及打包了，省时省力~~PS：有更多的时间刷刷新闻了嘿嘿

#### 如何做

一开始，我了解到git上有个钩子的方法，通过git的hooks里面的post-receive好像是可以实现，不过再尝试了几次，以及看了几篇文章之后，我发现，一点屁用都没有！！！当然这里面可能是我git水平不够，或者环境，权限没弄好，导致的，请恕在下无能！

后面我就采用了github的webhook来实现，接下来，就让我们来看看github的神奇魔法吧！

1. 首先，我们要在github上建个仓库，拿到仓库地址后，然后就到服务器上clone一下，还有到Gitbook Editor配置一下（Editor这里最后再说说怎么配置）；
2. ![](/assets/import.png) Gitbook Editor 在我们每次编辑之后就会有个save按钮，save之后右边那个就是上传到github仓库上，也就是git push。PS：这编辑器也是够简单粗暴的，不过我喜欢~~

3. 接下来我们要去github上面的项目配置一下**webhooks**了，首先打开github项目网址，然后去项目的setting设置里，  
   ![](/assets/githubSetting.png)在这里新建一个webhook，填上一个网址。而当push完项目时，github就会去POST这个网址，并且传上一系列参数，这里可选表单模式与json模式，看个人喜欢选择咯！`ssh-keygen -t rsa -C "your_email@youremail.com"`

4. 这里还有很关键的一步，我们需要去服务器生成ssh密钥，这个是用来授权使用的。  
   生成命令：`ssh-keygen -t rsa -C "your_email@youremail.com"`  
   至于配置的话，就在github的个人设置里，这里我配置了两次，一个是用邮箱账户生成，一个使用nginx用户生成（就是把后面的邮箱地址改成运行用户的名字：nginx），原因是因为一开始的授权不成功，后面设置多一个nginx的就可以了，不知道是不是因为运行用户的问题，这个大伙有遇到的话不妨可以尝试一下。![](/assets/miyue.png)

#### 到这为止，都没什么问题，也比较简单，但接下来就是关键了~~~

由于我们是用php开发的，所以我就写了一个php文件来接收这个POST，然后用system函数/shell\_exec函数来执行外部环境的命令，也就是在linux下的命令，这里的坑就大了。

1. 一般情况下，我们ssh连上去都是root账户，有root权限，所以很多命令运行起来都没什么问题，毕竟天大地大ROOT最大嘛
   但是github通过post过来的时候，跟我们浏览器访问的时候是一样的，都是php的运行用户，在这里我们的php配置的运行用户叫nginx，不信？哟呵，大伙可以写个php文件，然后写上一句  `echo shell_exec('id -a') `看看显示什么哈，我们这里都是501\(nginx\)。

2. 当我们把文件写好了之后，比如第一步，尝试一下`shell_exec(cd 指定目录 && git pull)`，然后通过浏览器访问一下php文件，然后去知道目录下面ls一下，就会发现，文件更新啦，只要可行，那当我们推送到github仓库后，就会自动帮我们更新了。

3. 那接下来，就是要打包了，gitbook的打包命令，之前已经说过了，`gitbook build`这时候就尴尬了，我遇到了大坑，差点爬不出来，要么找不到命令，要么就是运行报错。
   直接运行gitbook的话就会找不到命令，这时有可能是命令的软链接有误，可以用 **ll** 命令检查一下/usr/local/bin/跟/usr/bin 中的gitbook，如果没有或者链接显示红色，如下：![](/assets/2.png)  
   那就需要重新建立软链接了。  
   假如进行了以上操作还是不行的话，那就用npm把gitbook都卸载掉吧，然后重新用`sudo npm install -g gitbook`安装，之后还是检查一下链接，接下来，你就会发现通过`sudo /usr/local/bin/gitbook --version `可以显示出版本号了。

4. 但是，在改成build的情况下你会发现，报错了= =，如下：![](/assets/impor23t.png)  
   以上用`sudo -u nginx /usr/local/bin/gitbook build `中前面的`sudo -u nginx`是为了模拟浏览器的运行用户，这样运行不了，大概率是账户权限问题，最后被折腾的没有办法了，只能去/etc/sudoers那里给nginx添加sudo权限，这样最终才解决了问题。  
   ![](/assets/import3.png)![](/assets/impo22rt.png)

以上是我在sudoers上的解决方法，这样设置了之后，通过浏览器端就可以执行更新与编译打包了。

#### 总结

以上的做法都是在现有的系统下去执行，在账户授权这里我觉得还是不够谨慎，不过在测试服务器的话问题应该不大，所以就先这样用着，之后在尝试一下从node，npm开始从头搭一次，看看还会不会有这样的权限问题，如果小伙伴们有更好的解决方法，欢迎一起探讨。

#### 附：Gitbook Editor的配置

![](/assets/imporaaat.png)打开这个配置，把仓库地址填进去即可！



