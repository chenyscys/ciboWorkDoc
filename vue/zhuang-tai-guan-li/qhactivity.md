qhActivity状态组件，是用来记录活动数据的，对应关系如下：

```
qhActivity:{
    activity:{                //活动信息
        uniqid:'',            //活动ID
        name:'',            //活动名称
        start_at:'',            //活动开始时间
        end_at:'',            //活动结束时间
        share_config:{            //活动分享信息
            share_title:'',        //活动分享标题
            share_desc:'',        //活动分享描述
            share_linkurl:'',    //活动分享链接
            share_image:''        //活动分享图片
        }
    },
    assist_id:'',                //用户发起助力ID
    helpAssistId:'',            //助力ID
    canAssist:false,            //是否可以给这个助力ID助力
    join_num:0                //活动参与人数
}
```



