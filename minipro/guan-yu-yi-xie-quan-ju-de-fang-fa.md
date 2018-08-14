1、官方的网络请求方法是`wx.request()`，不过由于我们服务端接口的关系，需要做一些身份认证，因此重新做了一次封装。

首先页面先引入根目录下的一个js文件 `/resource/js/common.js`，用require方法引入，这里要注意，引入的时候要写的是相对路

径。那么方法如下：

```catalog
http({
    url: '/mp/getUserData',                //必填，请求地址，不需要加域名，域名统一在config文件配
    params:{'aaa':123,'bbb':222},          //接口参数，非必填
    header:{                               //请求头部，非必填
        'content-type': 'application/json'
    },
    method: 'POST',                        //请求方式，get，post等。
    success: function(data){               //成功回调，data为接口返回数据,非必填
        
    },
    fail: function(data){                  //错误回调，data为接口返回信息，非必填
    
    },
    complete: function(){                  //完成回调，无论成功还是失败的回调方法，必填
    
    }
})
```

如果要调用我们服务器以外的接口，那么请用原生方法wx.request\(\);

