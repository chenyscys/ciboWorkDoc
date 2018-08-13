# 解决gitbook保存推送后，服务器不更新的问题

        前段时间，我们的PHP人生导师问我，为啥gitbook推送了之后没反应，安排了个作业叫我去搞搞，我一直拖到了今天，准备写关于小程序文章的时候才想起来，顺便弄了一下。

        首先，我打开29服务器，进入gitbook文件夹，命令如下：

* `cd /app/gitbook/ciboWorkDoc`

接着我们直接用`git  pull`命令更新一下看看，果然，是有文件冲突了。

![](/assets/QQ图片20180813175124.png)

如上图，是 _`SUMMARY.md` _目录文件跟连接SQL Server文章的`lian-jiesql-server.md`文件冲突了

解决方法也很简单，直接删除，用rm命令删除了这两个文件，然后再用 `git pull` 命令更新一下，再执行一下gitbook文件夹下面的build.sh命令文件就可以了，即 `sh build.sh`



