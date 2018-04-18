scrollPos状态组件，是用来记录页面滚动条的位置，一共有4个属性，分别为上下左右，这里为了能记录每个页面的滚动条位置，采用了对象方式来记录每一个值：

```
state = {
    scrollLeft:{

    },
    scrollTop:{

    },
    scrollRight:{

    },
    scrollDown:{

    }
}
```

这样，只要在想记录滚动条位置的时候，把页面作为一个属性，commit到状态里面就可以了。

```
let scrollTop= {
    crazyBase:10
};
this.$store.commit('updateScrollPos',{scrollTop:scrollTop});
```

如上，我记录的是crazyBase页面的滚动条距离顶部的距离，很简单，对吧！

**在记录的时候千万要记得加上页面名称，否则会覆盖掉别人的哦。**

