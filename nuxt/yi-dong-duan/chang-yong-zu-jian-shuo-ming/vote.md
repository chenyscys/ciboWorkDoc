### 点赞、助力组件

* #### 组件功能实现

点赞：   判断是否有点赞资格，判断点赞数是否超过100，超过100则需要填写验证码，若验证成功则投票，并显示投票结果，投票成功，并在显示的点赞数上加1。

助力：   判断是否有助力资格，判断助力数是否超过100，超过100则需要填写验证码，若验证成功则投票，并显示投票结果，投票成功，并在显示的助力数上加1，并伴随已助力信息。

* #### 组件位置

~/components/vote

* #### 组件使用

点赞父组件引用：

`//OtherAspag被点赞的对象，OtherAspag.like_num为当前点赞数，点赞type为‘good’`

`<template>`

`<div>`

`<i @click="gotoVote('good',OtherAspag)" >点赞</i>`

`<vote ref="vote" :goodchange.sync="OtherAspag.like_num" ></vote>`

`</div>`

`</template>`

`<script>`

`import vote from "~/components/vote";`

`export default {`

`components: {vote },`

`data(){`

`return{`

```
               OtherAspag:null，

               goodchange:0

      }
```

`},`

`methods: {`

`gotoVote(type,item){`

`this.$refs.vote.toVote(type,item);`

`}`

`}`

`}`

`</script>`

助力swipeCard组件引用：

`//cardData被助力的对象，cardData.like为当前助力数，cardData.my_num为是否已为该用户助力，助力type为‘help’`

`<template>`

`<div>`

`<div class="head-r flex" @click="vote('help',cardData)">`

`<van-icon name="like" size="18"  :color="cardData.my_num > 0 ? '#ff006c':'#ddd'"/>{{cardData.like}}`

`</div>`

```
   <vote ref="vote" :helpchange.sync="cardData"></vote>;

</div>
```

`</template>`

`<script>`

`import vote from "~/components/vote";`

`export default {`

`components: {vote },`

`data(){`

`return{`

```
        helpchange:{}

     }
```

`},`

`props: {`

`cardData: {`

`type: Object,`

`default: {}`

`}`

`},`

`methods: {`

`vote(type,item){`

`this.$refs.vote.toVote(type,item);`

`}`

`}`

`}`

`</script>`

#### 



