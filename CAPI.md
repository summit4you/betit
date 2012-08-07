betit
=====
版本：0.1  
作者：[丘文峰](mailto:809104518@qq.com)

本文档用于描述BetIt的客户端接口
******************************
索引
----
* 下行接口
	*	[好友动态列表接口](#全站动态列表接口)
	*	[全部打赌列表接口]
	*	[通知列表接口]
	*	[私信列表接口]
	*	[私信详情]
	*	[好友排行榜接口]
	*	[热门打赌排行榜接口]
	*	[我的个人信息]
	*	[打赌详情]
	*	[评论列表]
	*	[搜索打赌]
	*	[搜索好友]
	*	[推荐打赌列表]

* 上行接口
	*	[注册]
	*	[登录]
	*	[发布打赌]
	*	[参与打赌]
	*	[撰写评论]
	*	[发布私信]
	*	[更改头像]
	*	[更改昵称]
	*	[编写心情]

接口说明
--------
<h2 id="friendfeed">全站动态列表接口</h2>
/capi/space.php?do=feed&uid=1&start=0&feedmaxnum=10
#### 请求参数
	* 当前用户id -- uid
	* 第几页 -- start
	* 每页显示数量  -- feedmaxnum
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[feeds]，feed列表， 条目字段如下
			* feedid -- feed的id值
			* appid -- 当icon为quiz时代表参与打赌
			* title_template -- feed的标题
			* body_template -- feed的内容
			* dateline -- feed的时间
			* uid -- 发布feed的用户id
			* username -- 发布feed用户
			* image_1_link -- 打赌A图片
			* image_2_link -- 打赌B图片
			* idtype -- feed类型
				* quizid -- 打赌
				* doid -- 心情
				* picid -- 图片
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{"code":0,"data":{"feeds":{"38527753d7ee50e50c95d6427110b925":{"feedid":"83","appid":"1","icon":"quiz","uid":"5","username":"summit","dateline":"08-06 07:11",
	"friend":"0","hash_template":"d054367a46e659022b40f4334dec2c56","hash_data":"38527753d7ee50e50c95d6427110b925",
	"title_template":"summit 公布了打赌 <a target=\"_blank\"   href=\"space.php?uid=5&do=quiz&id=54\"  target=\"_blank\">测试优惠券<\/a>的答案，答案是3",
	"title_data":{"url":"space.php?uid=5&do=quiz&id=54","subject":"测试优惠券","key":"3"},"body_template":"<br>参与人数1人,很不幸本期没有人获胜，大家要加油哟！",
	"body_data":{"attend":"1"},"body_general":"","image_1":"","image_1_link":"","image_2":"","image_2_link":"","image_3":"","image_3_link":"","image_4":"",
	"image_4_link":"","target_ids":"","id":"0","idtype":"","hot":"0","magic_class":"","icon_image":"image\/icon\/quiz.gif","target":" target=\"_blank\"",
	"style":" onclick=\"readfeed(this, 83);\"","thisapp":1},"c6a4a0d241035ff650c7d2f841f387c8":{"feedid":"82","appid":"1","icon":"quiz","uid":"5","username":"summit",
	"dateline":"08-06 07:10","friend":"0","hash_template":"d6269a47b34e39569585a1d028651f60","hash_data":"c6a4a0d241035ff650c7d2f841f387c8",
	"title_template":"summit 发表了新打赌","title_data":[],"body_template":"<b><a target=\"_blank\"   href=\"space.php?uid=5&do=quiz&id=54\" >测试优惠券<\/a><\/b><br>
	<br>12:2人投注<br>3:1人投注<br\/>奖池：60金币","body_data":{"subject":"<a href=\"space.php?uid=5&do=quiz&id=54\">测试优惠券<\/a>",
	"option":"<br>12:2人投注<br>3:1人投注","totalcost":"<br\/>奖池：60金币"},"body_general":"","image_1":"","image_1_link":"","image_2":"","image_2_link":"",
	"image_3":"","image_3_link":"","image_4":"","image_4_link":"","target_ids":"","id":"54","idtype":"quizid","hot":"0","magic_class":"","icon_image":"image\/icon\/quiz.gif","target":" target=\"_blank\"","style":"","thisapp":1}},"count":2},
	"msg":"数据获取成功","action":"rest_success"}