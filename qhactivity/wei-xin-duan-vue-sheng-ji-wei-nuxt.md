原本为了更好地体验与开发，我把邦客珠海的微信端，从vue框架，迁移到vue的一个进阶框架，NUXT，然并卵，很可能微信项目自此夭折，不过迁移也迁移完了，下面是新项目的介绍以及开发规范与注意点：

1、svn地址：svn://192.168.3.29/svn/cibo\_nuxt

2、技术栈： vant + nuxt （包含：vue + vuex + axios）+ less

3、nuxt 文档：[https://zh.nuxtjs.org/](https://zh.nuxtjs.org/)

vant 文档：[https://youzan.github.io/vant/\#/zh-CN/intro](https://youzan.github.io/vant/#/zh-CN/intro)

4、目录结构：

![](/assets/nuxt.png)

**.nuxt **是运行目录，**node\_modules** 是依赖目录， **dist、nuxt **是构建打包目录，这几个开发时都可以不理会。

主要开发的文件是 **client **文件夹以及 **nuxt.config.js** 项目配置文件。

**client **包含了项目所有页面，样式，脚本，媒体资源等等。

![](/assets/client.png)

**assets** 是资源目录，里面主要包含的是全局的样式文件以及图标；

**components **是存放共用组件目录，跟vue类似；

**layouts **是存放页面框架组件，主要用于定义页面组件的外框架；（必不可少，至少要有一个**default.vue**的组件在里面）

**middleware** 是中间件脚本，用于跳转特定路由前的检测工作。

**pages **是页面组件，与vue类似；

**plugins** 是插件库，用于使用自己的库或者第三方模块。

**static **存放静态资源，如视频，音乐，大型图片等。调用路径：‘/nuxt/xxx.xxx’，这里nuxt是可配置的。

**store **是VUEX的实现，不过它是通过模块化的方式来实现，要注意书写方式。

**tools **是工具函数库，其实与plugins类似，可合并到plugins里。

5、nuxt.config.js 配置文件

这个配置文件，是整个nuxt项目的关键，可以配置全局变量，全局中间件，全局插件，全局样式，访问ip，端口，统一的头部信息，

全局loading效果，静态化之后的文件夹名，babel配置等等。

具体配置请看文件注释以及官方文档。

6、关于样式：

**common.less**：全局通用样式写在这；

**theme.less** ：这个是关于的vant UI框架的主题定制，有需要改vant 全局样式请到这里修改；

**variable.less**： 这是全局的css变量，设定全局css变量，请到这里设定。



7、如何使用？

* svn checkout 项目到本地，cmd到对应目录，执行npm install； **PS：要注意NPM要在5.2.0以上，最好升级到最新的稳定版node与npm；**
* npm install 完了之后，运行 npm run dev就可以跑起来了。



8、如何部署：

进入到对应目录，执行 npm run generate，然后把对应的文件夹 nuxt 放到 laravel 项目下的**public**文件夹下，即可。



9、关于路由，由于项目会执行静态化，因此，之前nuxt文档中的动态路由，我们是用不了的，那个需要用node的服务器。

因此，我折中，通过用query，即url参数来实现，具体可参考，pages/store里面的goods跟shop页面组件。







