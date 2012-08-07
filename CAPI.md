betit
=====
版本：0.1  
作者：[丘文峰](mailto:809104518@qq.com)

本文档用于描述BetIt的客户端接口
******************************
索引
----
* 下行接口
	*	[好友动态列表接口](#好友动态列表接口)
	*	[全部打赌列表接口](#全站动态列表接口)
	*	[通知列表接口](#通知列表接口)
	*	[私信列表接口](#私信列表接口)
	*	[私信详情](#私信详情)
	*	[好友排行榜接口](#好友排行榜接口)
	*	[热门打赌排行榜接口]
	*	[我的个人信息]
	*	[打赌详情]
	*	[评论列表]
	*	[搜索打赌]
	*	[搜索好友]
	*	[推荐打赌列表]

* 上行接口
	*	[注册]
	*	[登录](#登录)
	*	[发布打赌]
	*	[参与打赌]
	*	[撰写评论]
	*	[发布私信]
	*	[更改头像]
	*	[更改昵称]
	*	[编写心情]

接口说明
--------

<h2>好友动态列表接口</h2>
/capi/space.php?do=feed&uid=1&start=0&perpage=10&view=we&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0
#### 请求参数
	* 当前用户id -- uid
	* 第几页 -- start
	* 每页显示数量  -- perpage
	* 查询参数 -- view, 值为we代表好友动态列表
	* API密钥 -- m_auth, 由登录后返回
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

<h2>全站动态列表接口</h2>
/capi/space.php?do=feed&uid=1&start=0&perpage=10&view=all&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0
#### 请求参数
	* 当前用户id -- uid
	* 第几页 -- start
	* 每页显示数量  -- perpage
	* 查询参数 -- view, 值为all代表全站动态列表
	* API密钥 -- m_auth, 由登录后返回
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

<h2>通知列表接口</h2>
/capi/space.php?do=notice&start=0&prepage=2&uid=1&type=quizinvalid&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0
#### 请求参数
	* 当前用户id -- uid
	* 第几页 -- start
	* 每页显示数量  -- perpage
	* 通知类型 -- type
		* quiz -- 打赌
		* quizcomment -- 打赌评论
		* quizinvite -- 打赌邀请
		* clickquiz -- 打赌表态
		* quizwin -- 打赌赢
		* quizlost -- 打赌输
		* quizinvalid -- 打赌流失
		* credit -- 金币
		* 空 -- 代表全部通知
	* API密钥 -- m_auth, 由登录后返回
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[notices]，通知列表， 条目字段如下
			* id -- 通知id
			* uid -- 接收通知的用户
			* type -- 通知类型（取值含义见请求参数）
			* authorid -- 发送通知的用户
			* authorid -- 发送通知的用户
			* note -- 通知的内容
			* isfriend -- 接收和发送方是否好友
			* dateline -- 时间
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{"code":0,"data":{"notice":[{"id":"124","uid":"5","type":"quizwin","new":"0","authorid":"5","author":"summit","note":"恭喜你在 
	<a href=\"space.php?uid=5&do=quiz&id=53\" target=\"_blank\">《234444444444444444》<\/a>的悬赏打赌中得胜，获得金币20。","dateline":"1344236803","isfriend":1,
	"style":""},{"id":"122","uid":"5","type":"quizlost","new":"0","authorid":"5","author":"summit","note":"很不幸你在 <a href=\"space.php?uid=5&do=quiz&id=52\" 
	target=\"_blank\">《测试优惠券》<\/a>的悬赏打赌中没有获胜，输了打赌20，请继续努力o~下次得奖的就是你！","dateline":"1344236757","isfriend":1,"style":""},
	{"id":"120","uid":"5","type":"quizwin","new":"0","authorid":"5","author":"summit","note":"恭喜你在 <a href=\"space.php?uid=5&do=quiz&id=51\" target=\"_blank\">
	《34》<\/a>的悬赏打赌中得胜，获得金币20。","dateline":"1344236043","isfriend":1,"style":""},{"id":"118","uid":"5","type":"quizwin","new":"0","authorid":"5",
	"author":"summit","note":"恭喜你在 <a href=\"space.php?uid=5&do=quiz&id=50\" target=\"_blank\">《123》<\/a>的悬赏打赌中得胜，获得金币20。","dateline":"1344235975",
	"isfriend":1,"style":""},{"id":"116","uid":"5","type":"quizwin","new":"0","authorid":"5","author":"summit",
	"note":"恭喜你在 <a href=\"space.php?uid=5&do=quiz&id=49\" target=\"_blank\">《测试优惠券》<\/a>的悬赏打赌中得胜，获得金币40。","dateline":"1344235733","isfriend":1,
	"style":""}],"count":5},"msg":"数据获取成功","action":"rest_success"}

<h2>私信列表接口</h2>
capi/space.php?do=pm&start=0&prepage=2&uid=1&filter=newpm&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0
#### 请求参数
	* 当前用户id -- uid
	* 第几页 -- start
	* 每页显示数量  -- perpage
	* 私信类型 -- filter
		* newpm -- 未读私信
		* privatepm -- 私人消息
		* systempm -- 系统消息
		* announcepm -- 公共消息
		* 空 -- 私人消息
	* API密钥 -- m_auth, 由登录后返回
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[pms]，私信列表， 条目字段如下
			* pmid -- 私信id
			* msgfrom -- 消息发送人
			* msgfromid -- 消息发送人id
			* msgtoid -- 消息接收人id
			* authorid -- 发送通知的用户
			* new -- 是否未读
			* subject -- 私信标题
			* message -- 私信内容
			* delstatus -- 删除状态
			* fromappid -- 应用程序ID，可以忽略
			* dateline -- 时间
			* daterange -- 消息相隔的天数，1代表1天内，2代表两天内，3代表3天内
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{"code":0,"data":{"pms":[{"pmid":"7","msgfrom":"admin","msgfromid":"1","msgtoid":"5","new":"1","subject":"你好summit","dateline":"08-07 07:33","message":"你好summit",
	"delstatus":"0","related":"0","fromappid":"1","daterange":1,"touid":"1"}],"count":1},"msg":"数据获取成功","action":"rest_success"}

<h2>私信详情</h2>
capi/space.php?do=pm&subop=view&pmid=2&touid=12&daterange=10&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0
#### 请求参数
	* 消息送至的用户id -- touid
	* 检索消息的区间（几天之内的） -- daterange
	* 消息id -- pmid
	* 操作参数 -- subop, 必须为view
	* API密钥 -- m_auth, 由登录后返回

#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[pms]，私信列表， 条目字段如下
			* pmid -- 私信id
			* msgfrom -- 消息发送人
			* msgfromid -- 消息发送人id
			* msgtoid -- 消息接收人id
			* authorid -- 发送通知的用户
			* new -- 是否未读
			* subject -- 私信标题
			* message -- 私信内容
			* delstatus -- 删除状态
			* fromappid -- 应用程序ID，可以忽略
			* dateline -- 时间
			* daterange -- 消息相隔的天数，1代表1天内，2代表两天内，3代表3天内
		* data[count], 返回列表条目数, 便用遍历

#### 样例
	{"code":0,"data":{"pms":[{"pmid":"3","msgfrom":"aifaxian","msgfromid":"1","msgtoid":"12","folder":"inbox","new":"1","subject":"你好啊","dateline":"03-09 18:04",
	"message":"你好啊","delstatus":"0","related":"1","fromappid":"1","daterange":5}],"count":1},"msg":"数据获取成功","action":"rest_success"}

<h2>好友排行榜接口</h2>
capi/space.php?uid=5&do=friend&m_auth=54f8qnt8HxbRz8NWomy0e4k2gKvVvc6oil8qDY9upUERswmzj
#### 请求参数
	* 当前用户id -- uid
	* API密钥 -- m_auth, 由登录后返回

#### 返回字段
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[friends]，好友列表， 条目字段如下(类似于[登录](#登录)返回的空间信息
			* groupid -- 所在用户组（级别）
			* credit -- 金币
			* experience -- 经验
			* username -- 用户名
			* name -- 实名
			* namestatus -- 是否实名
			* videostatus -- 是否视频认证
			* friendnum -- 好友数
			* viewnum -- 浏览次数
			* notenum -- 通知数
			* addfriendnum -- 关注数
			* doingnum -- 心情数
			* lastpost -- 最新提交时间
			* lastlogin -- 最新登录时间
			* attachsize -- 空间大小
			* flag -- 是否被禁
			* newpm -- 是否有新通知
			* avatar -- 个人头像
			* quiznum -- 发布的打赌数
			* winnum -- 赢的次数
			* lostnum -- 输的次数
			* voternum -- 参加打赌的次数
		* data[count], 返回列表条目数, 便用遍历

#### 样例
	{"code":0,"data":{"friends":{"7":{"uid":"7","groupid":"11","credit":"1800","experience":"2000","username":"test2","name":"","namestatus":"0","videostatus":"0",
	"domain":"","friendnum":"1","viewnum":"4","notenum":"6","addfriendnum":"0","mtaginvitenum":"0","eventinvitenum":"0","myinvitenum":"0","pokenum":"0",
	"doingnum":"0","blognum":"0","albumnum":"0","threadnum":"0","pollnum":"0","eventnum":"0","sharenum":"0","dateline":"1343973929","updatetime":"1343974426",
	"lastsearch":"0","lastpost":"1343974426","lastlogin":"1343974880","lastsend":"0","attachsize":"0","addsize":"0","addfriend":"0","flag":"0","newpm":"0",
	"avatar":"0","regip":"127.0.0.1","ip":"127000000","mood":"0","quiznum":"1","winnum":"0","lostnum":"0","voternum":"1","resideprovince":"","residecity":"",
	"note":"","spacenote":"","sex":"0","gid":"0","num":"6","p":"","c":"","group":"其他","isfriend":1}},"count":1},"msg":"数据获取成功","action":"rest_success"}

<h2>登录</h2>
capi/do.php?ac=login&username=summit&password=likeyou&loginsubmit=true
#### 请求参数
	* 用户名 -- username
	* 密码 -- password
	* 提交类型 -- loginsubmit， 必须为true
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户
	* 用户空间信息 -- space
		* groupid -- 所在用户组（级别）
		* credit -- 金币
		* experience -- 经验
		* username -- 用户名
		* name -- 实名
		* namestatus -- 是否实名
		* videostatus -- 是否视频认证
		* friendnum -- 好友数
		* viewnum -- 浏览次数
		* notenum -- 通知数
		* addfriendnum -- 关注数
		* doingnum -- 心情数
		* lastpost -- 最新提交时间
		* lastlogin -- 最新登录时间
		* attachsize -- 空间大小
		* flag -- 是否被禁
		* newpm -- 是否有新通知
		* avatar -- 个人头像
		* quiznum -- 发布的打赌数
		* winnum -- 赢的次数
		* lostnum -- 输的次数
		* voternum -- 参加打赌的次数
#### 样例
	{"code":{"space":{"uid":"1","groupid":"11","credit":"2030","experience":"2030","username":"admin","name":"","namestatus":"0","videostatus":"0","domain":"",
	"friendnum":"0","viewnum":"3","notenum":"0","addfriendnum":"0","doingnum":"0",
	"blognum":"3","albumnum":"0","threadnum":"0","pollnum":"0","eventnum":"0","sharenum":"0","dateline":"1343725030","updatetime":"1343966557","lastsearch":"0",
	"lastpost":"1344324792","lastlogin":"1344328793","attachsize":"774822","addsize":"0","addfriend":"0","flag":"0","newpm":"0","avatar":"0",
	"mood":"0","quiznum":"27","winnum":"2","lostnum":"0","voternum":"10"},
	"m_auth":"55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0"},"data":[],
	"msg":"登录成功了，现在引导您进入登录前页面 \\1","action":"login_success"}