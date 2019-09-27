### 图片压缩、旋转、上传组件

* #### 组件实现的功能

组件实现了图片读取，判断是否大于2M，若大于2M对图片进行压缩，若有传入旋转角度，对图片以中心为轴心进行旋转相应度数，然后上传。

* #### 组件位置

~/components/activity/20190922/upCompressImg

* #### 组件使用

##### 父组件引用：

> `<template>`
>
> `<upCompressImg :goods="goods"></upCompressImg>`
>
> `</template>`
>
> `<script>`
>
> `import upCompressImg from "~/components/activity/20190922/upCompressImg";`
>
> `export default {`
>
> `components: { upCompressImg },`
>
> `data() {`
>
> ```
> return {
>
>   goods={}
> ```

> `}`
>
> `}`
>
> `}`
>
> `</script>`

* #### 使用效果

#### 

* #### 实现原理

#### 



