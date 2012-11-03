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
	*	[热门打赌排行榜接口](#热门打赌排行榜接口)
	*	[我的个人信息](#我的个人信息)
	*	[打赌详情](#打赌详情)
	*	[获取投注好友](#获取投注好友)
	*	[评论列表](#评论列表)
	*	[搜索打赌](#搜索打赌)
	*	[搜索好友](#搜索好友)
	*	[推荐打赌列表](#推荐打赌列表)
	*   [我发起的打赌](#我发起的打赌)
	*   [我参与的打赌](#我参与的打赌)
	*   [已揭晓的打赌](#已揭晓的打赌)
	*   [系统未读信息计数器](#系统未读信息计数器)

* 上行接口
	*	[获取注册验证码](#获取注册验证码)
	*	[注册](#注册)
	*	[登录](#登录)
	*	[上传图片](#上传图片)
	*	[发布打赌](#发布打赌)
	*	[参与打赌](#参与打赌)
	*	[公布答案](#公布答案)
	*	[分享打赌](#分享打赌)
	*	[邀请好友参与打赌](#邀请好友参与打赌)
	*	[撰写评论](#撰写评论)
	*	[发布私信](#发布私信)
	*	[更改头像](#更改头像)
	*	[更改昵称](#更改昵称)
	*	[编写心情](#编写心情)
	*	[邀请好友](#邀请好友)
	*	[退出](#退出)
	*	[单向加好友](#单向加好友)
	*	[通过好友验证](#通过好友验证)
	*   [微博登陆](#微博登陆)

接口说明
--------

<h2>好友动态列表接口</h2>
域名/capi/space.php?do=feed&uid=1&page=0&perpage=10&view=friend&dateline=1343793316&queryop=down&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0
#### 请求参数
	* 当前用户id -- uid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* 查询参数 -- view, 值为we代表好友动态列表
	* API密钥 -- m_auth, 由登录后返回
	* 时间点 -- dateline
	* 查询方式 -- queryop, 取值可以是up, down
		* up 代表上拉，取比dateline新的动态
		* down 代表到底，取紧接着dateline之后的动态
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[feeds]，feed列表， 条目字段如下
			* title_template -- feed的标题
			* body_template -- feed的内容
			* dateline -- feed的时间
			* uid -- 发布feed的用户id
			* username -- 发布feed用户
			* body_data -- feed的内容，当前仅有打赌、表态、评论、加为好友
				* 打赌(icon值为quiz)
					* subject -- 打赌标题
					* option -- 打赌A, B选择
						* oid -- 选项id
						* option -- 选项描述
						* relatedtime -- 最新投票的时间
						* votenum -- 投票人数
						* pic -- 选项图片
					* totalcost -- 奖池总额
					* endtime -- 截止时间
					* resulttime -- 预计公布答案时间
				* 表态(icon值click)
					* touser -- 操作的对象，文本描述
					* touserid -- 操作对象的用户id
					* click -- 表态的动作
					* subject -- 表态的打赌标题
					* id -- 表态的文章id
					* idtype -- 表态的文章类型，当前仅有quizid
				* 评论(icon值为comment)
					* touser -- 操作的对象，文本描述
					* touserid -- 操作对象的用户id
					* quiz -- 评论的打赌标题
					* quizid -- 评论的打赌id
				* 加为好友(icon值为friend)
					* touser -- 操作的对象，文本描述
					* touserid -- 操作对象的用户id
			* icon -- feed类型
				* quiz -- 打赌
				* do -- 心情
				* pic -- 图片
				* profile -- 更新资料
				* click -- 表太空
				* comment -- 评论
				* friend -- 成为好友
			* comments: 若是打赌动态，则会返回两条最新评论
			* commentnum: 若是打赌动态，则会返回打赌当前的评论总数
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{
		"code": 0,
		"data": {
			"feeds": [
				{
					"icon": "click",
					"uid": "15",
					"username": "xiao",
					"dateline": "1345429834",
					"friend": "0",
					"title_template": "feed_click_quiz",
					"title_data": {
						"touser": " fat___lin ",
						"subject": " wp8是否会让诺基亚走出困境 ",
						"click": "握手",
						"touseruid": "6",
						"id": "35",
						"idtype": "quiz"
					},
					"body_template": "",
					"body_data": [],
					"id": "0",
					"idtype": "",
					"hot": "0",
					"avatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/15_avatar_small.jpg"
				},
				{
					"icon": "comment",
					"uid": "15",
					"username": "xiao",
					"dateline": "1345429820",
					"friend": "0",
					"title_template": "{actor} 评论了 {touser} 的打赌 {quiz}",
					"title_data": {
						"touser": " fat___lin ",
						"quiz": " wp8是否会让诺基亚走出困境 ",
						"touseruid": "6",
						"quizid": "35"
					},
					"body_template": "",
					"body_data": [],
					"id": "0",
					"idtype": "",
					"hot": "0",
					"avatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/15_avatar_small.jpg"
				},
				{
					"icon": "friend",
					"uid": "15",
					"username": "xiao",
					"dateline": "1345429287",
					"friend": "0",
					"title_template": "{actor} 和 {touser} 成为了好友",
					"title_data": {
						"touser": " fat___lin ",
						"touseruid": "6"
					},
					"body_template": "",
					"body_data": [],
					"id": "0",
					"idtype": "",
					"hot": "0",
					"avatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/15_avatar_small.jpg"
				},
				{
					"icon": "profile",
					"uid": "15",
					"username": "xiao",
					"dateline": "1345429067",
					"friend": "0",
					"title_template": "{actor} 开通了自己的个人主页",
					"title_data": [],
					"body_template": "",
					"body_data": [],
					"id": "0",
					"idtype": "",
					"hot": "0",
					"avatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/15_avatar_small.jpg"
				},
				{
					"icon": "quiz",
					"uid": "6",
					"username": "fat___lin",
					"dateline": "1344838782",
					"friend": "0",
					"title_template": "{actor} 发表了新打赌",
					"title_data": [],
					"body_template": "<b>{subject}</b><br>{option}{totalcost}",
					"body_data": {
						"subject": "wp8是否会让诺基亚走出困境",
						"option": [
							{
								"oid": "67",
								"option": "会",
								"relatedtime": "1344838782",
								"votenum": "2"
							},
							{
								"oid": "68",
								"option": "不会",
								"relatedtime": "1344838782",
								"votenum": "0"
							}
						],
						"totalcost": "40",
						"endtime": "1345436753",
						"resulttime": "1345440353"
					},
					"id": "35",
					"idtype": "quizid",
					"hot": "2",
					"commentnum": "4",
					"comments": [
						{
							"cid": "43",
							"uid": "6",
							"id": "35",
							"idtype": "quizid",
							"authorid": "14",
							"authoravatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/06_avatar_small.jpg",
							"author": "lin",
							"ip": "113.111.133.241",
							"dateline": "1345428187",
							"message": "无条件支持老牌诺基亚！",
							"magicflicker": "0"
						},
						{
							"cid": "44",
							"uid": "6",
							"id": "35",
							"idtype": "quizid",
							"authorid": "14",
							"authoravatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/06_avatar_small.jpg",
							"author": "lin",
							"ip": "113.111.133.241",
							"dateline": "1345428234",
							"message": "期待wp8啊！！！",
							"magicflicker": "0"
						}
					],
					"avatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/06_avatar_small.jpg"
				},
				{
					"icon": "quiz",
					"uid": "6",
					"username": "fat___lin",
					"dateline": "1344831840",
					"friend": "0",
					"title_template": "{actor} 发表了新打赌",
					"title_data": [],
					"body_template": "<b>{subject}</b><br>{option}{totalcost}",
					"body_data": {
						"subject": "中国好声音里面，杨坤和哈林的学员谁会先满了",
						"option": [
							{
								"oid": "65",
								"option": "杨坤",
								"relatedtime": "1344831840",
								"votenum": "1"
							},
							{
								"oid": "66",
								"option": "哈林",
								"relatedtime": "1344831840",
								"votenum": "0"
							}
						],
						"totalcost": "20",
						"endtime": "1345436561",
						"resulttime": "1345440161"
					},
					"id": "34",
					"idtype": "quizid",
					"hot": "1",
					"commentnum": "1",
					"comments": [
						{
							"cid": "46",
							"uid": "6",
							"id": "34",
							"idtype": "quizid",
							"authorid": "14",
							"author": "lin",
							"ip": "113.111.133.241",
							"dateline": "1345428299",
							"message": "肯定是杨坤，他饥不择食啊。。",
							"magicflicker": "0"
						}
					],
					"avatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/06_avatar_small.jpg"
				},
				{
					"icon": "quiz",
					"uid": "6",
					"username": "fat___lin",
					"dateline": "1344831670",
					"friend": "0",
					"title_template": "{actor} 发表了新打赌",
					"title_data": [],
					"body_template": "<b>{subject}</b><br>{option}{totalcost}",
					"body_data": {
						"subject": "广州明晚会不会下雨（8月13号）",
						"option": [
							{
								"oid": "63",
								"option": "会",
								"relatedtime": "1344831670",
								"votenum": "0",
								"pic": "201208/13/6_1344831563P0d8.jpg"
							},
							{
								"oid": "64",
								"option": "不会",
								"relatedtime": "1344831670",
								"votenum": "0"
							}
						],
						"totalcost": "0",
						"endtime": "1345436233",
						"resulttime": "1345439833"
					},
					"id": "33",
					"idtype": "quizid",
					"hot": "0",
					"commentnum": "0",
					"avatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/06_avatar_small.jpg"
				},
				{
					"icon": "quiz",
					"uid": "6",
					"username": "fat___lin",
					"dateline": "1343961427",
					"friend": "0",
					"title_template": "{actor} 发表了新打赌",
					"title_data": [],
					"body_template": "<b>{subject}</b><br>{option}{totalcost}",
					"body_data": {
						"subject": "伦敦奥运会刘翔能否成功夺冠？",
						"option": [
							{
								"oid": "59",
								"option": "肯定能的啦",
								"relatedtime": "1343961427",
								"votenum": "2",
								"pic": "201208/3/6_1343961421UuUs.png"
							},
							{
								"oid": "60",
								"option": "对手太强，夺冠无望",
								"relatedtime": "1343961427",
								"votenum": "1",
								"pic": "201208/3/6_1343961413OiIi.jpg"
							}
						],
						"totalcost": "300",
						"endtime": "1344838912",
						"resulttime": "1344569296"
					},
					"id": "31",
					"idtype": "quizid",
					"hot": "1",
					"commentnum": "0",
					"avatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/06_avatar_small.jpg"
				},
				{
					"icon": "quiz",
					"uid": "6",
					"username": "fat___lin",
					"dateline": "1343960800",
					"friend": "0",
					"title_template": "{actor} 发表了新打赌",
					"title_data": [],
					"body_template": "<b>{subject}</b><br>{option}{totalcost}",
					"body_data": {
						"subject": "易建联脚裸受伤，下场比赛是否出赛？",
						"option": [
							{
								"oid": "57",
								"option": "会硬撑参赛的",
								"relatedtime": "1343960800",
								"votenum": "0",
								"pic": "201208/3/6_1343960641jmNj.png"
							},
							{
								"oid": "58",
								"option": "不会出场",
								"relatedtime": "1343960800",
								"votenum": "3",
								"pic": "201208/3/6_1343960712yJpT.gif"
							}
						],
						"totalcost": "300",
						"endtime": "1344838887",
						"resulttime": "1344567636"
					},
					"id": "30",
					"idtype": "quizid",
					"hot": "1",
					"commentnum": "0",
					"avatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/06_avatar_small.jpg"
				},
				{
					"icon": "quiz",
					"uid": "1",
					"username": "admin",
					"dateline": "1343817352",
					"friend": "0",
					"title_template": "{actor} 发表了新竞猜",
					"title_data": [],
					"body_template": "<b>{subject}</b><br>{option}",
					"body_data": {
						"subject": "下图哪个是本届金牌？",
						"option": [
							{
								"oid": "49",
								"option": "这个",
								"relatedtime": "1343817352",
								"votenum": "2",
								"pic": "201208/1/1_1343817334pZ1p.jpg"
							},
							{
								"oid": "50",
								"option": "应该是这个",
								"relatedtime": "1343817352",
								"votenum": "2",
								"pic": "201208/1/1_1343817348B2v5.jpg"
							}
						],
						"totalcost": "200",
						"endtime": "1343817501",
						"resulttime": "1344425641"
					},
					"id": "26",
					"idtype": "quizid",
					"hot": "1",
					"commentnum": "0",
					"avatar": "http://58.215.187.8:8081/center/data/avatar/000/00/00/01_avatar_small.jpg"
				}
			],
			"count": 10
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>全站动态列表接口</h2>
域名/capi/space.php?do=feed&uid=1&page=0&perpage=10&view=quiz&queryop=down&dateline=13234834&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0
#### 请求参数
	* 当前用户id -- uid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* 查询参数 -- view, 值为quiz代表全站打赌动态列表
	* API密钥 -- m_auth, 由登录后返回
	* 时间点 -- dateline
	* 查询方式 -- queryop, 取值可以是up, down
		* up 代表上拉，取比dateline新的动态
		* down 代表到底，取紧接着dateline之后的动态
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[feeds]，feed列表， 条目字段如下
			* title_template -- feed的标题
			* body_template -- feed的内容
			* dateline -- feed的时间
			* uid -- 发布feed的用户id
			* username -- 发布feed用户
			* body_data -- feed的内容，当前仅有打赌有意义
				* subject -- 打赌标题
				* option -- 打赌A, B选择
					* oid -- 选项id
					* option -- 选项描述
					* relatedtime -- 最新投票的时间
					* votenum -- 投票人数
					* pic -- 选项图片
				* totalcost -- 奖池总额
				* endtime -- 截止时间
				* resulttime -- 预计公布答案时间
			* icon -- feed类型
				* quiz -- 打赌
				* do -- 心情
				* pic -- 图片
				* profile -- 更新资料
			* comments: 若是打赌动态，则会返回两条最新评论
			* commentnum: 若是打赌动态，则会返回打赌当前的评论总数
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{
		"code": 0,
		"data": {
			"feeds": [
				{
					"icon": "quiz",
					"uid": "5",
					"username": "summit",
					"dateline": "1344929322",
					"friend": "0",
					"title_template": "{actor} 发表了新打赌",
					"title_data": [],
					"body_template": "<b>{subject}</b><br>{option}{totalcost}",
					"body_data": {
						"subject": "3423423",
						"option": [
							{
								"oid": "111",
								"option": "32423423",
								"relatedtime": "1344929322",
								"votenum": "2"
							},
							{
								"oid": "112",
								"option": "234324",
								"relatedtime": "1344929322",
								"votenum": "0"
							}
						],
						"totalcost": "40",
						"endtime": "1344929838",
						"resulttime": "1345537713"
					},
					"id": "57",
					"idtype": "quizid",
					"hot": "1",
					"commentnum": "0",
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				},
				{
					"icon": "quiz",
					"uid": "1",
					"username": "admin",
					"dateline": "1344929249",
					"friend": "0",
					"title_template": "{actor} 发表了新打赌",
					"title_data": [],
					"body_template": "<b>{subject}</b><br>{option}{totalcost}",
					"body_data": {
						"subject": "20120803时间戳",
						"option": [
							{
								"oid": "109",
								"option": "21",
								"relatedtime": "1344929249",
								"votenum": "0",
								"pic": "http://betit-pic.b0.upaiyun.com/201208/14/1_13449290756gK5.jpg"
							},
							{
								"oid": "110",
								"option": "123",
								"relatedtime": "1344929249",
								"votenum": "0",
								"pic": "http://betit-pic.b0.upaiyun.com/201208/14/1_1344929111K4Ac.png"
							}
						],
						"totalcost": "0",
						"endtime": "1345533855",
						"resulttime": "1345537455"
					},
					"id": "56",
					"idtype": "quizid",
					"hot": "0",
					"commentnum": "0",
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/01_avatar_small.jpg"
				}
			],
			"count": 2
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>通知列表接口</h2>
域名/capi/space.php?do=notice&page=0&prepage=2&uid=1&type=quizinvalid&dateline=324234&queryop=up&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0
#### 请求参数
	* 当前用户id -- uid
	* 第几页 -- page
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
	* 时间点 -- dateline
	* 查询方式 -- queryop, 取值可以是up, down
		* up 代表上拉，取比dateline新的动态
		* down 代表到底，取紧接着dateline之后的动态
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
			* avatar -- 通知头像
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{
		"code": 0,
		"data": {
			"notices": [
				{
					"id": "205",
					"uid": "5",
					"type": "quiz",
					"new": "0",
					"authorid": "1",
					"author": "summit",
					"note": "温馨提示：你的 《我的打赌》 的打赌将在1小时后到期，请及时公布答案.",
					"dateline": "1344932518",
					"isfriend": 0,
					"style": "",
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				},
				{
					"id": "206",
					"uid": "5",
					"type": "quizexceed",
					"new": "0",
					"authorid": "1",
					"author": "summit",
					"note": "由于你的 《我的打赌》 打赌由于超期没有公布答案，已被取消并扣除你的信用20。",
					"dateline": "1344932518",
					"isfriend": 0,
					"style": "",
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				}
			],
			"count": 2
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>私信列表接口</h2>
域名/capi/space.php?do=pm&page=0&prepage=2&uid=1&filter=newpm&dateline=0&queryop=up&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0
#### 请求参数
	* 当前用户id -- uid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* 私信类型 -- filter
		* newpm -- 未读私信
		* privatepm -- 私人消息
		* systempm -- 系统消息
		* announcepm -- 公共消息
		* 空 -- 私人消息
	* API密钥 -- m_auth, 由登录后返回
	* 时间点 -- dateline
	* 查询方式 -- queryop, 取值可以是up, down
		* up 代表上拉，取比dateline新的动态
		* down 代表到底，取紧接着dateline之后的动态
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[pms]，私信列表， 条目字段如下
			* pmid -- 私信id
			* msgfrom -- 消息发送人
			* msgfromavatar -- 消息发送人头像
			* msgfromid -- 消息发送人id
			* msgtoid -- 消息接收人id
			* msgtoavatar -- 消息接收人头像
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
	{
		"code": 0,
		"data": {
			"pms": [
				{
					"pmid": "7",
					"msgfrom": "admin",
					"msgfromid": "1",
					"msgtoid": "5",
					"new": "0",
					"subject": "你好summit",
					"dateline": "1344324792",
					"message": "你好summit",
					"delstatus": "0",
					"related": "0",
					"fromappid": "1",
					"daterange": 5,
					"touid": "1",
					"msgfromavatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/01_avatar_small.jpg",
					"msgtoavatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				}
			],
			"count": 1
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>私信详情</h2>
域名/capi/space.php?do=pm&subop=view&pmid=2&touid=12&daterange=10&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZUXHu0
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
			* msgfromavatar -- 消息发送人头像
			* msgtoid -- 消息接收人id
			* msgtoavatar -- 消息接收人头像
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
	{
		"code": 0,
		"data": {
			"pms": [
				{
					"pmid": "6",
					"msgfrom": "summit",
					"msgfromid": "5",
					"msgtoid": "1",
					"folder": "inbox",
					"new": "1",
					"subject": "23423432423",
					"dateline": "1344324163",
					"message": "23423432423",
					"delstatus": "0",
					"related": "1",
					"fromappid": "1",
					"daterange": 5,
					"msgfromavatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg",
					"msgtoavatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/01_avatar_small.jpg"
				},
				{
					"pmid": "8",
					"msgfrom": "summit",
					"msgfromid": "5",
					"msgtoid": "1",
					"folder": "inbox",
					"new": "1",
					"subject": "你好吧。admin",
					"dateline": "1344324259",
					"message": "你好吧。admin",
					"delstatus": "0",
					"related": "1",
					"fromappid": "1",
					"daterange": 5,
					"msgfromavatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg",
					"msgtoavatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/01_avatar_small.jpg"
				},
				{
					"pmid": "9",
					"msgfrom": "admin",
					"msgfromid": "1",
					"msgtoid": "5",
					"folder": "inbox",
					"new": "0",
					"subject": "你好summit",
					"dateline": "1344324792",
					"message": "你好summit",
					"delstatus": "0",
					"related": "1",
					"fromappid": "1",
					"daterange": 5,
					"msgfromavatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/01_avatar_small.jpg",
					"msgtoavatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				}
			],
			"count": 3
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>好友排行榜接口</h2> 
域名/capi/space.php?uid=5&do=friend&m_auth=54f8qnt8HxbRz8NWomy0e4k2gKvVvc6oil8qDY9upUERswmzj
#### 请求参数
	* 当前用户id -- uid
	* API密钥 -- m_auth, 由登录后返回

#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
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
			* spacenote -- 心情
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
			* creditrank -- 金币排行
			* experiencerank -- 经验排行
		* data[count], 返回列表条目数, 便用遍历

#### 样例
	{
		"code": 0,
		"data": {
			"friends": [
				{
					"uid": "5",
					"groupid": "11",
					"credit": "1040",
					"experience": "1004",
					"username": "summit",
					"name": "",
					"namestatus": "0",
					"videostatus": "0",
					"domain": "",
					"friendnum": "10",
					"viewnum": "20",
					"notenum": "22",
					"addfriendnum": "0",
					"mtaginvitenum": "0",
					"eventinvitenum": "0",
					"myinvitenum": "0",
					"pokenum": "0",
					"doingnum": "0",
					"blognum": "0",
					"albumnum": "0",
					"threadnum": "0",
					"pollnum": "0",
					"eventnum": "0",
					"sharenum": "0",
					"dateline": "1343726668",
					"updatetime": "1343726701",
					"lastsearch": "0",
					"lastpost": "1343726701",
					"lastlogin": "1344936333",
					"lastsend": "0",
					"attachsize": "0",
					"addsize": "0",
					"addfriend": "0",
					"flag": "0",
					"newpm": "0",
					"avatar": "http://58.215.187.8:8081/center/images/noavatar_small.gif",
					"regip": "113.111.115.181",
					"ip": "74125184",
					"mood": "0",
					"quiznum": "0",
					"winnum": "1",
					"lostnum": "0",
					"voternum": "1",
					"resideprovince": "",
					"residecity": "",
					"note": "",
					"spacenote": "",
					"sex": "0",
					"gid": "0",
					"num": "5",
					"creditrank": "4",
					"experiencerank": "3",
					"p": "",
					"c": "",
					"group": "其他",
					"isfriend": 1
				},
				{
					"uid": "1",
					"groupid": "5",
					"credit": "152",
					"experience": "45",
					"username": "admin",
					"name": "",
					"namestatus": "0",
					"videostatus": "0",
					"domain": "",
					"friendnum": "8",
					"viewnum": "7",
					"notenum": "1",
					"addfriendnum": "0",
					"mtaginvitenum": "0",
					"eventinvitenum": "0",
					"myinvitenum": "0",
					"pokenum": "1",
					"doingnum": "0",
					"blognum": "1",
					"albumnum": "0",
					"threadnum": "0",
					"pollnum": "0",
					"eventnum": "0",
					"sharenum": "0",
					"dateline": "1343725030",
					"updatetime": "1343873852",
					"lastsearch": "0",
					"lastpost": "1343873852",
					"lastlogin": "1346209918",
					"lastsend": "0",
					"attachsize": "2155640",
					"addsize": "0",
					"addfriend": "0",
					"flag": "0",
					"newpm": "0",
					"avatar": "http://58.215.187.8:8081/center/images/noavatar_small.gif",
					"regip": "127.0.0.1",
					"ip": "113111119",
					"mood": "0",
					"quiznum": "2",
					"winnum": "0",
					"lostnum": "1",
					"voternum": "2",
					"resideprovince": "",
					"residecity": "",
					"note": "",
					"spacenote": "",
					"sex": "0",
					"gid": "0",
					"num": "1",
					"creditrank": "4",
					"experiencerank": "3",
					"p": "",
					"c": "",
					"group": "其他",
					"isfriend": 1
				},
				{
					"uid": "14",
					"groupid": "5",
					"credit": "79",
					"experience": "14",
					"username": "lin",
					"name": "",
					"namestatus": "0",
					"videostatus": "0",
					"domain": "",
					"friendnum": "5",
					"viewnum": "3",
					"notenum": "0",
					"addfriendnum": "0",
					"mtaginvitenum": "0",
					"eventinvitenum": "0",
					"myinvitenum": "0",
					"pokenum": "2",
					"doingnum": "0",
					"blognum": "0",
					"albumnum": "0",
					"threadnum": "0",
					"pollnum": "0",
					"eventnum": "0",
					"sharenum": "0",
					"dateline": "1344825403",
					"updatetime": "0",
					"lastsearch": "0",
					"lastpost": "0",
					"lastlogin": "1345707145",
					"lastsend": "0",
					"attachsize": "0",
					"addsize": "0",
					"addfriend": "0",
					"flag": "0",
					"newpm": "0",
					"avatar": "http://58.215.187.8:8081/center/images/noavatar_small.gif",
					"regip": "113.111.133.144",
					"ip": "113111117",
					"mood": "0",
					"quiznum": "0",
					"winnum": "0",
					"lostnum": "0",
					"voternum": "2",
					"resideprovince": "",
					"residecity": "",
					"note": "",
					"spacenote": "",
					"sex": "0",
					"gid": "0",
					"num": "0",
					"creditrank": "4",
					"experiencerank": "3",
					"p": "",
					"c": "",
					"group": "其他",
					"isfriend": 1
				}
			],
			"count": 3
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>热门打赌排行榜接口</h2>
域名/capi/space.php?do=feed&uid=1&page=0&perpage=10&view=quizhot&dateline=234324&queryop=up&m_auth=55dalDuJytwHteL6s5qlKwHLmhIhpGZ4fZU
#### 请求参数
	* 用户id -- uid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* 查询参数 -- view, 必须为quizhot, do, 必须为feed
	* API密钥 -- m_auth, 由登录后返回
	* 时间点 -- dateline
	* 查询方式 -- queryop, 取值可以是up, down
		* up 代表上拉，取比dateline新的动态
		* down 代表到底，取紧接着dateline之后的动态
#### 返回结果
	* 错误码 -- code, 0:代表成功， 1:代表失败
		* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
		* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[feeds]，feed列表， 条目字段如下
			* title_template -- feed的标题
			* body_template -- feed的内容
			* dateline -- feed的时间
			* uid -- 发布feed的用户id
			* username -- 发布feed用户
			* body_data -- feed的内容，当前仅有打赌有意义
				* subject -- 打赌标题
				* option -- 打赌A, B选择
					* oid -- 选项id
					* option -- 选项描述
					* relatedtime -- 最新投票的时间
					* votenum -- 投票人数
					* pic -- 选项图片
				* totalcost -- 奖池总额
				* endtime -- 截止时间
				* resulttime -- 预计公布答案时间
			* icon -- feed类型
				* quiz -- 打赌
				* do -- 心情
				* pic -- 图片
				* profile -- 更新资料
			* comments: 若是打赌动态，则会返回两条最新评论
			* commentnum: 若是打赌动态，则会返回打赌当前的评论总数
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{
		"code": 0,
		"data": {
			"feeds": [
				{
					"icon": "quiz",
					"uid": "5",
					"username": "summit",
					"dateline": "1344929322",
					"friend": "0",
					"title_template": "{actor} 发表了新打赌",
					"title_data": [],
					"body_template": "<b>{subject}</b><br>{option}{totalcost}",
					"body_data": {
						"subject": "3423423",
						"option": [
							{
								"oid": "111",
								"option": "32423423",
								"relatedtime": "1344929322",
								"votenum": "2"
							},
							{
								"oid": "112",
								"option": "234324",
								"relatedtime": "1344929322",
								"votenum": "0"
							}
						],
						"totalcost": "40",
						"endtime": "1344929838",
						"resulttime": "1345537713"
					},
					"id": "57",
					"idtype": "quizid",
					"hot": "1",
					"commentnum": "0",
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				},
				{
					"icon": "quiz",
					"uid": "1",
					"username": "admin",
					"dateline": "1344929249",
					"friend": "0",
					"title_template": "{actor} 发表了新打赌",
					"title_data": [],
					"body_template": "<b>{subject}</b><br>{option}{totalcost}",
					"body_data": {
						"subject": "20120803时间戳",
						"option": [
							{
								"oid": "109",
								"option": "21",
								"relatedtime": "1344929249",
								"votenum": "0",
								"pic": "http://betit-pic.b0.upaiyun.com/201208/14/1_13449290756gK5.jpg"
							},
							{
								"oid": "110",
								"option": "123",
								"relatedtime": "1344929249",
								"votenum": "0",
								"pic": "http://betit-pic.b0.upaiyun.com/201208/14/1_1344929111K4Ac.png"
							}
						],
						"totalcost": "0",
						"endtime": "1345533855",
						"resulttime": "1345537455"
					},
					"id": "56",
					"idtype": "quizid",
					"hot": "0",
					"commentnum": "0",
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/01_avatar_small.jpg"
				}
			],
			"count": 2
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>我的个人信息</h2>
域名/capi/cp.php?ac=profile&m_auth=65e8JkX8RscU2y2pYZEVdcZrja2YOr2QXuhbPBCHzLAw
#### 请求参数
	* API密钥 -- m_auth, 由登录后返回
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回一个数据
		* data[space], 当前登录用户的信息，具体内容如下
			* 用户id -- uid
			* 性别 -- sex, 男取值0， 女取值1
			* 用户邮箱 -- email
			* 手机 -- mobile
			* qq帐号 -- qq
			* msn帐号 -- msn
			* weibo帐号 -- weibo
			* 隐私数组 -- privacy, 由类型区分0代表全站可见
			* 动态数组 -- feed, 由类型区分
			* 好友数 -- friend
			* 动态好友数 -- feedfriend
			* 金币 -- credit
			* 信用 -- experience
			* 用户名 -- username
			* 实名 -- name
			* 是否实名 -- namestatus, 1是, 0否
			* 心情数 -- doingnum
			* 分享数 -- sharenum
			* 最近活跃时间 -- dateline
			* 最近更新时间 -- updatetime
			* 最近一次搜索时间 -- lastsearch
			* 最近一次发布时间 -- lastpost
			* 最近一次登录时间 -- lastlogin
			* 最近一次发送消息时间 -- lastsend
			* 是否禁用 -- flag
			* 是否有新通知 -- newpm
			* 头像 -- avatar
			* 登录的ip -- ip
			* 附件大小 -- attachsize
			* 发布的打赌数 -- quiznum
			* 赢的次数 -- winnum
			* 输的次数 -- lostnum
			* 参与打赌数 -- voternum
			* 好友列表id -- friends

			
#### 样例
	{
		"code": 0,
		"data": {
			"space": {
				"uid": "5",
				"sex": "0",
				"email": "summit_mail@qq.com",
				"newemail": "",
				"emailcheck": "0",
				"mobile": "",
				"qq": "",
				"msn": "",
				"msnrobot": "",
				"msncstatus": "0",
				"videopic": "",
				"birthyear": "0",
				"birthmonth": "0",
				"birthday": "0",
				"blood": "",
				"marry": "0",
				"birthprovince": "",
				"birthcity": "",
				"resideprovince": "",
				"residecity": "",
				"note": "",
				"spacenote": "",
				"authstr": "",
				"theme": "",
				"nocss": "0",
				"menunum": "0",
				"css": "",
				"privacy": {
					"view": {
						"index": "0",
						"friend": "0",
						"wall": "0",
						"feed": "0",
						"mtag": "0",
						"event": "0",
						"doing": "0",
						"blog": "0",
						"quiz": "0",
						"album": "0",
						"share": "0",
						"poll": "0"
					},
					"feed": {
						"doing": 1,
						"blog": 1,
						"quiz": 1,
						"joinquiz": 1,
						"upload": 1,
						"share": 1,
						"poll": 1,
						"joinpoll": 1,
						"thread": 1,
						"post": 1,
						"mtag": 1,
						"event": 1,
						"join": 1,
						"friend": 1,
						"comment": 1,
						"show": 1,
						"credit": 1,
						"spaceopen": 1,
						"invite": 1,
						"task": 1,
						"profile": 1,
						"click": 1
					}
				},
				"friend": "7",
				"feedfriend": "7",
				"sendmail": "",
				"magicstar": "0",
				"magicexpire": "0",
				"timeoffset": "",
				"weibo": "",
				"groupid": "11",
				"credit": "2048",
				"experience": "2108",
				"username": "summit",
				"name": "",
				"namestatus": "0",
				"videostatus": "0",
				"domain": "",
				"friendnum": "1",
				"viewnum": "17",
				"notenum": "0",
				"addfriendnum": "0",
				"mtaginvitenum": "0",
				"eventinvitenum": "0",
				"myinvitenum": "0",
				"pokenum": "0",
				"doingnum": "0",
				"blognum": "2",
				"albumnum": "0",
				"threadnum": "0",
				"pollnum": "0",
				"eventnum": "0",
				"sharenum": "0",
				"dateline": "1343789930",
				"updatetime": "1344932295",
				"lastsearch": "0",
				"lastpost": "1344932295",
				"lastlogin": "1345359730",
				"lastsend": "0",
				"attachsize": "0",
				"addsize": "0",
				"addfriend": "0",
				"flag": "0",
				"newpm": "0",
				"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg",
				"regip": "127.0.0.1",
				"ip": "127000000",
				"mood": "0",
				"quiznum": "10",
				"winnum": "4",
				"lostnum": "1",
				"voternum": "8",
				"self": 1,
				"friends": [
					"7"
				],
				"allnotenum": 0
			}
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>打赌详情</h2>
域名/capi/space.php?do=quiz&id=54&uid=5&m_auth=af9cCEMpQlfFTifZltugadwhGAXL%2Ba%2BCor8voR9jZyBh60v4xFryq2ibMM1tNHXaHYweU%2B8hsBHobKzgHFJs

#### 请求参数
	* 打赌id -- id
	* 发布此打赌的用户id -- uid
	* API密钥 -- m_auth, 由登录后返回

#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回一个数据
		* data[quiz], 打赌详情，具体内容如下
			* 打赌id -- quizid
			* 发布打赌用户id -- uid
			* 发布打赌用户头像 -- avatar
			* 最热用户 -- hotuser
			* 发布时间 -- dateline
			* 投一注所需金币 -- joincost
			* 用户最大投注数 -- portion
			* 截止投注时间 -- endtime
			* 预计公布结果时间 -- resulttime
			* 最近一次投注时间 -- lastvote
			* 当前累计投注 -- voternum
			* 奖金池 -- totalcost
			* 是否已经提醒过 -- hasremind
			* 是否已经超期 -- hasexceed
			* 答案选项id -- keyoid
			* 答案 -- keyoption
			* 选项数组 -- options，具体内容如下：
				* 选项id -- oid
				* 所属竞猜 -- quizid
				* 用户id -- uid
				* 选项 -- option, 文本描述
				* 相片id -- picid
				* 相片路径 -- pic
				* 投注人数 -- votenum
				* 投注占总投注百分比 -- percent

#### 样例
	{
		"code": 0,
		"data": {
			"quiz": {
				"quizid": "52",
				"uid": "5",
				"tag": [],
				"message": "",
				"postip": "127.0.0.1",
				"related": [],
				"relatedtime": "0",
				"target_ids": "",
				"hotuser": "",
				"magiccolor": "0",
				"magicpaper": "0",
				"magiccall": "0",
				"option": "a:2:{i:0;s:3:\"能\";i:1;s:6:\"不能\";}",
				"invite": "",
				"topicid": "0",
				"username": "summit",
				"subject": "测试优惠券",
				"classid": "0",
				"viewnum": "1",
				"replynum": "0",
				"hot": "0",
				"dateline": "1344236417",
				"pic": "",
				"picflag": "0",
				"noreply": "0",
				"friend": "0",
				"password": "",
				"click_1": "0",
				"click_2": "0",
				"click_3": "0",
				"click_4": "0",
				"click_5": "0",
				"joincost": "20",
				"portion": "3",
				"endtime": "1344236757",
				"resulttime": "1344844795",
				"lastvote": "1344236423",
				"voternum": "1",
				"maxchoice": "0",
				"sex": "0",
				"keyoid": "102",
				"keyoption": "不能",
				"totalcost": "20",
				"hasremind": "1",
				"hasexceed": "0",
				"options": [
					{
						"oid": "101",
						"quizid": "52",
						"uid": "5",
						"option": "能",
						"relatedtime": "1344236417",
						"picid": "0",
						"votenum": "1",
						"percent": 100,
						"width": 160
					},
					{
						"oid": "102",
						"quizid": "52",
						"uid": "5",
						"option": "不能",
						"relatedtime": "1344236417",
						"picid": "0",
						"votenum": "0",
						"percent": 0,
						"width": 0
					}
				],
				"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
			}
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>获取投注好友</h2>
域名/capi/do.php?ac=ajax&op=getjoinuser&oid=33&page=0&prepage=10&m_auth=7c44hpLskh17xPRklyu
#### 请求参数
	* 操作类型(固定搭配) -- op:getjoinuser
	* 投注的选项id -- oid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* API密钥 -- m_auth, 由登录后返回
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[joinusers],用户列表(以joinnum排序)，具体内容如下
			* 投注id -- jid(请忽略)
			* 用户id -- uid
			* 用户名 -- username
			* 打赌id -- quizid
			* 投注的选项 -- option，文本
			* 投注时间 -- dateline(请忽略)
			* 选项id -- oid
			* 投注份数 -- joinnum
			* 用户组别 -- grouptitle
		* data[count], 返回列表条目数, 便用遍历

#### 样例
	{"code":0,"data":{"joinusers":[{"jid":"29","uid":"4","username":"summit2","quizid":"18","option":"\"\u80fd\"","dateline":"1343787281","oid":"33","joinnum":"3",
	"avatar":"http:\/\/localhost:8080\/betit\/center\/data\/avatar\/000\/00\/00\/04_avatar_middle.jpg"， "grouptitle":"赌霸"},{"jid":"34","uid":"5","username":"summit","quizid":"18",
	"option":"\"\u80fd\"","dateline":"1343792803","oid":"33","joinnum":"1","avatar":"http:\/\/localhost:8080\/betit\/center\/data\/avatar\/000\/00\/00\/05_avatar_middle.jpg", "grouptitle":"赌霸"}],
	"count":2},"msg":"\u6570\u636e\u83b7\u53d6\u6210\u529f","action":"rest_success"}
[↑返回顶部](#betit)

<h2>评论列表</h2>
域名/capi/do.php?ac=ajax&op=getcomment&id=24&idtype=quizid&page=0&prepage=1&dateline=234234&queryop=up&m_auth=af9cCEMpQlfFTifZltugadwhG

#### 请求参数
	* 操作类型 -- op, 必须为getcomment
	* 查询评论关联的id -- id, 若为打赌，则为打赌id值，若为空间则为用户id值，若为分享则为分享id值
	* 指示id代表的类型 -- idtype, quizid代表打赌，uid代表空间, sid代表分享
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* API密钥 -- m_auth, 由登录后返回
	* 时间点 -- dateline
	* 查询方式 -- queryop, 取值可以是up, down
		* up 代表上拉，取比dateline新的评论
		* down 代表到底，取紧接着dateline之后的评论
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[comments],评论列表，具体内容如下
			* 评论id -- cid
			* 评论对象，用户id -- uid
			* 评论对象头像 -- avatar
			* 评论关联的id -- id
			* 评论类型 -- idtype
			* 发表评论的用户id -- authorid
			* 发表评论的用户头像 -- authoravatar
			* 发表评论的用户名 -- author
			* 发表的时间 -- dateline
			* 发表的ip -- ip
			* 评论的内容 -- message
		* data[count], 返回列表条目数, 便用遍历

#### 样例
	{
    "code": 0,
    "data": {
        "comments": [
            {
                "cid": "31",
                "uid": "1",
                "id": "24",
                "idtype": "quizid",
                "authorid": "1",
                "author": "admin",
                "ip": "127.0.0.1",
                "dateline": "1344407149",
                "message": "234234",
                "magicflicker": "0",
                "avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/01_avatar_small.jpg"
            }
        ],
        "count": 1
    },
    "msg": "数据获取成功",
    "action": "rest_success"
}

<h2>搜索打赌</h2>
域名/capi/space.php?uid=5&do=quiz&page=0&perpage=2&view=new&searchkey=测试&m_auth=af9cCEMpQ
#### 请求参数
	* 用户id -- uid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* 查询参数 -- view, 必须为new
	* 查询内容 -- searchkey
	* API密钥 -- m_auth, 由登录后返回
[↑返回顶部](#betit)

#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回三个数据
		* data[quizs]，打赌列表， 条目字段如下
			* 打赌id : quizid
			* 发布打赌的用户id : uid
			* 发布打赌的用户头像: avatar
			* 发布打赌的用户名 : username
			* 打赌标题: subject
			* 浏览次数: viewnum
			* 回复次数：replynum
			* 热度: hot
			* 时间: dateline
			* 参与所需金币: joincost
			* 允许最大投注次数: portion
			* 截止时间: endtime
			* 预计公布结果时间: resulttime
			* 最近一次投票时间: lastvote
			* 参与打赌的人数: voternum
			* 答案id: keyoid
			* 答案: keyoption
			* 奖金池: totalcost
		* data[count], 返回列表条目数, 便用遍历
		* data[reward], 查询操作扣除的金币和信用

#### 样例
	{
		"code": 0,
		"data": {
			"quizs": [
				{
					"quizid": "54",
					"topicid": "0",
					"uid": "5",
					"username": "summit",
					"subject": "测试优惠券",
					"classid": "0",
					"viewnum": "6",
					"replynum": "0",
					"hot": "0",
					"dateline": "1344237052",
					"pic": "",
					"picflag": "0",
					"noreply": "0",
					"friend": "0",
					"password": "",
					"click_1": "0",
					"click_2": "0",
					"click_3": "0",
					"click_4": "0",
					"click_5": "0",
					"joincost": "20",
					"portion": "3",
					"endtime": "1344237071",
					"resulttime": "1344845443",
					"lastvote": "1344237066",
					"voternum": "1",
					"maxchoice": "0",
					"sex": "0",
					"keyoid": "106",
					"keyoption": "3",
					"totalcost": "60",
					"hasremind": "1",
					"hasexceed": "0",
					"tag": "",
					"message": "",
					"postip": "127.0.0.1",
					"related": "",
					"relatedtime": "0",
					"target_ids": "",
					"hotuser": "",
					"magiccolor": "0",
					"magicpaper": "0",
					"magiccall": "0",
					"option": [
						"12",
						"3"
					],
					"invite": ",7",
					"optioncount": [
						"2",
						"1"
					],
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				},
				{
					"quizid": "52",
					"topicid": "0",
					"uid": "5",
					"username": "summit",
					"subject": "测试优惠券",
					"classid": "0",
					"viewnum": "2",
					"replynum": "0",
					"hot": "0",
					"dateline": "1344236417",
					"pic": "",
					"picflag": "0",
					"noreply": "0",
					"friend": "0",
					"password": "",
					"click_1": "0",
					"click_2": "0",
					"click_3": "0",
					"click_4": "0",
					"click_5": "0",
					"joincost": "20",
					"portion": "3",
					"endtime": "1344236757",
					"resulttime": "1344844795",
					"lastvote": "1344236423",
					"voternum": "1",
					"maxchoice": "0",
					"sex": "0",
					"keyoid": "102",
					"keyoption": "不能",
					"totalcost": "20",
					"hasremind": "1",
					"hasexceed": "0",
					"tag": "",
					"message": "",
					"postip": "127.0.0.1",
					"related": "",
					"relatedtime": "0",
					"target_ids": "",
					"hotuser": "",
					"magiccolor": "0",
					"magicpaper": "0",
					"magiccall": "0",
					"option": [
						"能",
						"不能"
					],
					"invite": "",
					"optioncount": [
						"1",
						"0"
					],
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				}
			],
			"count": 2,
			"reward": {
				"credit": 1,
				"experience": 0
			}
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>搜索好友</h2>
域名/capi/cp.php?ac=friend&op=search&page=0&perpage=1&searchkey=admin&searchsubmit=true&searchmode=1&m_auth=af9cCEMpQ
#### 请求参数
	* 用户id -- uid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* 查询参数 -- searchsubmit必须为true, searchmode必须为1
	* 查询内容 -- searchkey
	* API密钥 -- m_auth, 由登录后返回

#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[friend]，打赌列表， 条目字段如下
			* 用户id -- uid
			* 用户头像 -- avatar
			* 金币 -- credit
			* 信用 -- experience
			* 用户名 -- username
			* 实名 -- name
			* 是否实名 -- namestatus, 1是, 0否
			* 心情数 -- doingnum
			* 分享数 -- sharenum
			* 最近活跃时间 -- dateline
			* 最近更新时间 -- updatetime
			* 最近一次搜索时间 -- lastsearch
			* 最近一次发布时间 -- lastpost
			* 最近一次登录时间 -- lastlogin
			* 最近一次发送消息时间 -- lastsend
			* 是否禁用 -- flag
			* 是否有新通知 -- newpm
			* 头像 -- avatar
			* 登录的ip -- ip
			* 附件大小 -- attachsize
			* 发布的打赌数 -- quiznum
			* 赢的次数 -- winnum
			* 输的次数 -- lostnum
			* 参与打赌数 -- voternum
			* 是否好友-- isfriend, 0否，1是
		* data[count], 返回列表条目数, 便用遍历

#### 样例
	{
		"code": 0,
		"data": {
			"friends": [
				{
					"uid": "5",
					"groupid": "11",
					"credit": "1040",
					"experience": "1004",
					"username": "summit",
					"name": "",
					"namestatus": "0",
					"videostatus": "0",
					"domain": "",
					"friendnum": "10",
					"viewnum": "20",
					"notenum": "22",
					"addfriendnum": "0",
					"mtaginvitenum": "0",
					"eventinvitenum": "0",
					"myinvitenum": "0",
					"pokenum": "0",
					"doingnum": "0",
					"blognum": "0",
					"albumnum": "0",
					"threadnum": "0",
					"pollnum": "0",
					"eventnum": "0",
					"sharenum": "0",
					"dateline": "1343726668",
					"updatetime": "1343726701",
					"lastsearch": "0",
					"lastpost": "1343726701",
					"lastlogin": "1344936333",
					"lastsend": "0",
					"attachsize": "0",
					"addsize": "0",
					"addfriend": "0",
					"flag": "0",
					"newpm": "0",
					"avatar": "http://58.215.187.8:8081/center/images/noavatar_small.gif",
					"regip": "113.111.115.181",
					"ip": "74125184",
					"mood": "0",
					"quiznum": "0",
					"winnum": "1",
					"lostnum": "0",
					"voternum": "1",
					"resideprovince": "",
					"residecity": "",
					"note": "",
					"spacenote": "",
					"sex": "0",
					"gid": "0",
					"num": "5",
					"p": "",
					"c": "",
					"group": "其他",
					"isfriend": 1
				},
				{
					"uid": "1",
					"groupid": "5",
					"credit": "152",
					"experience": "45",
					"username": "admin",
					"name": "",
					"namestatus": "0",
					"videostatus": "0",
					"domain": "",
					"friendnum": "8",
					"viewnum": "7",
					"notenum": "1",
					"addfriendnum": "0",
					"mtaginvitenum": "0",
					"eventinvitenum": "0",
					"myinvitenum": "0",
					"pokenum": "1",
					"doingnum": "0",
					"blognum": "1",
					"albumnum": "0",
					"threadnum": "0",
					"pollnum": "0",
					"eventnum": "0",
					"sharenum": "0",
					"dateline": "1343725030",
					"updatetime": "1343873852",
					"lastsearch": "0",
					"lastpost": "1343873852",
					"lastlogin": "1346209918",
					"lastsend": "0",
					"attachsize": "2155640",
					"addsize": "0",
					"addfriend": "0",
					"flag": "0",
					"newpm": "0",
					"avatar": "http://58.215.187.8:8081/center/images/noavatar_small.gif",
					"regip": "127.0.0.1",
					"ip": "113111119",
					"mood": "0",
					"quiznum": "2",
					"winnum": "0",
					"lostnum": "1",
					"voternum": "2",
					"resideprovince": "",
					"residecity": "",
					"note": "",
					"spacenote": "",
					"sex": "0",
					"gid": "0",
					"num": "1",
					"p": "",
					"c": "",
					"group": "其他",
					"isfriend": 1
				},
				{
					"uid": "14",
					"groupid": "5",
					"credit": "79",
					"experience": "14",
					"username": "lin",
					"name": "",
					"namestatus": "0",
					"videostatus": "0",
					"domain": "",
					"friendnum": "5",
					"viewnum": "3",
					"notenum": "0",
					"addfriendnum": "0",
					"mtaginvitenum": "0",
					"eventinvitenum": "0",
					"myinvitenum": "0",
					"pokenum": "2",
					"doingnum": "0",
					"blognum": "0",
					"albumnum": "0",
					"threadnum": "0",
					"pollnum": "0",
					"eventnum": "0",
					"sharenum": "0",
					"dateline": "1344825403",
					"updatetime": "0",
					"lastsearch": "0",
					"lastpost": "0",
					"lastlogin": "1345707145",
					"lastsend": "0",
					"attachsize": "0",
					"addsize": "0",
					"addfriend": "0",
					"flag": "0",
					"newpm": "0",
					"avatar": "http://58.215.187.8:8081/center/images/noavatar_small.gif",
					"regip": "113.111.133.144",
					"ip": "113111117",
					"mood": "0",
					"quiznum": "0",
					"winnum": "0",
					"lostnum": "0",
					"voternum": "2",
					"resideprovince": "",
					"residecity": "",
					"note": "",
					"spacenote": "",
					"sex": "0",
					"gid": "0",
					"num": "0",
					"p": "",
					"c": "",
					"group": "其他",
					"isfriend": 1
				}
			],
			"count": 3
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>推荐打赌列表</h2>
#### 注意：同 [热门打赌排行榜接口](#热门打赌排行榜接口)
域名/capi/space.php?uid=5&do=quiz&page=0&perpage=2&view=hot&dateline=234234&queryop=up&m_auth=54f8qnt8HxbRz8NWomy0e4k2gKvVvc6oil8qDY9upUERswmzj17Dt8R%252B652pTEKjHTOgNjgJ80RzLSsp7vbN
#### 请求参数
	* 用户id -- uid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* 查询参数 -- view, 必须为hot
	* API密钥 -- m_auth, 由登录后返回
	* 时间点 -- dateline
	* 查询方式 -- queryop, 取值可以是up, down
		* up 代表上拉，取比dateline新的打赌
		* down 代表到底，取紧接着dateline之后的打赌
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[quizs]，打赌列表， 条目字段如下
			* 打赌id : quizid
			* 发布打赌的用户id : uid
			* 发布打赌的用户名 : username
			* 打赌标题: subject
			* 浏览次数: viewnum
			* 回复次数：replynum
			* 热度: hot
			* 时间: dateline
			* 参与所需金币: joincost
			* 允许最大投注次数: portion
			* 截止时间: endtime
			* 预计公布结果时间: resulttime
			* 最近一次投票时间: lastvote
			* 参与打赌的人数: voternum
			* 答案id: keyoid
			* 答案: keyoption
			* 奖金池: totalcost
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{
		"code": 0,
		"data": {
			"quizs": [
				{
					"quizid": "54",
					"topicid": "0",
					"uid": "5",
					"username": "summit",
					"subject": "测试优惠券",
					"classid": "0",
					"viewnum": "6",
					"replynum": "0",
					"hot": "0",
					"dateline": "1344237052",
					"pic": "",
					"picflag": "0",
					"noreply": "0",
					"friend": "0",
					"password": "",
					"click_1": "0",
					"click_2": "0",
					"click_3": "0",
					"click_4": "0",
					"click_5": "0",
					"joincost": "20",
					"portion": "3",
					"endtime": "1344237071",
					"resulttime": "1344845443",
					"lastvote": "1344237066",
					"voternum": "1",
					"maxchoice": "0",
					"sex": "0",
					"keyoid": "106",
					"keyoption": "3",
					"totalcost": "60",
					"hasremind": "1",
					"hasexceed": "0",
					"tag": "",
					"message": "",
					"postip": "127.0.0.1",
					"related": "",
					"relatedtime": "0",
					"target_ids": "",
					"hotuser": "",
					"magiccolor": "0",
					"magicpaper": "0",
					"magiccall": "0",
					"option": [
						"12",
						"3"
					],
					"invite": ",7",
					"optioncount": [
						"2",
						"1"
					],
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				},
				{
					"quizid": "52",
					"topicid": "0",
					"uid": "5",
					"username": "summit",
					"subject": "测试优惠券",
					"classid": "0",
					"viewnum": "2",
					"replynum": "0",
					"hot": "0",
					"dateline": "1344236417",
					"pic": "",
					"picflag": "0",
					"noreply": "0",
					"friend": "0",
					"password": "",
					"click_1": "0",
					"click_2": "0",
					"click_3": "0",
					"click_4": "0",
					"click_5": "0",
					"joincost": "20",
					"portion": "3",
					"endtime": "1344236757",
					"resulttime": "1344844795",
					"lastvote": "1344236423",
					"voternum": "1",
					"maxchoice": "0",
					"sex": "0",
					"keyoid": "102",
					"keyoption": "不能",
					"totalcost": "20",
					"hasremind": "1",
					"hasexceed": "0",
					"tag": "",
					"message": "",
					"postip": "127.0.0.1",
					"related": "",
					"relatedtime": "0",
					"target_ids": "",
					"hotuser": "",
					"magiccolor": "0",
					"magicpaper": "0",
					"magiccall": "0",
					"option": [
						"能",
						"不能"
					],
					"invite": "",
					"optioncount": [
						"1",
						"0"
					],
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				}
			],
			"count": 2,
			"reward": {
				"credit": 1,
				"experience": 0
			}
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>我发起的打赌</h2>
域名/capi/space.php?uid=1&do=quiz&view=me&page=0&perpage=10&dateline=234234324&queryop=up&m_auth=8324dfhg37246dsf
#### 请求参数
	* 固定参数 -- do, 必须为quiz; view, 必须为me
	* 用户id -- uid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* 查询参数 -- view, 必须为hot
	* API密钥 -- m_auth, 由登录后返回
	* 时间点 -- dateline
	* 查询方式 -- queryop, 取值可以是up, down
		* up 代表上拉，取比dateline新的打赌
		* down 代表到底，取紧接着dateline之后的打赌

#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[quizs]，打赌列表， 条目字段如下
			* 打赌id : quizid
			* 发布打赌的用户id : uid
			* 发布打赌的用户名 : username
			* 打赌标题: subject
			* 浏览次数: viewnum
			* 回复次数：replynum
			* 热度: hot
			* 时间: dateline
			* 参与所需金币: joincost
			* 允许最大投注次数: portion
			* 截止时间: endtime
			* 预计公布结果时间: resulttime
			* 最近一次投票时间: lastvote
			* 参与打赌的人数: voternum
			* 答案id: keyoid
			* 答案: keyoption
			* 奖金池: totalcost
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{
		"code": 0,
		"data": {
			"quizs": [
				{
					"quizid": "54",
					"topicid": "0",
					"uid": "5",
					"username": "summit",
					"subject": "测试优惠券",
					"classid": "0",
					"viewnum": "6",
					"replynum": "0",
					"hot": "0",
					"dateline": "1344237052",
					"pic": "",
					"picflag": "0",
					"noreply": "0",
					"friend": "0",
					"password": "",
					"click_1": "0",
					"click_2": "0",
					"click_3": "0",
					"click_4": "0",
					"click_5": "0",
					"joincost": "20",
					"portion": "3",
					"endtime": "1344237071",
					"resulttime": "1344845443",
					"lastvote": "1344237066",
					"voternum": "1",
					"maxchoice": "0",
					"sex": "0",
					"keyoid": "106",
					"keyoption": "3",
					"totalcost": "60",
					"hasremind": "1",
					"hasexceed": "0",
					"tag": "",
					"message": "",
					"postip": "127.0.0.1",
					"related": "",
					"relatedtime": "0",
					"target_ids": "",
					"hotuser": "",
					"magiccolor": "0",
					"magicpaper": "0",
					"magiccall": "0",
					"option": [
						"12",
						"3"
					],
					"invite": ",7",
					"optioncount": [
						"2",
						"1"
					],
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				},
				{
					"quizid": "52",
					"topicid": "0",
					"uid": "5",
					"username": "summit",
					"subject": "测试优惠券",
					"classid": "0",
					"viewnum": "2",
					"replynum": "0",
					"hot": "0",
					"dateline": "1344236417",
					"pic": "",
					"picflag": "0",
					"noreply": "0",
					"friend": "0",
					"password": "",
					"click_1": "0",
					"click_2": "0",
					"click_3": "0",
					"click_4": "0",
					"click_5": "0",
					"joincost": "20",
					"portion": "3",
					"endtime": "1344236757",
					"resulttime": "1344844795",
					"lastvote": "1344236423",
					"voternum": "1",
					"maxchoice": "0",
					"sex": "0",
					"keyoid": "102",
					"keyoption": "不能",
					"totalcost": "20",
					"hasremind": "1",
					"hasexceed": "0",
					"tag": "",
					"message": "",
					"postip": "127.0.0.1",
					"related": "",
					"relatedtime": "0",
					"target_ids": "",
					"hotuser": "",
					"magiccolor": "0",
					"magicpaper": "0",
					"magiccall": "0",
					"option": [
						"能",
						"不能"
					],
					"invite": "",
					"optioncount": [
						"1",
						"0"
					],
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				}
			],
			"count": 2,
			"reward": {
				"credit": 1,
				"experience": 0
			}
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>我参与的打赌</h2>
域名/capi/space.php?uid=1&do=quiz&view=me&page=0&perpage=10&filtrate=join&dateline=234234324&queryop=up&m_auth=8324dfhg37246dsf
#### 攻略
	实际上和我发起的打赌类似，只是增加filtrate=join

#### 请求参数
	* 固定参数 -- do, 必须为quiz; view, 必须为me， filtrate,必须为join
	* 用户id -- uid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* 查询参数 -- view, 必须为hot
	* API密钥 -- m_auth, 由登录后返回
	* 时间点 -- dateline
	* 查询方式 -- queryop, 取值可以是up, down
		* up 代表上拉，取比dateline新的打赌
		* down 代表到底，取紧接着dateline之后的打赌

#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[quizs]，打赌列表， 条目字段如下
			* 打赌id : quizid
			* 发布打赌的用户id : uid
			* 发布打赌的用户名 : username
			* 打赌标题: subject
			* 浏览次数: viewnum
			* 回复次数：replynum
			* 热度: hot
			* 时间: dateline
			* 参与所需金币: joincost
			* 允许最大投注次数: portion
			* 截止时间: endtime
			* 预计公布结果时间: resulttime
			* 最近一次投票时间: lastvote
			* 参与打赌的人数: voternum
			* 答案id: keyoid
			* 答案: keyoption
			* 奖金池: totalcost
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{
		"code": 0,
		"data": {
			"quizs": [
				{
					"quizid": "54",
					"topicid": "0",
					"uid": "5",
					"username": "summit",
					"subject": "测试优惠券",
					"classid": "0",
					"viewnum": "6",
					"replynum": "0",
					"hot": "0",
					"dateline": "1344237052",
					"pic": "",
					"picflag": "0",
					"noreply": "0",
					"friend": "0",
					"password": "",
					"click_1": "0",
					"click_2": "0",
					"click_3": "0",
					"click_4": "0",
					"click_5": "0",
					"joincost": "20",
					"portion": "3",
					"endtime": "1344237071",
					"resulttime": "1344845443",
					"lastvote": "1344237066",
					"voternum": "1",
					"maxchoice": "0",
					"sex": "0",
					"keyoid": "106",
					"keyoption": "3",
					"totalcost": "60",
					"hasremind": "1",
					"hasexceed": "0",
					"tag": "",
					"message": "",
					"postip": "127.0.0.1",
					"related": "",
					"relatedtime": "0",
					"target_ids": "",
					"hotuser": "",
					"magiccolor": "0",
					"magicpaper": "0",
					"magiccall": "0",
					"option": [
						"12",
						"3"
					],
					"invite": ",7",
					"optioncount": [
						"2",
						"1"
					],
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				},
				{
					"quizid": "52",
					"topicid": "0",
					"uid": "5",
					"username": "summit",
					"subject": "测试优惠券",
					"classid": "0",
					"viewnum": "2",
					"replynum": "0",
					"hot": "0",
					"dateline": "1344236417",
					"pic": "",
					"picflag": "0",
					"noreply": "0",
					"friend": "0",
					"password": "",
					"click_1": "0",
					"click_2": "0",
					"click_3": "0",
					"click_4": "0",
					"click_5": "0",
					"joincost": "20",
					"portion": "3",
					"endtime": "1344236757",
					"resulttime": "1344844795",
					"lastvote": "1344236423",
					"voternum": "1",
					"maxchoice": "0",
					"sex": "0",
					"keyoid": "102",
					"keyoption": "不能",
					"totalcost": "20",
					"hasremind": "1",
					"hasexceed": "0",
					"tag": "",
					"message": "",
					"postip": "127.0.0.1",
					"related": "",
					"relatedtime": "0",
					"target_ids": "",
					"hotuser": "",
					"magiccolor": "0",
					"magicpaper": "0",
					"magiccall": "0",
					"option": [
						"能",
						"不能"
					],
					"invite": "",
					"optioncount": [
						"1",
						"0"
					],
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				}
			],
			"count": 2,
			"reward": {
				"credit": 1,
				"experience": 0
			}
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)


<h2>已揭晓的打赌</h2>
域名/capi/space.php?uid=1&do=quiz&view=me&page=0&perpage=10&filtrate=expiration&dateline=234234324&queryop=up&m_auth=8324dfhg37246dsf
#### 攻略
	实际上和我发起的打赌类似，只是增加filtrate=expiration

#### 请求参数
	* 固定参数 -- do, 必须为quiz; view, 必须为me， filtrate,必须为join
	* 用户id -- uid
	* 第几页 -- page
	* 每页显示数量  -- perpage
	* 查询参数 -- view, 必须为hot
	* API密钥 -- m_auth, 由登录后返回
	* 时间点 -- dateline
	* 查询方式 -- queryop, 取值可以是up, down
		* up 代表上拉，取比dateline新的打赌
		* down 代表到底，取紧接着dateline之后的打赌

#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[quizs]，打赌列表， 条目字段如下
			* 打赌id : quizid
			* 发布打赌的用户id : uid
			* 发布打赌的用户名 : username
			* 打赌标题: subject
			* 浏览次数: viewnum
			* 回复次数：replynum
			* 热度: hot
			* 时间: dateline
			* 参与所需金币: joincost
			* 允许最大投注次数: portion
			* 截止时间: endtime
			* 预计公布结果时间: resulttime
			* 最近一次投票时间: lastvote
			* 参与打赌的人数: voternum
			* 答案id: keyoid
			* 答案: keyoption
			* 奖金池: totalcost
		* data[count], 返回列表条目数, 便用遍历
#### 样例
	{
		"code": 0,
		"data": {
			"quizs": [
				{
					"quizid": "54",
					"topicid": "0",
					"uid": "5",
					"username": "summit",
					"subject": "测试优惠券",
					"classid": "0",
					"viewnum": "6",
					"replynum": "0",
					"hot": "0",
					"dateline": "1344237052",
					"pic": "",
					"picflag": "0",
					"noreply": "0",
					"friend": "0",
					"password": "",
					"click_1": "0",
					"click_2": "0",
					"click_3": "0",
					"click_4": "0",
					"click_5": "0",
					"joincost": "20",
					"portion": "3",
					"endtime": "1344237071",
					"resulttime": "1344845443",
					"lastvote": "1344237066",
					"voternum": "1",
					"maxchoice": "0",
					"sex": "0",
					"keyoid": "106",
					"keyoption": "3",
					"totalcost": "60",
					"hasremind": "1",
					"hasexceed": "0",
					"tag": "",
					"message": "",
					"postip": "127.0.0.1",
					"related": "",
					"relatedtime": "0",
					"target_ids": "",
					"hotuser": "",
					"magiccolor": "0",
					"magicpaper": "0",
					"magiccall": "0",
					"option": [
						"12",
						"3"
					],
					"invite": ",7",
					"optioncount": [
						"2",
						"1"
					],
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				},
				{
					"quizid": "52",
					"topicid": "0",
					"uid": "5",
					"username": "summit",
					"subject": "测试优惠券",
					"classid": "0",
					"viewnum": "2",
					"replynum": "0",
					"hot": "0",
					"dateline": "1344236417",
					"pic": "",
					"picflag": "0",
					"noreply": "0",
					"friend": "0",
					"password": "",
					"click_1": "0",
					"click_2": "0",
					"click_3": "0",
					"click_4": "0",
					"click_5": "0",
					"joincost": "20",
					"portion": "3",
					"endtime": "1344236757",
					"resulttime": "1344844795",
					"lastvote": "1344236423",
					"voternum": "1",
					"maxchoice": "0",
					"sex": "0",
					"keyoid": "102",
					"keyoption": "不能",
					"totalcost": "20",
					"hasremind": "1",
					"hasexceed": "0",
					"tag": "",
					"message": "",
					"postip": "127.0.0.1",
					"related": "",
					"relatedtime": "0",
					"target_ids": "",
					"hotuser": "",
					"magiccolor": "0",
					"magicpaper": "0",
					"magiccall": "0",
					"option": [
						"能",
						"不能"
					],
					"invite": "",
					"optioncount": [
						"1",
						"0"
					],
					"avatar": "http://localhost:8080/betit/center/data/avatar/000/00/00/05_avatar_small.jpg"
				}
			],
			"count": 2,
			"reward": {
				"credit": 1,
				"experience": 0
			}
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>系统未读信息计数器</h2>
域名/capi/space.php?do=stat&m_auth=e8b7zu%2BuRuir9hvAgj%2BLxbZtCgUKnFTojhHKjm9zc%2ByGzcuj2cUL

#### 请求参数
	* 固定参数 -- do, 必须为stat
	* API密钥 -- m_auth, 由登录后返回

#### 返回字段

	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组,
		* allnotenum: 未读通知数
		* newpn: 新短消息
		* addfriendnum: 好友请求

#### 样例

	{
		"code": 0,
		"data": {
			"allnotenum": 25,
			"newpm": "0",
			"addfriendnum": "0"
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}


[↑返回顶部](#betit)

******************************
<h2>获取注册验证码</h2>
域名/capi/do.php?ac=register&op=seccode
#### 请求参数
	* 操作类型 -- op, 必须为seccode
	
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, rest_success:代表成功, rest_fail:代表失败
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回两个数据
		* data[seccode_auth] -- 返回的验证码key，在注册时需要传入
		* data[seccode] -- 验证码

#### 样例
	{"code":0,"data":{"seccode_auth":"1a6431MIvgvhZZzUPUmCUML%2FtL4rlXrN2R8nL5G3qvta","seccode":"CQ7T"},
	"msg":"数据获取成功","action":"rest_success"}
[↑返回顶部](#betit)

<h2>注册</h2>
/capi/do.php?ac=register&registersubmit=true&username=test4&password=123&password2=123&seccode=cQ7T&m_auth=1a6431MIvgvhZZzUPUmCUML%2FtL4rlXrN2R8nL5G3qvta
#### 请求参数
	* 操作参数 -- registersubmit, 必须为true
	* 用户名 -- username
	* 用户输入的第一次密码 -- password
	* 用户输入的确认密码 -- password2
	* 用户输入的验证码 -- seccode
	* 生成验证码返回的key -- m_auth

#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户
	* 用户空间信息 -- space
		* groupid -- 所在用户组（级别）
		* credit -- 金币(这里代表注册增加的金币)
		* experience -- 经验(这里代表注册增加的经验)
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
	{"code":0,"data":{"space":{"uid":"11","sex":"0","email":"test6@betit.cn","newemail":"","emailcheck":"0",
	"mobile":"","qq":"","msn":"","msnrobot":"","msncstatus":"0","videopic":"","birthyear":"0","birthmonth":"0",
	"birthday":"0","blood":"","marry":"0","birthprovince":"","birthcity":"","resideprovince":"","residecity":"",
	"note":"","spacenote":"","authstr":"","theme":"","nocss":"0","menunum":"0","css":"",
	"privacy":{"view":{"index":"0","friend":"0","wall":"0","feed":"0","mtag":"0","event":"0","doing":"0",
	"blog":"0","quiz":"0","album":"0","share":"0","poll":"0"},"feed":{"doing":1,"blog":1,"quiz":1,"joinquiz":1,
	"upload":1,"share":1,"poll":1,"joinpoll":1,"thread":1,"post":1,"mtag":1,"event":1,"join":1,"friend":1,
	"comment":1,"show":1,"credit":1,"spaceopen":1,"invite":1,"task":1,"profile":1,"click":1}},"friend":"",
	"feedfriend":"","sendmail":"","magicstar":"0","magicexpire":"0","timeoffset":"","weibo":"","groupid":"0",
	"credit":"25","experience":"15","username":"test6","name":"","namestatus":"0","videostatus":"0","domain":"",
	"friendnum":"0","viewnum":"0","notenum":"0","addfriendnum":"0","mtaginvitenum":"0","eventinvitenum":"0",
	"myinvitenum":"0","pokenum":"0","doingnum":"0","blognum":"0","albumnum":"0","threadnum":"0","pollnum":"0",
	"eventnum":"0","sharenum":"0","dateline":"1344414070","updatetime":"0","lastsearch":"0","lastpost":"0",
	"lastlogin":"1344414070","lastsend":"0","attachsize":"0","addsize":"0","addfriend":"0","flag":"0","newpm":"0",
	"avatar":"0","regip":"127.0.0.1","ip":"127000000","mood":"0","quiznum":"0","winnum":"0","lostnum":"0",
	"voternum":"0","self":1,"friends":[],"allnotenum":0},
	"m_auth":"cf7chDvDIcnUVeupGp4utLftIQEP%2B1rP8eGrGWydH3ITmly6DURpvHCvByCJlE0hEus%2F5Ji%2FqVUrfnd3dHn6%2BA"},
	"msg":"注册成功了，进入个人空间","action":"registered"}
[↑返回顶部](#betit)
	
<h2>登录</h2>
域名/capi/do.php?ac=login&username=summit&password=likeyou&loginsubmit=true
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
		* reward -- 操作增加的金币分和经验
			* credit -- 金币
			* experience -- 经验
#### 样例
	{
		"code": {
			"space": {
				"uid": "5",
				"groupid": "11",
				"credit": "2047",
				"experience": "2108",
				"username": "summit",
				"name": "",
				"namestatus": "0",
				"videostatus": "0",
				"domain": "",
				"friendnum": "1",
				"viewnum": "17",
				"notenum": "0",
				"addfriendnum": "0",
				"mtaginvitenum": "0",
				"eventinvitenum": "0",
				"myinvitenum": "0",
				"pokenum": "0",
				"doingnum": "0",
				"blognum": "2",
				"albumnum": "0",
				"threadnum": "0",
				"pollnum": "0",
				"eventnum": "0",
				"sharenum": "0",
				"dateline": "1343789930",
				"updatetime": "1344932295",
				"lastsearch": "1345360391",
				"lastpost": "1344932295",
				"lastlogin": "1345359730",
				"lastsend": "0",
				"attachsize": "0",
				"addsize": "0",
				"addfriend": "0",
				"flag": "0",
				"newpm": "0",
				"avatar": "0",
				"regip": "127.0.0.1",
				"ip": "127000000",
				"mood": "0",
				"quiznum": "10",
				"winnum": "4",
				"lostnum": "1",
				"voternum": "8",
				"reward": {
					"credit": 0,
					"experience": 0
				}
			},
			"m_auth": "b819QOI5fDiDEO7L0DG66A%2FF%2B0bUu3DVzWGp3IQvkHwE%2BWc7p9qfAUwWK7jsI0C4FaXDCSbWNaqeCOlWIRDb"
		},
		"data": [],
		"msg": "登录成功了，现在引导您进入登录前页面 \\1",
		"action": "login_success"
	}
[↑返回顶部](#betit)

<h2>上传图片</h2>
#### 注意:采用POST上传
#### POST样例：
	`<!DOCTYPE HTML>
	<html>
	<head>
	<meta charset="utf-8">
	<title>上传图片</title></head><body>
	<form action="capi/cp.php?ac=upload" method="post" enctype="multipart/form-data">
	<input type="file" name="attach"/><input type="hidden" name="op" value="uploadphoto2" />
	<input type="hidden" name="uid" value="1" />
	<input type="hidden" name="uploadsubmit2"  value="true" />
	<input type="hidden" name="m_auth"  value="af9cCEMpQlfFTifZltugadwhGAXL%2Ba%2BCor8voR9jZyBh60v4xFryq2i" />
	<input type="hidden" name="topicid"  value="0" />
	<input type="hidden" name="ac"  value="upload" />
	<input type="hidden" name="albumid" value="0" />
	<input type="submit"  name="submit"  value="提交"/>
	</form>
	</body>
	</html>`
#### 请求参数
	* 上传文件 -- attach
	* 操作类型(固定搭配) -- op: uploadphoto2, uploadsubmit2:true, topicid:0. albumid:0, ac:upload
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户
	* 上传用户id -- uid
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回一个数据
		* data[pic] -- 上传成功的图片内容，具体条目如下:
			* 上传的用户id -- uid
			* 上传的用户名 -- username
			* 上传时间 -- dateline
			* 上传文件名 -- filename
			* 图片标题 -- title, 默认为空
			* 图片类型 -- type
			* 图片大小 -- size
			* 图片服务端文件名 -- filepath
			* 是否生成了缩略图 -- thumb, 1代表生成了，0代表没有
			* 是否放在远端图像服务器 -- remote
			* 图片id -- picid, <em>重要</em>，当发布打赌时需要关联
			* 图片服务端路径 -- pic
#### 样例
	{"code":0,"data":{"pic":{"albumid":0,"uid":"1","username":"test6","dateline":"1344415852","filename":"qq提醒.png","postip":"127.0.0.1","title":"",
	"type":"image\/png","size":165056,"filepath":"1_1344415852h77H.png","thumb":1,"remote":0,"topicid":0,"picid":80,"pic":"attachment\/1_1344415852h77H.png.thumb.jpg"}},
	"msg":"进行的操作完成了","action":"do_success"}
[↑返回顶部](#betit)

<h2>发布打赌</h2>
域名/capi/cp.php?ac=quiz&quizsubmit=true&subject=我的打赌&options[1]=A赢&options[2]=B输&pics[1]=81&pics[2]=79&joincost=20&portion=3
&endtime=12324324235&resulttime=4343234&friend=0&m_auth=af9cCEMpQlfFT

#### 请求参数
	* 操作类型(固定搭配) -- quizsubmit: true
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户
	* 打赌的标题 -- subject
	* A选项的描述 -- options[1]
	* B选项的描述 -- options[2]
	* A选项的图片id -- pics[1]
	* B选项的图片id -- pics[2]
	* 每一份投注需要的金币数 -- joincost
	* 每个用户可允许的最大投注次数 -- portion
	* 打赌投注截止时间 -- endtime
	* 打赌预计公布答案时间 -- resulttime
	* 是否全站公开 -- frined , 默认0全站公开

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回一个数据
		* data[quiz] -- 发布成功的打赌，具体条目如下:
			* 打赌的标题 -- subject
			* 是否全站公开 -- frined , 默认0全站公开
			* 每一份投注需要的金币数 -- joincost
			* 每个用户可允许的最大投注次数 -- portion
			* 打赌投注截止时间 -- endtime
			* 打赌预计公布答案时间 -- resulttime
			* 打赌id --  quizid
			* 发布的用户id -- uid
			* 发布的用户名 -- username
			* reward -- 操作增加的金币分和经验
				* credit -- 金币
				* experience -- 经验

#### 样例
	{
		"code": 0,
		"data": {
			"quiz": {
				"subject": "我的打赌",
				"classid": 0,
				"friend": 0,
				"password": null,
				"noreply": 0,
				"joincost": 20,
				"portion": 3,
				"endtime": null,
				"resulttime": null,
				"picflag": 0,
				"pic": "",
				"topicid": 0,
				"uid": 5,
				"username": "summit",
				"dateline": "1345361570",
				"quizid": 59,
				"reward": {
					"credit": 0,
					"experience": 0
				}
			}
		},
		"msg": "进行的操作完成了",
		"action": "do_success"
	}
[↑返回顶部](#betit)


<h2>参与打赌</h2>
域名/capi/cp.php?ac=quiz&op=vote&votesubmit=true&quizid=55&option[]=108&m_auth=af9cCEMpQlfFTifZlt
#### 请求参数
	* 操作类型(固定搭配) -- op:vote, votesubmit: true
	* 打赌id --  quizid
	* 投注的选项 -- option[]
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回一个数据
		* data[quiz], 打赌详情，具体内容如下
			* 打赌id -- quizid
			* 发布打赌用户id -- uid
			* 最热用户 -- hotuser
			* 发布时间 -- dateline
			* 投一注所需金币 -- joincost
			* 用户最大投注数 -- portion
			* 截止投注时间 -- endtime
			* 预计公布结果时间 -- resulttime
			* 最近一次投注时间 -- lastvote
			* 当前累计投注 -- voternum
			* 奖金池 -- totalcost
			* 是否已经提醒过 -- hasremind
			* 是否已经超期 -- hasexceed
			* 答案选项id -- keyoid
			* 答案 -- keyoption
			* 选项数组 -- options，具体内容如下：
				* 选项id -- oid
				* 所属竞猜 -- quizid
				* 用户id -- uid
				* 选项 -- option, 文本描述
				* 相片id -- picid
				* 相片路径 -- pic
				* 投注人数 -- votenum
				* 投注占总投注百分比 -- percent
			* reward -- 操作增加的金币分和经验
				* credit -- 金币
				* experience -- 经验
#### 样例
	{
		"code": 0,
		"data": {
			"quiz": {
				"quizid": "59",
				"uid": "5",
				"tag": "",
				"message": "",
				"postip": "127.0.0.1",
				"related": "",
				"relatedtime": "0",
				"target_ids": "",
				"hotuser": "",
				"magiccolor": "0",
				"magicpaper": "0",
				"magiccall": "0",
				"option": "a:2:{i:0;s:4:\"A赢\";i:1;s:4:\"B输\";}",
				"invite": "",
				"topicid": "0",
				"username": "summit",
				"subject": "我的打赌",
				"classid": "0",
				"viewnum": "0",
				"replynum": "0",
				"hot": "0",
				"dateline": "1345361570",
				"pic": "",
				"picflag": "0",
				"noreply": "0",
				"friend": "0",
				"password": "",
				"click_1": "0",
				"click_2": "0",
				"click_3": "0",
				"click_4": "0",
				"click_5": "0",
				"joincost": "20",
				"portion": "3",
				"endtime": "0",
				"resulttime": "0",
				"lastvote": "0",
				"voternum": "0",
				"maxchoice": "0",
				"sex": "0",
				"keyoid": "0",
				"keyoption": "",
				"totalcost": "0",
				"hasremind": "1",
				"hasexceed": "1",
				"options": [
					{
						"oid": "115",
						"quizid": "59",
						"uid": "5",
						"option": "A赢",
						"relatedtime": "1345361570",
						"picid": "81",
						"votenum": "0",
						"pic": "attachment/201208/8/1_13444161795Gzu.png.thumb.jpg"
					},
					{
						"oid": "116",
						"quizid": "59",
						"uid": "5",
						"option": "B输",
						"relatedtime": "1345361570",
						"picid": "79",
						"votenum": "0",
						"pic": "attachment/201208/1/1_1343816747cmwS.png"
					}
				],
				"reward": {
					"credit": "-20",
					"experience": 0
				}
			}
		},
		"msg": "进行的操作完成了",
		"action": "do_success"
	}
[↑返回顶部](#betit)

<h2>公布答案</h2>
域名/capi/cp.php?ac=quiz&op=publickey&quizid=55&keysubmit=true&keyid=107&m_auth=7c44hpLskh17xPRklyuRE%2FK0fAcYbTThZ

#### 请求参数
	* 操作类型(固定搭配) -- op:publickey, keysubmit: true
	* 打赌id --  quizid
	* 答案选项id -- keyid
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回一个数据
		* data[quiz], 打赌详情，具体内容如下
			* 打赌id -- quizid
			* 发布打赌用户id -- uid
			* 最热用户 -- hotuser
			* 发布时间 -- dateline
			* 投一注所需金币 -- joincost
			* 用户最大投注数 -- portion
			* 截止投注时间 -- endtime
			* 预计公布结果时间 -- resulttime
			* 最近一次投注时间 -- lastvote
			* 当前累计投注 -- voternum
			* 奖金池 -- totalcost
			* 是否已经提醒过 -- hasremind
			* 是否已经超期 -- hasexceed
			* 答案选项id -- keyoid
			* 答案 -- keyoption
			* 选项数组 -- options，具体内容如下：
				* 选项id -- oid
				* 所属竞猜 -- quizid
				* 用户id -- uid
				* 选项 -- option, 文本描述
				* 相片id -- picid
				* 相片路径 -- pic
				* 投注人数 -- votenum
				* 投注占总投注百分比 -- percent
#### 样例
	{"code":0,"data":{"quiz":{"quizid":"55","uid":"1","tag":"","message":"","postip":"127.0.0.1","related":"","relatedtime":"0","target_ids":"","hotuser":"",
	"magiccolor":"0","magicpaper":"0","magiccall":"0","option":"a:2:{i:0;s:4:\"A赢\";i:1;s:4:\"B输\";}","invite":"","topicid":"0","username":"admin",
	"subject":"我的打赌","classid":"0","viewnum":"1","replynum":"2","hot":"0","dateline":"1344417374","pic":"","picflag":"0","noreply":"0","friend":"0",
	"password":"","click_1":"0","click_2":"0","click_3":"0","click_4":"0","click_5":"0","joincost":"20","portion":"3","endtime":"0","resulttime":"0",
	"lastvote":"1344418287","voternum":"1","maxchoice":"0","sex":"0","keyoid":"0","keyoption":"","totalcost":"20","hasremind":"1","hasexceed":"1",
	"options":[{"oid":"107","quizid":"55","uid":"1","option":"A赢","relatedtime":"1344417374","picid":"81","votenum":"0",
	"pic":"attachment\/201208\/8\/1_13444161795Gzu.png.thumb.jpg"},{"oid":"108","quizid":"55","uid":"1","option":"B输","relatedtime":"1344417374","picid":"79",
	"votenum":"1","pic":"attachment\/201208\/1\/1_1343816747cmwS.png"}]}},"msg":"进行的操作完成了","action":"do_success"}
[↑返回顶部](#betit)

<h2>分享打赌</h2>
域名/capi/cp.php?ac=share&type=quiz&id=54&sharesubmit=true&general=好打赌&m_auth=7c44hpLskh17xPRklyuRE%2FK0fAcYbT
#### 请求参数
	* 操作类型(固定搭配) -- type:quiz, sharesubmit: true
	* 打赌id --  id
	* 分享说明 -- general
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 返回操作完成增加的金币和经验
		* credit -- 金币
		* experience -- 经验
#### 样例
	{
		"code": 0,
		"data": {
			"credit": 2,
			"experience": 2
		},
		"msg": "进行的操作完成了",
		"action": "do_success"
	}
[↑返回顶部](#betit)

<h2>邀请好友参与打赌</h2>
域名/capi/cp.php?ac=quiz&op=invite&quizid=54&uid=5&group=-1&ids[]=7&invitesubmit=true&m_auth=7c44hpLskh17xPRkly

#### 请求参数
	* 操作类型(固定搭配) -- op:invite, sharesubmit: true, group=-1
	* 打赌id --  quizid
	* 用户id -- uid
	* 邀请列表 -- ids[], 传邀请用户的用户id
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录

#### 样例
	{"code":0,"data":[],"msg":"\u8fdb\u884c\u7684\u64cd\u4f5c\u5b8c\u6210\u4e86","action":"do_success"}
[↑返回顶部](#betit)

<h2>撰写评论</h2>
域名/capi/cp.php?ac=comment&commentsubmit=true&message=i like you -- summit&idtype=quizid&id=55&m_auth=af9cCEMpQlfFT

#### 请求参数
	* 操作类型(固定搭配) -- commentsubmit: true
	* 指示id代表的类型 -- idtype, quizid代表打赌，uid代表空间, sid代表分享
	* 评论关联的id -- id
	* 评论内容 -- message
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 返回操作完成增加的金币和经验
		* credit -- 金币
		* experience -- 经验
#### 样例
	{
		"code": 0,
		"data": {
			"credit": 1,
			"experience": 1
		},
		"msg": "数据获取成功",
		"action": "rest_success"
	}
[↑返回顶部](#betit)

<h2>发布私信</h2>
域名/capi/cp.php?ac=pm&op=send&touid=0&pmid=0&username=test6&message=你好!summit&pmsubmit=true&m_auth=af9cCEMpQlfFTifZltugadwh

#### 请求参数
	* 操作类型(固定搭配) -- op: send, touid: 0, pmid: 0, pmsubmit: true
	* 接收方的用户名 -- username
	* 私信内容 -- message
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录

#### 样例
	{"code":0,"data":[],"msg":"进行的操作完成了","action":"do_success"}
[↑返回顶部](#betit)

<h2>更改头像</h2>
#### 注意:采用POST上传
#### POST样例：
	`<!DOCTYPE HTML>
	<html>
	<head>
	<meta charset="utf-8">
	<title>上传头像</title></head><body>
	<form action="capi/cp.php?ac=avatar" method="post" enctype="multipart/form-data">
	<input type="file" name="Filedata"/><input type="submit"  name="submit"  value="提交"/>
	<input type="hidden" name="m_auth" value="af9cCEMpQlfFTifZltugadwhGAXL%2Ba%2BCor8voR9jZyBh60v4xFryq2ibMM1tNHXaHYweU%2B8hsBHobKzgHFJs" />
	<input type="hidden" name="ac" value="avatar" />
	<input type="hidden" name="avatarsubmit" id="avatarsubmit" value="true" />
	</form></body>`

#### 请求参数
	* 上传头像 -- Filedata
	* 操作类型(固定搭配) -- ac:avatar, avatarsubmit:true
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户
	
#### 返回字段
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 本操作返回三个数据
		* data[url], 返回头像的链接
			* big -- 大头像URL
			* middle -- 中头像URL
			* small -- 小头像URL
		* data[reward], 返回操作增加的金币和信用
			* credit -- 增加的金币量
			* experience -- 增加的信用
		* date[dateline]: 操作更新的时间

#### 样例
	{"code":0,"data":{"url":{"big":"http:\/\/localhost:8080\/betit\/center\/data\/avatar\/000\/00\/00\/00_avatar_big.jpg","middle":"http:\/\/localhost:8080\/betit\/center\/data\/avatar\/000\/00\/00\/00_avatar_middle.jpg","small":"http:\/\/localhost:8080\/betit\/center\/data\/avatar\/000\/00\/00\/00_avatar_small.jpg"},"msg":"",
	"reward":{"credit":0,"experience":0},"dateline":"1344421976"},"msg":"\u8fdb\u884c\u7684\u64cd\u4f5c\u5b8c\u6210\u4e86","action":"do_success"}
[↑返回顶部](#betit)

<h2>更改昵称</h2>
域名/capi/cp.php?ac=profile&op=name&name=summit&m_auth=af9cCEMpQlfFTifZltu

#### 请求参数
	* 操作类型(固定搭配) -- op: name
	* 昵称 -- name
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 返回操作完成增加的金币和经验
		* credit -- 金币
		* experience -- 经验
#### 样例
	{
		"code": 0,
		"data": {
			"credit": 0,
			"experience": 0
		},
		"msg": "进行的操作完成了",
		"action": "do_success"
	}
[↑返回顶部](#betit)

<h2>编写心情</h2>
域名/capi/cp.php?ac=doing&addsubmit=true&spacenote=true&message=你好!summit&m_auth=af9cCEMpQlfFTifZ

#### 请求参数
	* 操作类型(固定搭配) -- addsubmit: true, spacenote:true
	* 心情内容 -- message
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 返回操作完成增加的金币和经验
		* credit -- 金币
		* experience -- 经验
#### 样例
	{
		"code": 0,
		"data": {
			"credit": 3,
			"experience": 3
		},
		"msg": "进行的操作完成了",
		"action": "do_success"
	}
[↑返回顶部](#betit)

<h2>邀请好友</h2>
域名/capi/cp.php?ac=invite&emailinvite=true&email=summit_mail@qq.com&saymsg=来betit包赚没赔&m_auth=7c44hpLskh17xPRklyu

#### 请求参数
	* 操作类型(固定搭配) --emailinvite: true
	* 好友的邮件: email, 以逗号分隔
	* 对好友说的话: saymsg
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户
	
#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录
	* 结果 -- data, json数组, 返回操作完成增加的金币和经验
		* credit -- 金币
		* experience -- 经验
#### 样例
	{
		"code": 0,
		"data": {
			"credit": 0,
			"experience": 0
		},
		"msg": "邮件已经送出，您的好友可能需要几分钟后才能收到邮件",
		"action": "send_result_1"
	}
[↑返回顶部](#betit)

<h2>退出</h2>
域名/capi/cp.php?ac=common&op=logout&m_auth=7c44hpLskh17xPRklyu

#### 请求参数
	* 操作类型（固定搭配） -- ac:common , op:logout
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, login_success:代表登录成功
	* 错误信息 -- msg, 详细参见附录

#### 样例
	{
  	  "code": 0,
	    "data": [],
	    "msg": "你已经安全退出了\\1",
	    "action": "security_exit"
	}
	
[↑返回顶部](#betit)

<h2>单向加好友</h2>
域名/capi/cp.php?ac=friend&op=add&uid=7&gid=0&addsubmit=true&note=想认识你&m_auth=c8202FOb80TMCC8F

#### 请求参数
	* 操作类型（固定搭配） -- ac:friend , op:add, addsubmit=true
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户
	* 加为好友的用户id -- uid
	* 发送请求的消息 -- note
	* 好友组别 -- gid
		* 0 -- 其他
		* 1 -- 通过本站认识
		* 2 -- 通过活动认识
		* 3 -- 通过朋友认识
		* 4 -- 亲人
		* 5 -- 同事
		* 6 -- 同学
		* 7 -- 不认识

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, request_has_been_sent:代表成功
	* 错误信息 -- msg, 详细参见附录

#### 样例
	{
		"code": 0,
		"data": [],
		"msg": "好友请求已经发送，请等待对方验证中",
		"action": "request_has_been_sent"
	}
[↑返回顶部](#betit)

<h2>通过好友验证</h2>
域名/capi/cp.php?ac=friend&op=add&uid=13&gid=0&add2submit=true&m_auth=c8202FOb80TMCC8F

#### 请求参数
	* 操作类型（固定搭配） -- ac:friend , op:add, add2submit=true
	* API密钥 -- m_auth, 每次调用接口，需要提供此key以验证用户
	* 加为好友的用户id -- uid
	* 好友组别 -- gid
		* 0 -- 其他
		* 1 -- 通过本站认识
		* 2 -- 通过活动认识
		* 3 -- 通过朋友认识
		* 4 -- 亲人
		* 5 -- 同事
		* 6 -- 同学
		* 7 -- 不认识

#### 返回参数
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 错误类型 -- action, request_has_been_sent:代表成功
	* 错误信息 -- msg, 详细参见附录

#### 样例
	{
		"code": 0,
		"data": [
			"test8"
		],
		"msg": "您和 晓林 成为好友了",
		"action": "friends_add"
	}
[↑返回顶部](#betit)

<h2>微博登陆</h2>
域名/capi/connect.php?sinauid=2343336&username=2236&name=you&oauth_token=23432432&oauth_token_secret=32423423&avatar=http://www.baidu.com/img/baidu_sylogo1.gif

#### 请求参数
	* sinauid - 新浪用户id
	* username - 对应新浪API：[http://open.weibo.com/wiki/2/users/show](http://open.weibo.com/wiki/2/users/show) users/show 返回结果的idstr
	* name  - 对应新浪API：[http://open.weibo.com/wiki/2/users/show](http://open.weibo.com/wiki/2/users/show) users/show 返回结果的name
	* oauth_token - 对应新浪OAuth2.0调用后返回的$_SESSION[last_key][oauth_token]
	* oauth_token_secret - 对应新浪OAuth2.0调用后返回的$_SESSION[last_key][oauth_token_secret]
	* avatar - 对应新浪API：[http://open.weibo.com/wiki/2/users/show](http://open.weibo.com/wiki/2/users/show) users/show 返回结果的avatar_large

### 返回结果
	* 错误码 -- code, 0:代表成功， 1:代表失败
	* 结果 -- data, json数组, 返回操作完成增加的金币和经验
		* space -- 用户信息
		* m_auth -- 每次调用接口，需要提供此key以验证用户

#### 样例
	{
    	"code": 0,
	    "data": {
	        "space": {
	            "uid": "27",
	            "sex": "0",
	            "email": "sina_2236@betit.cn",
	            "newemail": "",
	            "emailcheck": "0",
	            "mobile": "",
	            "qq": "",
	            "msn": "",
	            "msnrobot": "",
	            "msncstatus": "0",
	            "videopic": "",
	            "birthyear": "0",
	            "birthmonth": "0",
	            "birthday": "0",
	            "blood": "",
	            "marry": "0",
	            "birthprovince": "",
	            "birthcity": "",
	            "resideprovince": "",
	            "residecity": "",
	            "note": "",
	            "spacenote": "",
	            "authstr": "",
	            "theme": "",
	            "nocss": "0",
	            "menunum": "0",
	            "css": "",
	            "privacy": {
	                "view": {
	                    "index": "0",
	                    "friend": "0",
	                    "wall": "0",
	                    "feed": "0",
	                    "mtag": "0",
	                    "event": "0",
	                    "doing": "0",
	                    "blog": "0",
	                    "quiz": "0",
	                    "album": "0",
	                    "share": "0",
	                    "poll": "0"
	                },
	                "feed": {
	                    "doing": 1,
	                    "blog": 1,
	                    "quiz": 1,
	                    "joinquiz": 1,
	                    "upload": 1,
	                    "share": 1,
	                    "poll": 1,
	                    "joinpoll": 1,
	                    "thread": 1,
	                    "post": 1,
	                    "mtag": 1,
	                    "event": 1,
	                    "join": 1,
	                    "friend": 1,
	                    "comment": 1,
	                    "show": 1,
	                    "credit": 1,
	                    "spaceopen": 1,
	                    "invite": 1,
	                    "task": 1,
	                    "profile": 1,
	                    "click": 1
	                }
	            },
	            "friend": "",
	            "feedfriend": "",
	            "sendmail": "",
	            "magicstar": "0",
	            "magicexpire": "0",
	            "timeoffset": "",
	            "weibo": "",
	            "groupid": "5",
	            "credit": "40",
	            "experience": "30",
	            "username": "sina_2236",
	            "name": "you",
	            "namestatus": "1",
	            "videostatus": "0",
	            "domain": "",
	            "friendnum": "0",
	            "viewnum": "0",
	            "notenum": "0",
	            "addfriendnum": "0",
	            "mtaginvitenum": "0",
	            "eventinvitenum": "0",
	            "myinvitenum": "0",
	            "pokenum": "0",
	            "doingnum": "0",
	            "blognum": "0",
	            "albumnum": "0",
	            "threadnum": "0",
	            "pollnum": "0",
	            "eventnum": "0",
	            "sharenum": "0",
	            "dateline": "1348924152",
	            "updatetime": "1348924152",
	            "lastsearch": "0",
	            "lastpost": "0",
	            "lastlogin": "1348924919",
	            "lastsend": "0",
	            "attachsize": "0",
	            "addsize": "0",
	            "addfriend": "0",
	            "flag": "0",
	            "newpm": "0",
	            "avatar": "1",
	            "regip": "127.0.0.1",
	            "ip": "127000000",
	            "mood": "0",
	            "quiznum": "0",
	            "winnum": "0",
	            "lostnum": "0",
	            "voternum": "0",
	            "self": 1,
	            "friends": [],
	            "allnotenum": 0
	        },
	        "m_auth": "8756EDCHNPM%2FY3vbGc1QPbbi40FclNI%2FbXA99nxOW3bw5AQukNz7jmnQ4PctneOU2Tucv0rJr%2FMn4adzc6Hp%2Fg"
	    },
	    "msg": "登录成功了，现在引导您进入登录前页面 \\1",
	    "action": "login_success"
	}
[↑返回顶部](#betit)