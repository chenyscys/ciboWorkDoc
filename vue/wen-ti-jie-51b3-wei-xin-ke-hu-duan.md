代码写多了，坑也多，有时候还自己挖坑自己跳，这次写这一篇文章 ，单纯是记录一下可能日常遇到的一些问题，可能对于大神来说，切，湿湿碎啦，这么简单还需要记吗？没事，先记下来，日后好相查。

一. 微信音乐播放问题解决:

1、写页面引入本地的音乐，本地播放正常，上传了服务器，在微信打开测试发现音乐不能正常播放，首先先改引入音乐的路径：

src=“/dist/static/music.mp3”   备：这个dist是vue打包自动生成出dist，里面是整个项目的资源

2、

```
let that = this;
that.$refs.audio.play();
this.$wechat.ready(function () {
     that.$refs.audio.play();
});


	
```

备: 以前是wx.ready    来使音乐播放, 现在变成  this.$wechat.ready  来播放音乐

这样引用 , 可能本地会报错, 不用管 , 只管上传到服务器测试就好了

