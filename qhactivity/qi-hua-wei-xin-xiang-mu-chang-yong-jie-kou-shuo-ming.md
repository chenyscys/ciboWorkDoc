说明：{}里的是变量

* home/member/getInfo：

methods：**get，**desc**：获取用户信息**

* home/customEventLog/addEventLog：

methods：**post，**desc**：自定义事件记录**

* home/qhAssist/assistInit/{uniqid}：

methods：**get，**desc**：活动注册/获取活动信息**

* wechat/home/getWxConfig：

methods：**post，**desc**：获取微信配置数据**

* home/qhAssist/getAssist/{uniqid}：

methods：**get，**desc**：获取用户的活动数据**

* home/qhAssist/getAssistNum/{id}：

methods：**get，**desc**：获取某个用户的助力/点赞数。**

* home/qhAssist/getOtherAssist/{id}：

methods：**get，**desc**：获取某个用户的活动信息。**

* home/qhAssist/getAssistDetail/{uniqid}：

methods：**get，**desc**：获取用户某个活动的详细助力列表。**

* home/qhAssist/getAssistLog/{id}/{num?}：

methods：**post，**desc**：获取某个用户活动的详细助力列表。**

* home/qhAssist/getAssistLogRank/{uniqid}/{type?}/{order?}/{num?}：

methods：**post，**desc：**获取活动助力的排行榜**

* home/qhAssist/getFieldGroupRank/{uniqid}/{field}/{num?}/{order?}：

methods：**get，**desc**：根据某个活动的 json 某个字段分组排行榜。**

* home/qhAssist/getAssistJsonRank/{uniqid}/{str}/{type?}/{order?}/{num?}：

methods：**post，**desc：**获取某个活动的助力json某个字段的排行榜**

* home/qhAssist/getFormAssistLogRank/{uniqid}：

methods：**post，**desc：**获取表单活动排行榜**

* home/qhAssist/setShareStatus/{uniqid}/{id}：

methods：**get，**desc**：记录用户是否分享了这个活动，不过已无意义，因为微信没有这个方法了。**

* home/qhAssist/isAssist/{id}：

methods：**get，**desc**：可查询该ID是否可以助力**

* home/qhFormLog/addFormLog/{uniqid}：

methods：**post，**desc：**提交表单，新增表单记录**

* home/qhFormLog/updateFormLog/{uniqid}：

methods：**post，**desc：**提交表单，更新表单记录**

* home/qhFormLog/getFormDetail/{uniqid}：

methods：**get，**desc**：获取用户表单活动提交的表单数据。**

* home/qhFormLog/getFormOther/{uniqid}/{id}：

methods：**get，**desc**：获取某个用户表单活动提交的表单数据。**

* home/qhFormLog/getFormList/{uniqid}：

methods：**post，**desc：**获取表单活动报名记**

* home/qhAssist/getFieldSum/{uniqid}/{field}：

methods：**get，**desc**：获取某个活动某个json\_data字段的和**

* home/qhAssist/reduceUsedNum/{uniqid}/{num}：

methods：**post，**desc：**减去用户某个活动的机会可用数used\_num**

* home/qhAssist/getAllAssistNum/{uniqid}：

methods：**get，**desc**：获取某个用户总助力人数。**





