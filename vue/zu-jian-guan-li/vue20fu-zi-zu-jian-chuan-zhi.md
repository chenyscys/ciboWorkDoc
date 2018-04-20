鉴于一个自制的select下拉列表出场率多达五百次（夸张手法），而且调用的都是同一个接口，万年不变（也是夸张手法），所以今天决定把它抽成组件。

就是下面这个家伙。这个家伙点击右边箭头或者输入框，可以显示所有专柜；要是在输入框输入的话，又可以联动查询，所以还是比较有魅力的。

![](/assets/form.png)

在抽组件的过程中，vue父子组件传值方面总是容易忘记，所以记录下来日后好翻阅，也可以供大家参考。

下面我就以这个组件为例子进行说明。vsForm.vue为父组件，downBlock.vue为子组件。

**父组件通过 props 向下传递数据给子组件，子组件通过 $emit 给父组件发送消息。如下图所示：**

![](/assets/mind.png)

**1.父组件向子组件传值之props**

父组件![](/assets/parent.png)![](/assets/parent2.png)

`<downBlock @choose="getData" @key="keyClick" :signUp="isSignUp" :shoppeName="shoppe"></downBlock>`

如代码所示，父组件可以将动态绑定（v-bind）的数据，或者静态的数据传给子组件。



子组件![](/assets/child.png)

```
props:{
   signUp: { 

      type: Boolean,

      default: false

    },

    shoppeName: {

      type: String,

      default: ''
    }
}
```

子组件通过props获取父组件传过来的值。





**2.子组件向父组件传值之$emit**

**vm.$emit\( event,\[ arg\] \) ** ，子组件使用 $emit 触发父组件的自定义事件，event为事件名称（String），arg为可选参数，可传可不传。

子组件![](/assets/child3.png)

![](/assets/child4.png)

子组件通过click触发自己的chooseId方法，通过`this.$emit('choose', shopData)` 触发父组件的自定义事件'choose'，并将自己的数据存储为shopData对象传给父组件（如果只有一个值就直接传，多个值就用对象传）。



父组件![](/assets/parent3.png)![](/assets/parent4.png)父组件的通过触发自定义事件choose，调用了自己的getData方法，并将子组件传过来的值赋给自己的data。



3.父组件只能通过触发事件获得子组件的值，若想直接获取，可以通过v-ref绑定子组件对象，然后在父组件中直接this.$refs.XX访问（这个方法还没有亲测，有需要的小伙伴可以试一下）。

