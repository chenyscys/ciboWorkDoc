### 图片压缩、旋转、上传组件

* #### 组件实现的功能

组件实现了图片读取，判断是否大于2M，若大于2M对图片进行压缩，若有传入旋转角度，对图片以中心为轴心进行旋转相应度数，然后上传。

* #### 组件位置

~/components/activity/20190922/upCompressImg

* #### 组件使用

父组件引用：

> `//goods.upimg为若有需要传入的图片的地址，angle为传入需要旋转的角度可正负，按需选择传入的参数，没有可不填`
>
> `<template>`
>
> ```
>  <upCompressImg :goods="goods" :angle="angle" ></upCompressImg>
> ```
>
> `</template>`
>
> `<script>`
>
> `import upCompressImg from "~/components/activity/20190922/upCompressImg";`
>
> `export default {`
>
> ```
> components: {upCompressImg },
>
> data() {
>
> //若goods里面upimg有相应图片地址可填入，没有则为空
>
>     return {
>
>          goods:{upimg:''},
>
>          angle:0
>
>      }
>
>  }
> ```
>
> `}`
>
> `</script>`

* #### 实现原理

压缩：读取图片，获取图片长宽，根据图片的长宽绘制canvas，按压缩比例设置清晰度，重新绘制图片，传出新绘制的图片地址

旋转：读取图片，获取图片长宽，根据图片的长宽绘制canvas，将画布canvas的原点移至旋转点，将图片中心移至旋转点，旋转画布，重新绘制图片，传出新绘制图片地址

* #### 参考文档

[https://www.cnblogs.com/007sx/p/7583202.html](https://www.cnblogs.com/007sx/p/7583202.html)

[https://www.cnblogs.com/suyuanli/p/8279244.html](https://www.cnblogs.com/suyuanli/p/8279244.html)

#### 



