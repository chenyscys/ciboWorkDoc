#### 一、文件目录结构

根据小程序的开发文档，结合我们的实际情况，我们将采用分包模式的来进行开发，更好的解耦协作；

因此，这对于我们的文件目录结构有了一定要求，毕竟分包，就是为了避免用户一次性的加载小程序过大；

所以我们要避免文件重复的问题以及非必要情况下加载其他分包文件的情况。

官方分包加载的传送门：[https://developers.weixin.qq.com/miniprogram/dev/framework/subpackages.html](https://developers.weixin.qq.com/miniprogram/dev/framework/subpackages.html)![](/assets/{$V]TLBP]3F8S]563QOXHLQ.png)上图，便是文档中所写的打包跟引用原则，再结合分包的概念，大概定义一下我们的小程序的目录结构。

PS：xxx4件套 =  xxx.wxml + xxx.js + xxx.json + xxx.wxss;

```catalog
├── app.js                    小程序注册，入口文件
│            
├── app.json                  全局配置，包括路由路径定义，窗口表现，网络超时，底部tab等
│
├── config.js                 配置文件，主要是配置一些接口域名，跳转路径等
│
├── project.config.json       项目配置文件，创建项目时自动生成，也可导入
│
│── resource                  整个项目以及主包的资源文件，主要包括图片，公用js文件等
│
│── wxss                      整个项目以及主包的公用样式文件
│
│── wxs                       整个项目以及主包的公用wxs脚本文件
│
│── component                 整个项目以及主包的公用组件文件
│
│── template                  整个项目以及主包的公用模版文件
│
│── page                      整个项目的所有的页面文件，包括分包，主包等
│   │
│   └── main                  小程序主包
│       └── index（4件套）     主包首页
│       └── list              list页面的文件夹（里面包含四件套）
│   │
│   └── example               小程序分包
│       └── index（4件套）     分包首页
│       └── pages             其他页面的文件夹
|            └── list          list页面的文件夹（里面包含四件套）
│       └── wxss              分包专用的共享wxss
│       └── component         分包专用的共享component
│       └── template          分包专用的共享template
│       └── wxs               分包专用的共享wxs    
│       └── resource          分包专用的共享resource
│   │
│   └── example2              小程序分包2
│       └── index（4件套）     分包首页
│       └── pages             其他页面的文件夹
|            └── list          list页面的文件夹（里面包含四件套）
│       └── wxss              分包专用的共享wxss
│       └── component         分包专用的共享component
│       └── template          分包专用的共享template
│       └── wxs               分包专用的共享wxs    
│       └── resource          分包专用的共享resource
```



