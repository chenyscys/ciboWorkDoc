鉴于一个自制的select下拉列表出场率多达五百次（夸张手法），而且调用的都是同一个接口，所以今天决定把它抽成组件。

就是下面这个家伙。这个家伙点击右边箭头或者输入框，可以显示所有专柜；要是在输入框输入的话，又可以联动查询，所以还是比较有魅力的。

![](/assets/form.png)

在抽组件的过程中，父子组件传值方面总是容易忘记，所以记录下来日后好翻阅，也可以供大家参考。

下面我就以这个组件为例子进行说明。vsForm.vue为父组件，downBlock.vue为子组件。

**父组件通过 props 向下传递数据给子组件，子组件通过 events 给父组件发送消息。如下图所示：**

![](/assets/mind.png)

**1.父组件向子组件传值之props**



父组件

![](/assets/parent.png)![](/assets/parent2.png)

&lt;downBlock @choose="getData" @key="keyClick" :signUp="isSignUp" :shoppeName="shoppe"&gt;&lt;/downBlock&gt;

如代码所示，父组件可以将动态绑定（v-bind）的数据，或者静态的数据传给子组件。



子组件

![](/assets/child.png)![](/assets/child2.png)（放大代码块的图）

子组件通过props获取父组件传过来的值。



**2.子组件向父组件传值之$emit**

**vm.$emit\( event,\[ arg\] \) ** ，子组件使用 $emit 触发父组件的自定义事件，event为事件名称（String），arg为可选参数，可传可不传。

子组件![](/assets/child3.png)

![](/assets/child4.png)

子组件通过click触发自己的chooseId方法，并将自己数据存储为shopData对象传给父组件。



父组件![](/assets/parent3.png)![](/assets/parent4.png)



