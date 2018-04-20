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

如代码所示，父组件通过v-i

























