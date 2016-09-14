title: one post~
author: azlar
date: 2016-09-06 21:43:54
tags: ['test', 'zxc']
---

# 旺旺星球 API.v1 C 端

## 通用说明部分
### 1. URL
* a. 说明

	1. url = 主域名 + 相对域名
	2. api 中列出的域名均为相对域名，实际使用中可根据环境自由切换
	3. **接受参数方式为 post 或 get 均可**
	4. 某些**单一参数**的方式，如 [1.1 获取验证码](#toc_7) 的域名可以为，无需指出具体参数名字
	
			http://api.test.com/v1/c/user/1 (Get)
			http://api.test.com/v1/c/user/ (Post	{"id" = 1})

* b. 测试环境

	1. 主域名：http://123.56.154.187:8080/
		
* c. prod
	
	1. 主域名：http://api.dogplanet.cn


### 2. 验证规则
* 说明

* 验证方式


### 3. 返回码
### 4. [更新说明](#toc_29)

## 1.	登录注册部分

### 1.1	验证码通用接口

* url:

		/v1/c/user/get-code/
		
* params:	

		1. phone	（Get or Post）
		2. type	1	注册（默认）	2	找回密码

* response:
	
		1. ret: 1001	已发送		0	发送失败（已注册）
		2. msg:	成功（错误）提示


### 1.2	注册

* url:

		/v1/c/user/reg/
		
* params:
	
		1. phone
		2. code	验证码
		3. name
		4. password

* response:

		1. ret: 1001	成功		0	失败
		2. user => [
				id	=> 1,
				token => '58b9bc86ee11099db8fe449b05ed05ff',
				phone	=>	18600999999,
				name	=>	'azlar',
				mail	=>	'',
				birthday	=>	'0000-00-00',
				avatar	=>	'@img-url'
			] 

### 1.3	登录
* url:

		/v1/c/user/login/
	
* params:

		1. phone
		2. password

* response:

		1. ret: 1001	成功		0	失败
		2. user => [
				id	=> 1,
				token => '58b9bc86ee11099db8fe449b05ed05ff',
				phone	=>	18600999999,
				name	=>	'azlar',
				mail	=>	'',
				birthday	=>	'0000-00-00',
				avatar	=>	'@img-url'
			] 

### 1.4	找回密码
* 说明
	
		1. 使用之前先调用验证码接口，之后直接传递数据保存

* url:

		/v1/c/user/find
		
* params:
	
		1. phone
		2. code
		3. password

* response:
		
		1. ret: 1001	成功		0	失败
		2. user => [
				id	=> 1
				phone	=>	18600999999
				name	=>	'azlar'
				mail	=>	''
				birthday	=>	'0000-00-00'
				avatar	=>	'@img-url'
			]
			
			
### 1.5 获取用户信息
* 说明

		1. 仅限已登录用户

* url:

		/v1/c/user/
		
* params:
	
		1. id	用户 id
		2. tk	用户的 token

* response:
		
		1. ret: 1001	成功		0	失败（session 过期或不存在）
		2. user => [
				id	=> 1,
				token => '58b9bc86ee11099db8fe449b05ed05ff',
				phone	=>	18600999999,
				name	=>	'azlar',
				mail	=>	'',
				birthday	=>	'0000-00-00',
				avatar	=>	'@img-url'
			]
			

### 1.6 注销
* 说明
	
	1. 销毁 session

* url:

		/v1/c/user/logout/
		
* params:
	
		1. id	用户 id

* response:
		
		1. ret: 1001	成功		0	失败（未登录活不存在）



## 2.	首页搜索
* url:

		/v1/c/index/search/
		
* params:
	
		1. keyword
		2. type	'0'	'1'	'2'		(0：综合，1：当地达人，2：热门产品)

* response:

		1. ret:	1001	成功			0	无数据
		2. experts	=>	[
			[
				'id'	=> 124,
				'name'	=>	'陈成',
				'stars' => 5,		//星级
				'avatar'	=>	'@img-url',
				'features'	=>	['打酱油', '吃饭'],
				'services'	=>	[		//10: 全天可下单	20: 半天可下单	30: 不可下单
					'2015-09-19' => 30
					'2015-09-20' => 30
					'2015-09-21' => 30
					'2015-09-22' => 30
					'2015-09-23' => 20
					'2015-09-24' => 30
					'2015-09-25' => 30
				]
				'introduce'	=> 'why so serious',

			],
			[
				'id'	=> 124,
				'name'	=>	'陈成',
				'stars' => 5,		//星级
				'avatar'	=>	'@img-url',
				'features'	=>	['打酱油', '吃饭'],
				'services'	=>	[		//10: 全天可下单	20: 半天可下单	30: 不可下单
					'2015-09-19' => 30
					'2015-09-20' => 30
					'2015-09-21' => 30
					'2015-09-22' => 30
					'2015-09-23' => 20
					'2015-09-24' => 30
					'2015-09-25' => 30
					'2015-09-26' => 30
			]
		]
		
		3. products	=>	[
			[
				'id'	=> 100657,
				'name'	=>	'珊瑚高级海景（大/双）',
				'thumb'	=> '@img-url',
				'features'	=>	['采光充足', '享有碧绿葱翠的园林视野', '65 平米'],
				'price'	=>	12345,
				'introduce' => '环境幽雅美丽',
				'experts'	=> [
					[
						'id'	=> 124,
						'name'	=>	'陈成',
						'stars' => 5,		//星级
						'avatar'	=>	'@img-url',
						'features'	=>	['打酱油', '吃饭'],
						'services'	=>	[		//10: 全天可下单	20: 半天可下单	30: 不可下单
							'2015-09-19' => 30
							'2015-09-20' => 30
							'2015-09-21' => 30
							'2015-09-22' => 30
							'2015-09-23' => 20
							'2015-09-24' => 30
							'2015-09-25' => 30
							'2015-09-26' => 30
					],
					[
						'id'	=> 124,
						'name'	=>	'陈成',
						'stars' => 5,		//星级
						'avatar'	=>	'@img-url',
						'features'	=>	['打酱油', '吃饭'],
						'services'	=>	[		//10: 全天可下单	20: 半天可下单	30: 不可下单
							'2015-09-19' => 30
							'2015-09-20' => 30
							'2015-09-21' => 30
							'2015-09-22' => 30
							'2015-09-23' => 20
							'2015-09-24' => 30
							'2015-09-25' => 30
							'2015-09-26' => 30
					]
				]
			],
			
			[
				'id'	=> 100657,
				'name'	=>	'珊瑚高级海景（大/双）',
				'thumb'	=> '@img-url',
				'features'	=>	['采光充足', '享有碧绿葱翠的园林视野', '65 平米'],
				'price'	=>	12345,
				'introduce' => '环境幽雅而美丽',
				'experts'	=> [],
				]			
			],
		]

* sample
	
	```json
	url:	http://api.dogplanet.test/v1/c/index/search/
	
	params:	{"keyword": "夜潜"， "type": 0}
	
	response:
	{
	    "ret": 1001,
	    "products": [
	        {
	            "id": 10133,
	            "name": "夜潜",
	            "thumb": "",
	            "features": [
	                "专业教练",
	                "昼伏夜出的水下生物"
	            ],
	            "price": 680,
	            "introduce": "<p><span style=\";font-family:宋体;font-size:16px\">潜水时间为</span><span style=\";font-family:宋体;font-size:16px\">30分钟</span><span style=\";font-family:宋体;font-size:16px\">左右，夜间正常情况下开放</span><span style=\";font-family:宋体;font-size:16px\">时间为18:00-22:00，</span><span style=\"font-family: 宋体;\">在漆黑的水中顺着潜水灯的指引缓缓前行，潜入漆黑的海中并没有你</span><span style=\"font-family: 宋体;\">想像得那么恐怖，相反，它会带给你一种别样的新奇感受，收费680</span><span style=\"font-family: 宋体;\">元/位</span></p><p><br/></p>",
	            "experts": [
	                {
	                    "id": 5,
	                    "name": "酱油",
	                    "stars": 0,
	                    "avatar": "",
	                    "introduce": "",
	                    "features": [],
	                    "services": {
	                        "2015-09-19": 30,
	                        "2015-09-20": 30,
	                        "2015-09-21": 30,
	                        "2015-09-22": 30,
	                        "2015-09-23": 30,
	                        "2015-09-24": 30,
	                        "2015-09-25": 30,
	                        "2015-09-26": 30
	                    }
	                },
	                {
	                    "id": 6,
	                    "name": "陈成",
	                    "stars": 0,
	                    "avatar": "",
	                    "introduce": "这个人很吊",
	                    "features": [],
	                    "services": {
	                        "2015-09-19": 30,
	                        "2015-09-20": 30,
	                        "2015-09-21": 30,
	                        "2015-09-22": 30,
	                        "2015-09-23": 10,
	                        "2015-09-24": 30,
	                        "2015-09-25": 30,
	                        "2015-09-26": 30
	                    }
	                },
	                {
	                    "id": 10,
	                    "name": "who",
	                    "stars": 0,
	                    "avatar": "",
	                    "introduce": "",
	                    "features": [],
	                    "services": {
	                        "2015-09-19": 30,
	                        "2015-09-20": 30,
	                        "2015-09-21": 30,
	                        "2015-09-22": 30,
	                        "2015-09-23": 30,
	                        "2015-09-24": 30,
	                        "2015-09-25": 30,
	                        "2015-09-26": 30
	                    }
	                },
	                {
	                    "id": 11,
	                    "name": "who",
	                    "stars": 0,
	                    "avatar": "",
	                    "introduce": "",
	                    "features": [],
	                    "services": {
	                        "2015-09-19": 30,
	                        "2015-09-20": 30,
	                        "2015-09-21": 30,
	                        "2015-09-22": 30,
	                        "2015-09-23": 30,
	                        "2015-09-24": 30,
	                        "2015-09-25": 30,
	                        "2015-09-26": 30
	                    }
	                }
	            ]
	        },
	        {
	            "id": 10102,
	            "name": "夜潜",
	            "thumb": "",
	            "features": [
	                "昼伏夜出的水下生物",
	                "专业潜水导游",
	                "别样感受"
	            ],
	            "price": 0,
	            "introduce": "",
	            "experts": []
	        }
	    ]
	}
	
	```	


## 3. 搜索列表页
### 3.1 搜索列表头部请求
* url:

		/v1/c/list/head/
		
* params:

		1. type		[0 => '产品', 1 => '达人']	（Get or Post）

* response:

		1. ret:	1001	成功	0	失败
		2. search	=>	[
			"searchType"	=>	[
				['id' => 1, 'name' => '潜水'],
				['id' => 2, 'name' => '海岛'],
				['id' => 3, 'name' => '蜜月'],
				//...
			],
			"sex"	=>	[['id' => 1, 'name' => '男'], ['id' => 2, 'name' => '女']]，
			"peopleNum" => [
				['id' => 1, 'name' => '1人'],
				['id' => 2, 'name' => '2人'],
				['id' => 3, 'name' => '3人'],
				['id' => 4, 'name' => '4人'],
				['id' => 5, 'name' => '5人'],
				['id' => 6, 'name' => '6人'],
				['id' => 7, 'name' => '6人以上'],
        	]
		]
* sample:
		
	```json
	url:	http://api.dogplanet.test/v1/c/list/head/0
	
	params:	{"keyword": "夜潜"， "type": 0}
	
	response:
	{
	    "ret": 0,
	    "search": {
	        "searchType": [
	            {
	                "id": 7,
	                "name": "潜水"
	            },
	            {
	                "id": 8,
	                "name": "冲浪"
	            },
	            {
	                "id": 9,
	                "name": "摄影"
	            }
	        ],
	        "sex": [
	            {
	                "id": 1,
	                "name": "男"
	            },
	            {
	                "id": 2,
	                "name": "女"
	            }
	        ],
	        "peopleNum": [
	            {
	                "id": 1,
	                "name": "1人"
	            },
	            {
	                "id": 2,
	                "name": "2人"
	            },
	            {
	                "id": 3,
	                "name": "3人"
	            },
	            {
	                "id": 4,
	                "name": "4人"
	            },
	            {
	                "id": 5,
	                "name": "5人"
	            },
	            {
	                "id": 6,
	                "name": "6人"
	            },
	            {
	                "id": 7,
	                "name": "6人以上"
	            }
	        ]
	    }
	}
    
    ```


### 3.2 列表页数据请求
* url:
	
		/v1/c/list/search/
		
* params:
	- public
	
			1. keyword
			2. type			[0 => '产品', 1 => '达人']
			3. page			*optional*: 0
			4. pageSize		*optional*: 10
	
	- 产品
		
			1. searchType	*optional*: 0 (所有)
			2. date			*optional*: 日期，如 '2015-09-19'，不填即所有

	- 达人

			1. searchType	*optional*: 0 (所有)
			2. date			*optional*: 日期，如 '2015-09-19'	//0 或不填即所有 
			3. sex			*optional*: 性别 		//[0 => '所有', 1 => '男', 2 => '女']
			4. peopleNum	*optional*: 人数	//0 或不填即所有 
* response:
	- 产品
			
			1. ret:	1001	成功	0	无数据
			2. products	=>	[
				[
					'id'	=> 100657,
					'name'	=>	'珊瑚高级海景（大/双）',
					'thumb'	=> '@img-url',
					'features'	=>	['采光充足', '享有碧绿葱翠的园林视野', '65 平米'],
					'price'	=>	12345,
					'introduce' => '环境幽雅美丽',
					'experts'	=> [
					[
						'id'	=> 124,
						'name'	=>	'陈成',
						'stars' => 5,		//星级
						'avatar'	=>	'@img-url',
						'features'	=>	['打酱油', '吃饭'],
						'services'	=>	[		//10: 全天可下单	20: 半天可下单	30: 不可下单
							'2015-09-19' => 30
							'2015-09-20' => 30
							'2015-09-21' => 30
							'2015-09-22' => 30
							'2015-09-23' => 20
							'2015-09-24' => 30
							'2015-09-25' => 30
							'2015-09-26' => 30
					],
					[
						'id'	=> 124,
						'name'	=>	'陈成',
						'stars' => 5,		//星级
						'avatar'	=>	'@img-url',
						'features'	=>	['打酱油', '吃饭'],
						'services'	=>	[		//10: 全天可下单	20: 半天可下单	30: 不可下单
							'2015-09-19' => 30
							'2015-09-20' => 30
							'2015-09-21' => 30
							'2015-09-22' => 30
							'2015-09-23' => 20
							'2015-09-24' => 30
							'2015-09-25' => 30
							'2015-09-26' => 30
					]
				]
			],
			
			[
				'id'	=> 100657,
				'name'	=>	'珊瑚高级海景（大/双）',
				'thumb'	=> '@img-url',
				'features'	=>	['采光充足', '享有碧绿葱翠的园林视野', '65 平米'],
				'price'	=>	12345,
				'introduce' => '环境幽雅而美丽',
				'experts'	=> [],
				]			
			],

				
				]
		
	- 达人

			1. ret:	1001	成功	0	无数据
			2. experts	=>	[
				[
					'id'	=> 124,
					'name'	=>	'陈成',
					'stars' => 5,		//星级
					'avatar'	=>	'@img-url',
					'features'	=>	['打酱油', '吃饭'],
					'services'	=>	[		//10: 全天可下单	20: 半天可下单	30: 不可下单
						'2015-09-19' => 30
						'2015-09-20' => 30
						'2015-09-21' => 30
						'2015-09-22' => 30
						'2015-09-23' => 20
						'2015-09-24' => 30
						'2015-09-25' => 30
					]
					'introduce'	=> 'why so serious',
	
				],
				[
					'id'	=> 5,
					'name'	=>	'陈成',
					'stars' => 5,		//星级
					'avatar'	=>	'@img-url',
					'features'	=>	['打酱油', '吃饭'],
					'services'	=>	[		//10: 全天可下单	20: 半天可下单	30: 不可下单
						'2015-09-19' => 30
						'2015-09-20' => 30
						'2015-09-21' => 30
						'2015-09-22' => 30
						'2015-09-23' => 20
						'2015-09-24' => 30
						'2015-09-25' => 30
					]
					'introduce'	=> 'why so serious',
	
				],
			]
* sample:
	- 达人
		
		```json
		url:	http://api.dogplanet.test/v1/c/list/search/
	
		params:	{"keyword": "潜水"， "type": 1, "searchType": 3, "date": 2015-09-20, "sex": 1, "peopleNum": 5}
		
		response:
		{
		    "ret": 1001,
		    "experts": [
		        {
		            "id": 6,
		            "name": "陈成",
		            "stars": 0,
		            "avatar": "",
		            "introduce": "这个人很吊",
		            "features": [
		                "潜水"
		            ],
		            "services": {
		                "2015-09-20": 30,
		                "2015-09-21": 30,
		                "2015-09-22": 30,
		                "2015-09-23": 10,
		                "2015-09-24": 30,
		                "2015-09-25": 30,
		                "2015-09-26": 30,
		                "2015-09-27": 30
		            }
		        }
		    ]
		}
		
		```
	- 产品
			
		```json
		url:	http://api.dogplanet.test/v1/c/list/search/
	
		params:	{"keyword": "夜潜"， "type": 0, "searchType": 7}
			
		response:
		{
		    "ret": 1001,
		    "products": [
		        {
		            "id": 10102,
		            "name": "夜潜",
		            "thumb": "",
		            "features": [
		                "昼伏夜出的水下生物",
		                "专业潜水导游",
		                "别样感受"
		            ],
		            "price": 0,
		            "introduce": "",
		            "experts": []
		        },
		        {
		            "id": 10106,
		            "name": "潜水",
		            "thumb": "",
		            "features": [
		                "潜水",
		                "专业陪同指导",
		                "海洋生物"
		            ],
		            "price": 0,
		            "introduce": "",
		            "experts": []
		        },
		        {
		            "id": 10138,
		            "name": "堡礁潜水",
		            "thumb": "",
		            "features": [
		                "一对一陪同",
		                "专业潜水装备"
		            ],
		            "price": 429,
		            "introduce": "<p><span style=\";font-family:宋体;font-size:16px\">堡礁潜水主要以体验潜水为主，在岸边下水，水下有少量珊瑚和热带</span><span style=\"font-family: 宋体;\">鱼群。</span><span style=\"font-family: 宋体;\">报名后更换潜水服，经潜水培训后去堡礁潜水点，背上氧气瓶，带上</span><span style=\"font-family: 宋体;\">潜水镜，由教练一对一陪同完成潜水活动。</span><span style=\"font-family: 宋体;\">深度</span><span style=\"font-family: 宋体;\">约</span><span style=\"font-family: 宋体;\">3-6米，潜水时间</span><span style=\"font-family: 宋体;\">约</span><span style=\"font-family: 宋体;\">30分钟，</span><span style=\"font-family: 宋体;\">&nbsp;7-60岁且身体健康者可参加，儿童需1米2以上以上</span><span style=\"font-family: 宋体;\">可参加，收费429元/位</span></p><p><br/></p>",
		            "experts": [
		                {
		                    "id": 10,
		                    "name": "who",
		                    "stars": 0,
		                    "avatar": "",
		                    "introduce": "",
		                    "features": [],
		                    "services": {
		                        "2015-09-20": 30,
		                        "2015-09-21": 30,
		                        "2015-09-22": 30,
		                        "2015-09-23": 30,
		                        "2015-09-24": 30,
		                        "2015-09-25": 30,
		                        "2015-09-26": 30,
		                        "2015-09-27": 30
		                    }
		                },
		                {
		                    "id": 11,
		                    "name": "who",
		                    "stars": 0,
		                    "avatar": "",
		                    "introduce": "",
		                    "features": [],
		                    "services": {
		                        "2015-09-20": 30,
		                        "2015-09-21": 30,
		                        "2015-09-22": 30,
		                        "2015-09-23": 30,
		                        "2015-09-24": 30,
		                        "2015-09-25": 30,
		                        "2015-09-26": 30,
		                        "2015-09-27": 30
		                    }
		                }
		            ]
		        },
		        {
		            "id": 10140,
		            "name": "VIP潜水",
		            "thumb": "",
		            "features": [
		                "海底景观最完整",
		                "高端潜水体验",
		                "完美邂逅美丽海洋生物"
		            ],
		            "price": 980,
		            "introduce": "<p><span style=\";font-family:宋体;font-size:16px\">VIP潜水区域是蜈支洲海域海底景观保存最为完整的地方，水下各种</span><span style=\"font-family: 宋体;\">珊瑚五彩斑斓，热带鱼群丰富多样</span><span style=\"font-family: 宋体;\">，下潜过程由浅入深</span><span style=\"font-family: 宋体;\">，是欣赏最美</span><span style=\"font-family: 宋体;\">海底世界和体验高端潜水的首选</span><span style=\"font-family: 宋体;\">潜水</span><span style=\"font-family: 宋体;\">深度</span><span style=\"font-family: 宋体;\">约</span><span style=\"font-family: 宋体;\">3-</span><span style=\"font-family: 宋体;\">10米，</span><span style=\"font-family: 宋体;\">间45分钟，全程VIP接待服务，并且赠送一次</span><span style=\"font-family: 宋体;\">性呼吸嘴，浴巾，寄存柜以及蛙鞋,7</span><span style=\"font-family: 宋体;\">-60</span><span style=\"font-family: 宋体;\">岁</span><span style=\"font-family: 宋体;\">且身体健康者可参</span><span style=\"font-family: 宋体;\">加，儿童1米2</span><span style=\"font-family: 宋体;\">以上可以参加。</span><span style=\"font-family: 宋体;\">收费980元/位</span></p><p><br/></p>",
		            "experts": [
		                {
		                    "id": 10,
		                    "name": "who",
		                    "stars": 0,
		                    "avatar": "",
		                    "introduce": "",
		                    "features": [],
		                    "services": {
		                        "2015-09-20": 30,
		                        "2015-09-21": 30,
		                        "2015-09-22": 30,
		                        "2015-09-23": 30,
		                        "2015-09-24": 30,
		                        "2015-09-25": 30,
		                        "2015-09-26": 30,
		                        "2015-09-27": 30
		                    }
		                },
		                {
		                    "id": 11,
		                    "name": "who",
		                    "stars": 0,
		                    "avatar": "",
		                    "introduce": "",
		                    "features": [],
		                    "services": {
		                        "2015-09-20": 30,
		                        "2015-09-21": 30,
		                        "2015-09-22": 30,
		                        "2015-09-23": 30,
		                        "2015-09-24": 30,
		                        "2015-09-25": 30,
		                        "2015-09-26": 30,
		                        "2015-09-27": 30
		                    }
		                }
		            ]
		        },
		        {
		            "id": 10141,
		            "name": "考取潜水证（不含门船票）",
		            "thumb": "",
		            "features": [
		                "一星潜水员课程",
		                "专业教练指导",
		                "快速掌握潜水技巧"
		            ],
		            "price": 3500,
		            "introduce": "<p><span style=\";font-family:宋体;font-size:16px\">此潜水办证是</span><span style=\";font-family:宋体;font-size:16px\">CMAS一星潜水员课程</span><span style=\";font-family:宋体;font-size:16px\">，</span><span style=\";font-family:宋体;font-size:16px\">一星级水肺潜水课程为基础级</span><span style=\"font-family: 宋体;\">潜水课程，其目的为指导潜水初学者具备最低限度之潜水常识与技</span><span style=\"font-family: 宋体;\">巧，以便在领导与监督时，能参加开放水域的潜水活动。</span><span style=\"font-family: 宋体;\">课程约为3至4天，第1天为理论课，讲解潜水方面的知识以及设备</span><span style=\"font-family: 宋体;\">的使用方法；第2天到泳池穿上潜水设备进行实操培训；第3天开始</span><span style=\"font-family: 宋体;\">到海里实操，全程有教练陪同，后期实操时根据客人掌握情况，可自</span><span style=\"font-family: 宋体;\">行练习，教练跟随。收费3500元/位</span></p><p><br/></p>",
		            "experts": [
		                {
		                    "id": 10,
		                    "name": "who",
		                    "stars": 0,
		                    "avatar": "",
		                    "introduce": "",
		                    "features": [],
		                    "services": {
		                        "2015-09-20": 30,
		                        "2015-09-21": 30,
		                        "2015-09-22": 30,
		                        "2015-09-23": 30,
		                        "2015-09-24": 30,
		                        "2015-09-25": 30,
		                        "2015-09-26": 30,
		                        "2015-09-27": 30
		                    }
		                },
		                {
		                    "id": 11,
		                    "name": "who",
		                    "stars": 0,
		                    "avatar": "",
		                    "introduce": "",
		                    "features": [],
		                    "services": {
		                        "2015-09-20": 30,
		                        "2015-09-21": 30,
		                        "2015-09-22": 30,
		                        "2015-09-23": 30,
		                        "2015-09-24": 30,
		                        "2015-09-25": 30,
		                        "2015-09-26": 30,
		                        "2015-09-27": 30
		                    }
		                }
		            ]
		        },
		        {
		            "id": 10142,
		            "name": "考取潜水证（含3次上下岛门船票）",
		            "thumb": "",
		            "features": [
		                "PADI开放水域潜水员",
		                "专业指导",
		                "快速掌握"
		            ],
		            "price": 3800,
		            "introduce": "<p><span style=\";font-family:&#39;Times New Roman&#39;;font-size:16px\">PADI<span style=\"font-family:宋体\">开放水域潜水员是广受全球公认且受重视的潜水员等级，考取</span></span><span style=\"font-family: 宋体;\">PADI开放水域潜水员鉴定卡（证书）后，您就可以单独和潜伴去潜</span><span style=\"font-family: 宋体;\">水</span><span style=\"font-family: 宋体;\">，不需要潜水专业人士在一旁督导了。</span><span style=\"font-family: 宋体;\">含</span><span style=\"font-family: 宋体;\">3次上岛</span><span style=\"font-family: 宋体;\">门船票，</span><span style=\"font-family: 宋体;\">发放PADI潜水证</span><span style=\"font-family: 宋体;\">。第1天为理论课，讲解潜水</span><span style=\"font-family: 宋体;\">方面的知识以及设备的使用方法；第2天到泳池穿上潜水设备进行实</span><span style=\"font-family: 宋体;\">操培训；第3天开始到海里实操，全程有教练陪同，后期实操时根据</span><span style=\"font-family: 宋体;\">客人掌握情况，可自行练习，教练跟随。收费3800元/位</span></p><p><br/></p>",
		            "experts": [
		                {
		                    "id": 10,
		                    "name": "who",
		                    "stars": 0,
		                    "avatar": "",
		                    "introduce": "",
		                    "features": [],
		                    "services": {
		                        "2015-09-20": 30,
		                        "2015-09-21": 30,
		                        "2015-09-22": 30,
		                        "2015-09-23": 30,
		                        "2015-09-24": 30,
		                        "2015-09-25": 30,
		                        "2015-09-26": 30,
		                        "2015-09-27": 30
		                    }
		                },
		                {
		                    "id": 11,
		                    "name": "who",
		                    "stars": 0,
		                    "avatar": "",
		                    "introduce": "",
		                    "features": [],
		                    "services": {
		                        "2015-09-20": 30,
		                        "2015-09-21": 30,
		                        "2015-09-22": 30,
		                        "2015-09-23": 30,
		                        "2015-09-24": 30,
		                        "2015-09-25": 30,
		                        "2015-09-26": 30,
		                        "2015-09-27": 30
		                    }
		                }
		            ]
		        }
		    ]
		}
		```



## 4. 详情页
### 4.1 达人
#### 4.1.1 达人详情页
* url:

		/v1/c/expert/
	
* params:
	
		1. id	达人 id	（Get or Post）

* response:
	
		1. ret:	1001	成功	0	无数据
		2. expert	=>	[
	        'id'    => 124,
	        'name'  =>  '陈成',
	        'stars' => 5,       //星级
	        'avatar'    =>  '@img-url',
	        'floorPrice'	=>	200,
	        'province'	=>	'海南省',
	        'city'	=>	'三亚市',
            "idCard"	=>	1,		//身份证
            "tel"	=>	18600502912,	//电话
            "mail"	=>	'azlarsin@gmail.com',		//邮箱
            "authInfo"	=>	0,	//认证信息
	        'background'	=>	'@img-url',
	        'features'  =>  ['打酱油', '吃饭'],
	        'services'  =>  [       //10: 全天可下单 20: 半天可下单   30: 不可下单
	            '2015-09-01' => 30
	            '2015-09-02' => 30
	            '2015-09-03' => 30
	            '2015-09-04' => 30
	            '2015-09-05' => 20
	            '2015-09-06' => 30
	            '2015-09-07' => 30
	            '2015-09-08' => 30
	            //....30 days 
	            //当月服务日历，打点代表不可购买：此处状态（数组 value） 10、20 时，为可购买状态（全、半天，不打点）；为 30 时，不可购买（打点）
	        ]
			'introduce' => 'why so serious',
			'shares'	=>	[
				'@img-url', 
				'@img-url', 
				'@img-url'
				//默认 5 张
			],
			'comments'	=>	[
				[
					'username'	=>	'陈成',
					'avatar'	=>	'@img-url',
					'stars'	=>	5,
					'time'	=>	'2015-09-24 19:51:59',
					'content'	=>	'服务很不错~~'
				],
				[
					'username'	=>	'陈成1',
					'avatar'	=>	'@img-url',
					'stars'	=>	3,
					'time'	=>	'2015-09-24 19:52:00',
					'content'	=>	'还不错'
				],
				//默认 3 条
			]
		]
* sample:

	```json
	url:	http://api.dogplanet.test/v1/c/expert
	
	params:	{"id": 6}
	
	or
	(http://api.dogplanet.test/v1/c/expert/6	Get)
	
	response:
	{
	    "ret": 1001,
	    "expert": {
	        "id": 6,
	        "name": "陈成",
	        "stars": 0,
	        "avatar": "",
	        "floorPrice": 200,
	        "province": "海南省",
	        "city": "三亚市",
	        "idCard": 1,
	        "tel": 18600500000,
	        "mail": azlarsin@gmail.com,
	        "authInfo": 0,
	        "background": "",
	        "introduce": "这个人很吊",
	        "features": [
	            "潜水"
	        ],
	        "services": {
	            "2015-09-01": 30,
	            "2015-09-02": 30,
	            "2015-09-03": 30,
	            "2015-09-04": 30,
	            "2015-09-05": 30,
	            "2015-09-06": 30,
	            "2015-09-07": 30,
	            "2015-09-08": 30,
	            "2015-09-09": 30,
	            "2015-09-10": 30,
	            "2015-09-11": 30,
	            "2015-09-12": 30,
	            "2015-09-13": 30,
	            "2015-09-14": 30,
	            "2015-09-15": 30,
	            "2015-09-16": 30,
	            "2015-09-17": 10,
	            "2015-09-18": 30,
	            "2015-09-19": 30,
	            "2015-09-20": 30,
	            "2015-09-21": 30,
	            "2015-09-22": 30,
	            "2015-09-23": 20,
	            "2015-09-24": 30,
	            "2015-09-25": 30,
	            "2015-09-26": 30,
	            "2015-09-27": 30,
	            "2015-09-28": 30,
	            "2015-09-29": 30,
	            "2015-09-30": 30
	        },
	        "shares": [
	            "http://123.56.154.187:8090/expert/201509/24/a0d16aec-dd19-a846-f53e-ac7b655a3348.jpg",
	            "http://123.56.154.187:8090/expert/201509/24/a0d16aec-dd19-a846-f53e-ac7b655a3348.jpg",
	            "http://123.56.154.187:8090/expert/201509/23/43fda131-6371-e921-207b-08fb796670e8.png"
	        ],
	        "comments": [
	            {
	                "username": "azlar",
	                "avatar": "",
	                "stars": 5,
	                "time": "2015-09-24 19:51:59",
	                "content": "阳光、沙滩、海风、爱人，独享宁静的二人世界。犹如在海面上漫步是广大爱好海上运动朋友的首选伙伴，它具有清洁、环保、噪音小等优点。蜈支洲岛选用的电动船设计新颖独特、造工精细、色彩艳 丽、质量可靠，适用与朋友休闲游乐，也适合谈情说爱的情侣电动船。"
	            },
	            {
	                "username": "azlar",
	                "avatar": "",
	                "stars": 2,
	                "time": "2015-09-24 17:51:17",
	                "content": "潜水时间为30分钟左右，夜间正常情况下开放时间为18:00-22:00，在漆黑的水中顺着潜水灯的指引缓缓前行，潜入漆黑的海中并没有你想像得那么恐怖，相反，它会带给你一种别样的新奇感受，收费680元/位\r\n"
	            },
	            {
	                "username": "azlar",
	                "avatar": "",
	                "stars": 3,
	                "time": "2015-09-24 13:51:37",
	                "content": "三亚蜈支洲岛珊瑚酒店地处蜈支洲岛西北角，是浪漫求婚，蜜月旅行，欢度幸福时光的甜蜜之所。一座浪漫的岛屿，绿林万丈；一片美丽的海湾，夕阳和海色静静相会；细腻白沙层层铺上海滩，自在旅人尽情呼吸自然空气。\n\n\n酒店由4栋连体建筑相连而成唯美的珊瑚状，设计装潢处处完美融合各种海洋元素，精致而独特，似一个海底精灵活跃在南海之滨，国家海岸。珊瑚酒店拥有257间高品质海岛度假型豪华客房，空间宽敞，景色优美，"
	            }
	        ]
	    }
	}
    
    ```



#### 4.1.2 达人详情页 - 日历
* url:

		/v1/c/expert/get-services
		
* params:

		1. id	达人	id
		2. date	服务月（如 2015-09, 2015-10, 2015-08）

* response:
		
		1. ret: 1001    成功  0   无数据
		2. services  =>  
			[       
					//10: 全天可下单 20: 半天可下单   30: 不可下单
	            '2015-09-01' => 30
	            '2015-09-02' => 20
	            '2015-09-03' => 30
	            '2015-09-04' => 30
	            '2015-09-05' => 20
	            '2015-09-06' => 30
	            '2015-09-07' => 30
	            '2015-09-08' => 30
	            //....30 days
	            //当月服务日历，打点代表不可购买：此处状态（数组 value） 10、20 时，为可购买状态（全、半天，不打点）；为 30 时，不可购买（打点）
	            ]

* sample

	```json
	url:	http://api.dogplanet.test/v1/c/expert/get-services
	
	params:	{"id": 6,  "date": '2015-9'}
	
	response:
	{
	    "ret": 1001,
	    "services": {
	        "2015-09-01": 30,
	        "2015-09-02": 10,
	        "2015-09-03": 30,
	        "2015-09-04": 30,
	        "2015-09-05": 30,
	        "2015-09-06": 30,
	        "2015-09-07": 30,
	        "2015-09-08": 30,
	        "2015-09-09": 30,
	        "2015-09-10": 30,
	        "2015-09-11": 30,
	        "2015-09-12": 30,
	        "2015-09-13": 30,
	        "2015-09-14": 30,
	        "2015-09-15": 30,
	        "2015-09-16": 30,
	        "2015-09-17": 10,
	        "2015-09-18": 30,
	        "2015-09-19": 30,
	        "2015-09-20": 30,
	        "2015-09-21": 30,
	        "2015-09-22": 30,
	        "2015-09-23": 20,
	        "2015-09-24": 30,
	        "2015-09-25": 30,
	        "2015-09-26": 30,
	        "2015-09-27": 30,
	        "2015-09-28": 30,
	        "2015-09-29": 30,
	        "2015-09-30": 30
	    }
	}
	
	```
    &
	
	```json
	url:	http://api.dogplanet.test/v1/c/expert/get-services
	
	params:	{"id": 6， "date": '2015-10'}
	
	response:
	{
	    "ret": 1001,
	    "services": {
	        "2015-10-01": 30,
	        "2015-10-02": 30,
	        "2015-10-03": 30,
	        "2015-10-04": 30,
	        "2015-10-05": 30,
	        "2015-10-06": 30,
	        "2015-10-07": 30,
	        "2015-10-08": 30,
	        "2015-10-09": 30,
	        "2015-10-10": 30,
	        "2015-10-11": 30,
	        "2015-10-12": 30,
	        "2015-10-13": 30,
	        "2015-10-14": 30,
	        "2015-10-15": 30,
	        "2015-10-16": 30,
	        "2015-10-17": 30,
	        "2015-10-18": 30,
	        "2015-10-19": 30,
	        "2015-10-20": 30,
	        "2015-10-21": 30,
	        "2015-10-22": 30,
	        "2015-10-23": 20,
	        "2015-10-24": 30,
	        "2015-10-25": 30,
	        "2015-10-26": 30,
	        "2015-10-27": 30,
	        "2015-10-28": 30,
	        "2015-10-29": 30,
	        "2015-10-30": 30,
	        "2015-10-31": 30
	    }
	}

	```





#### 4.1.3 达人详情页 - 评论
* url:

		/v1/c/expert/get-comments

* params: 
	
		1. id	达人	id
		2. page	页码	默认为 0 
		3. pageSize	每页显示条数	默认为 10

* response:

		1. ret: 1001    成功  0   无数据
		2. 'comments'	=>	[
				[
					'username'	=>	'陈成',
					'avatar'	=>	'@img-url',
					'stars'	=>	5,
					'time'	=>	'2015-09-24 19:51:59',
					'content'	=>	'服务很不错~~'
				],
				[
					'username'	=>	'陈成1',
					'avatar'	=>	'@img-url',
					'stars'	=>	3,
					'time'	=>	'2015-09-24 19:52:00',
					'content'	=>	'还不错'
				],
				//默认 3 条
			]

* sample:

	```json
	url:	http://api.dogplanet.test/v1/c/expert/get-comments?id=6&pageSize=3
	
	params:	{"id": 6， "date": '2015-10'}
	
	response:
	{
	    "ret": 1001,
	    "comments": [
	        {
	            "username": "azlar",
	            "avatar": "http://img0.dogplanet.test/tou.jpg",
	            "stars": 5,
	            "time": "2015-09-24 19:51:59",
	            "content": "阳光、沙滩、海风、爱人，独享宁静的二人世界。犹如在海面上漫步是广大爱好海上运动朋友的首选伙伴，它具有清洁、环保、噪音小等优点。蜈支洲岛选用的电动船设计新颖独特、造工精细、色彩艳 丽、质量可靠，适用与朋友休闲游乐，也适合谈情说爱的情侣电动船。"
	        },
	        {
	            "username": "azlar",
	            "avatar": "http://img0.dogplanet.test/tou.jpg",
	            "stars": 2,
	            "time": "2015-09-24 17:51:17",
	            "content": "潜水时间为30分钟左右，夜间正常情况下开放时间为18:00-22:00，在漆黑的水中顺着潜水灯的指引缓缓前行，潜入漆黑的海中并没有你想像得那么恐怖，相反，它会带给你一种别样的新奇感受，收费680元/位\r\n"
	        },
	        {
	            "username": "azlar",
	            "avatar": "http://img0.dogplanet.test/tou.jpg",
	            "stars": 3,
	            "time": "2015-09-24 17:51:17",
	            "content": "12312321321~~~~"
	        },
	        {
	            "username": "azlar",
	            "avatar": "http://img0.dogplanet.test/tou.jpg",
	            "stars": 3,
	            "time": "2015-09-24 13:51:37",
	            "content": "三亚蜈支洲岛珊瑚酒店地处蜈支洲岛西北角，是浪漫求婚，蜜月旅行，欢度幸福时光的甜蜜之所。一座浪漫的岛屿，绿林万丈；一片美丽的海湾，夕阳和海色静静相会；细腻白沙层层铺上海滩，自在旅人尽情呼吸自然空气。\n\n\n酒店由4栋连体建筑相连而成唯美的珊瑚状，设计装潢处处完美融合各种海洋元素，精致而独特，似一个海底精灵活跃在南海之滨，国家海岸。珊瑚酒店拥有257间高品质海岛度假型豪华客房，空间宽敞，景色优美，"
	        },
	        {
	            "username": "azlar",
	            "avatar": "http://img0.dogplanet.test/tou.jpg",
	            "stars": 5,
	            "time": "2015-09-24 13:51:17",
	            "content": "这次服务还不错。"
	        }
	    ]
	}
		
	```

### 4.2 产品
#### 4.2.1 产品详情页
* 说明
	- **逻辑说明**
		1. 产品详情分为两种：
			* 平台产品
				
				1. 平台商品请求的参数中，没有 expertId 字段，返回的参数中，携带推荐达人 product['experts']，没有 expertId 字段
				2. 平台商品的入口为 列表页

			* 达人（拥有）产品
					
				1. 请求的时候携带 expertId, 返回的参数中没有推荐达人，携带 expertId
				2. **达人产品详情页，目前的入口只有两个**：
					- 确认（服务）订单页的 [5.2.2 **达人推荐产品**](#toc_28) 达人推荐产品
					- 购物车内点击按钮进入的 [10. **达人商城**](#toc_54) 

	- 使用说明
		1. sliders：产品轮播图
		2. features：亮点
		3. subs：子产品
		4. weekend_price、festival_price 分别为：周末价格、节假日价格(暂时可能用不到)
		5. festival_price 暂时没有数据，为 0
		6. 暂时没有 “注意事项”、“退订策略” 字段
		7. 达人一次给了 12 个，子产品一次给了 所有 的
		8. 产品详情添加了 **`费用说明`(costInfo) `产品说明`(productInfo) `使用方法`(usageInfo) `退改规则`(refundInfo)** 四项，格式同原有的 `产品描述`(introduct)；具体使用参考产品的文档。
		9. 子产品字段中追加了一个 `advance => n` 参数，用来判断该子产品需要提前 `n` 天购买

* url:

		1. /v1/c/product

* params:
	- 平台商品
	
			1. id   产品 id
	
	- 达人商品
			
			1. id	产品 id
			2. expertId	达人 id

* response:
	
	- 平台商品
	
			1. ret: 1001    成功  0   参数错误
			2. product	=>	[
					'id'	=>	10099,
					'name'	=>	'蜈支洲岛珊瑚酒店',
					'price'	=>	1500,
					'features'	=>	['麻将房', '6平米私家泳池'],
					'introduce'	=>	'三亚蜈支洲珊瑚酒店',
					
					'costInfo'	=>	'费用说明',
					'productInfo'	=>	'产品说明',
					'usageInfo'	=>	'使用说明',
					'refundInfo'	=>	'退改规则',
					
					'sliders'	=>	[
						'@img-url',
						'@img-url',
						'@img-url',
	
						//...
					],
					'subs'	=>	[
						[
							'id'	=>	10129,
							'name'	=>	'海景房',
							'price'	=>	1900,
							'weekend_price'	=>	2200,
							'festival_price'	=>	0,
							'introduction'	=>	'珊瑚大床房',
							'thumb'	=>	'@img-url'
							'advance'	=>	0,
						],
						[
							'id'	=>	10130,
							'name'	=>	'麻将房',
							'price'	=>	2100,
							'weekend_price'	=>	2300,
							'festival_price'	=>	0,
							'introduction'	=>	'麻将房',
							'thumb'	=>	'@img-url',
							'advance'	=>	0,
						]
					],
					
					'experts'	=>	[
						[
							'id'	=>	'6',
							'name'	=>	陈成,
							'avatar'	=>	'@img-url'
						],
											[
							'id'	=>	'10',
							'name'	=>	吴蔚,
							'avatar'	=>	'@img-url'
						],
					]
					
				]
	- 达人商品
				
				1. ret: 1001    成功  0   参数错误
				2. product	=>	[
					'id'	=>	10099,
					'expertId'	=>	6
					'name'	=>	'蜈支洲岛珊瑚酒店',
					'price'	=>	1500,
					'features'	=>	['麻将房', '6平米私家泳池'],
					'introduce'	=>	'三亚蜈支洲珊瑚酒店',
					
					'costInfo'	=>	'费用说明',
					'productInfo'	=>	'产品说明',
					'usageInfo'	=>	'使用说明',
					'refundInfo'	=>	'退改规则',
					
					'sliders'	=>	[
						'@img-url',
						'@img-url',
						'@img-url',
	
						//...
					],
					'subs'	=>	[
						[
							'id'	=>	10129,
							'name'	=>	'海景房',
							'price'	=>	1900,
							'weekend_price'	=>	2200,
							'festival_price'	=>	0,
							'introduction'	=>	'珊瑚大床房',
							'thumb'	=>	'@img-url'
						],
						[
							'id'	=>	10130,
							'name'	=>	'麻将房',
							'price'	=>	2100,
							'weekend_price'	=>	2300,
							'festival_price'	=>	0,
							'introduction'	=>	'麻将房',
							'thumb'	=>	'@img-url'
						]
					],
			
* sample:
	
	- 平台商品
	
	```json
	url:	http://api.dogplanet.test/v1/c/product/10099
	
	params:	{"id": 10099}
	
	response:
	{
	    "ret": 1001,
	    "product": {
	        "id": 10099,
	        "name": "蜈支洲岛珊瑚酒店",
	        "price": 1500,
	        "features": [
	            "特别牛逼",
	            "分布于3至7层，68平方米",
	            "阳台大泡池沐浴",
	            "分布于4至6层，158平方米的面积",
	            "设有上、下楼两层，上层为客厅，下层为大床房",
	            "分布于1 至7 层，81平方米",
	            "简单淡雅，富有童趣",
	            "光照充足",
	            "分布于4至7层，68平方米",
	            "“至尊”海景视野",
	            "分布于2层，146平方米",
	            "设有上、下楼两层，下层为主客厅，上层为大床房",
	            "6平方米的私家泳",
	            "超豪华的私人阳台椅",
	            "分布于3至5层，82-113平方米",
	            "专属大泡池",
	            "豪华一线海景大阳台",
	            "分布于4层，158平方米的面积",
	            "设有上、下楼两层，上层为大床房，下层为双床房",
	            "豪华家庭房",
	            "超豪华的浴室设施配有时尚前卫的圆形大浴缸",
	            "2部42寸液晶电视",
	            "分布于2 层，158平方米",
	            "36平方米的私家泳池",
	            "下楼两层，上下层均为双床房",
	            "落地窗优质采光",
	            "分布于2至7层，82平方米",
	            "透明的落地窗",
	            "2部42寸液晶电视",
	            "分布于1-4层，61平方米",
	            "超豪华的私人大阳台",
	            "36平方米的专属私家泳池",
	            "分布于3、4层，113 平方米",
	            "海棠湾一线海景视野",
	            "270度的露天环海大阳台",
	            "分布于3至7层，68平方米",
	            "专属私人阳台上",
	            "俯瞰热带花园",
	            "全海景的视野",
	            "分布于4、5层 ，113平方米",
	            "麻将桌",
	            "分布于1至5层，63平方米",
	            "采光充足",
	            "享有碧绿葱翠的园林视野"
	        ],
	        "introduce": "<p>三亚蜈支洲岛珊瑚酒店地处蜈支洲岛西北角，是浪漫求婚，蜜月旅行，欢度幸福时光的甜蜜之所。一座浪漫的岛屿，绿林万丈；一片美丽的海湾，夕阳和海色静静相会；细腻白沙层层铺上海滩，自在旅人尽情呼吸自然空气。</p><p><br/></p><p>酒店由4栋连体建筑相连而成唯美的珊瑚状，设计装潢处处完美融合各种海洋元素，精致而独特，似一个海底精灵活跃在南海之滨，国家海岸。珊瑚酒店拥有257间高品质海岛度假型豪华客房，空间宽敞，景色优美，最小房间面积达60平方米。客房设计汲取五彩大地之灵感，将海洋元素融入其中，尽显海岛度假酒店的理念与生活。酒店拥有7间特色餐厅及酒廊，时尚入流，中西合璧。</p><p>53间各式风情木屋错落有致地分布在小岛各域。因房型、房间的地理位置和服务的差别，这些客房分为海韵木楼、临海木屋、云海别墅、豪华别墅和岛主别墅。房间周边，绿意深邃。房间内装修典雅，设备齐全。身处绿林遍布的海岛，犹如深处返璞归真之地。绿意满眼、清啼绕耳、大海无限的景致带您体验“天然海岛，度假养生”的“中国马尔代夫”生活。</p><p>酒店拥有七间特色餐厅及酒廊，时尚入流，中西合璧。酒店拥有一间富丽堂皇的大型多功能宴会厅和3间各具特色的小型会议室。无论是商界精英聚会还是亲朋好友私人小会，珊瑚酒店都可为您提供精致与奢华的个性化特色化服务。</p><p>酒店设施：西式餐厅、中式餐厅、残疾人设施、室外游泳池、会议室、SPA、无烟房、商务中心、桑拿、棋牌室、健身房、酒吧</p><p>网络设施：有可无线上网的公共区域&nbsp;免费</p><p>停车场：酒店提供免费停车位</p><p>房间设施：宽带上网&nbsp;空调&nbsp;国际长途电话&nbsp;吹风机&nbsp;24小时热水</p><p>酒店服务：早餐、接站、接机、接待外宾、洗衣、行李寄存、看护小孩、租车、叫醒</p><p><br/></p>",
	        "costInfo": "",
	        "productInfo": "",
	        "usageInfo": "",
	        "refundInfo": "",
	        "sliders": [
	            "http://123.56.154.187:8090/product/201508/24/c32c2d5f-f8dd-528a-9746-9531765260e8.jpg",
	            "http://123.56.154.187:8090/product/201508/24/6b892b0d-ba1d-1bd0-b803-33440dc79885.jpg",
	            "http://123.56.154.187:8090/product/201508/24/61b2fb32-984b-8894-3f45-e8ea1627546a.jpg",
	            "http://123.56.154.187:8090/product/201508/24/1419eb0f-95d6-71e7-1ccf-5ca0a612fdeb.jpg",
	            "http://123.56.154.187:8090/product/201508/24/3a06d343-3846-34cb-c17b-864b4b2a89c5.jpg",
	            "http://123.56.154.187:8090/product/201508/24/90f68ca4-bca5-74f4-d6f5-7baf9f9b2bd6.jpg",
	            "http://123.56.154.187:8090/product/201508/24/0044460f-f769-e6cd-edce-2dfeb8883250.jpg",
	            "http://123.56.154.187:8090/product/201508/24/105c02f4-f9a8-f23d-da0a-856a3a61af00.jpg",
	            "http://123.56.154.187:8090/product/201508/24/672f8bce-0194-ee20-887e-62b905bedded.jpg",
	            "http://123.56.154.187:8090/product/201508/24/37b0d725-2dde-2bea-bd15-96e3b24c0a64.jpg",
	            "http://123.56.154.187:8090/product/201508/24/d7d2e5d8-284f-e814-96f8-a9058466a72c.jpg",
	            "http://123.56.154.187:8090/product/201508/24/2c013fb2-490e-253e-8e95-46b29595fc9f.jpg",
	            "http://123.56.154.187:8090/product/201508/24/bc7b41ed-e307-301c-b8d5-c19126400e77.jpg",
	            "http://123.56.154.187:8090/product/201508/24/279b615d-c03a-2ca4-6561-0f01a21ce2d2.jpg",
	            "http://123.56.154.187:8090/product/201508/24/da0955bd-eea8-8bb7-f1f3-e13469f74d5f.jpg",
	            "http://123.56.154.187:8090/product/201508/24/7d212d16-c1fd-5267-fa2b-9317115a21f1.jpg",
	            "http://123.56.154.187:8090/product/201508/24/c314a2c4-774b-4cd5-8f36-a886d384cc97.jpg",
	            "http://123.56.154.187:8090/product/201508/24/1f220401-fbc3-40d6-1bff-5126b5e23285.jpg",
	            "http://123.56.154.187:8090/product/201508/24/aa1625b0-21f4-1552-00ed-6a548c354b7d.jpg",
	            "http://123.56.154.187:8090/product/201508/24/45ebd532-5a55-4823-6c26-a71015b8b34d.jpg",
	            "http://123.56.154.187:8090/product/201508/24/3abe38ad-d398-27bc-4c1d-84d4db9c38b5.jpg",
	            "http://123.56.154.187:8090/product/201508/24/71386323-0f64-c4ff-ee2e-4e9d2df17451.jpg",
	            "http://123.56.154.187:8090/product/201508/24/3744a360-c507-fbe1-b8d4-031ea194ea8a.jpg",
	            "http://123.56.154.187:8090/product/201508/24/67eef8c5-13f6-7da1-b7a8-642950d5f422.jpg",
	            "http://123.56.154.187:8090/product/201508/24/b817fc32-c575-7907-bfec-574c672df7af.jpg",
	            "http://123.56.154.187:8090/product/201508/24/21a05f75-d206-7f33-f8b7-831205146097.jpg",
	            "http://123.56.154.187:8090/product/201508/24/0e24c453-778c-a72f-e6af-6b98d7961ccf.jpg",
	            "http://123.56.154.187:8090/product/201508/24/fdc6dc77-3b3b-b56a-c0fc-c00d7155e854.jpg",
	            "http://123.56.154.187:8090/product/201508/24/e7e5ef46-101c-e451-9674-41c118cbd5b9.jpg",
	            "http://123.56.154.187:8090/product/201508/24/09c07c25-6b50-fab6-7948-0f8e766501f3.jpg",
	            "http://123.56.154.187:8090/product/201508/24/4935c26c-9c1f-1852-ac67-41a95f8c5b50.jpg",
	            "http://123.56.154.187:8090/product/201508/24/8cc12a21-733f-3348-39dd-c04da62cba15.jpg",
	            "http://123.56.154.187:8090/product/201508/24/54cdc8fa-b6d1-b4f2-05c1-b45bc56448de.jpg",
	            "http://123.56.154.187:8090/product/201508/24/db088fe8-e151-564d-97ad-5482112fcb12.jpg",
	            "http://123.56.154.187:8090/product/201508/24/0d206fc8-4e2a-c60a-aef8-ec19a7d75189.jpg",
	            "http://123.56.154.187:8090/product/201508/24/f3034b88-c93c-ffa7-ccbb-0f417364a626.jpg",
	            "http://123.56.154.187:8090/product/201508/24/aa2ccb9f-4855-9e42-319c-b0c13f1f52b0.jpg",
	            "http://123.56.154.187:8090/product/201508/24/b9ebd42d-b1cb-04ae-ee95-f0fd77c8b81f.jpg",
	            "http://123.56.154.187:8090/product/201508/24/e0bd43f9-4bc9-ae9f-4165-f81f7a13225c.jpg",
	            "http://123.56.154.187:8090/product/201508/24/0d0f07a2-6659-c36c-9618-8c9d61ebe6df.jpg",
	            "http://123.56.154.187:8090/product/201508/24/d5bc19d4-790c-c5a5-c28a-872e2fd61d4b.jpg",
	            "http://123.56.154.187:8090/product/201508/24/69ca0ffd-6224-3070-e0a3-483f03b5aa02.jpg",
	            "http://123.56.154.187:8090/product/201508/24/69d914e8-4eae-be55-706d-7ce87e10e2f7.jpg",
	            "http://123.56.154.187:8090/product/201508/24/1fbeaa04-33b8-16d3-7c13-b1fc449a651b.jpg",
	            "http://123.56.154.187:8090/product/201508/24/812fe2c6-84b4-633f-4523-fc2a2af35669.jpg",
	            "http://123.56.154.187:8090/product/201508/24/05df9756-4a1c-4fad-3709-e4d1c18bd307.jpg"
	        ],
	        "subs": [
	            {
	                "id": 10129,
	                "name": "珊瑚豪华海景房（大/双）",
	                "price": 1900,
	                "weekend_price": 2200,
	                "festival_price": 0,
	                "introduction": "<p>分布于3至7层，68平方米。中国蜈支洲岛—“中国马尔代夫，东方夏威夷”。一心一念一风景，观落日潮汐，看云卷云舒。珊瑚豪华海景房室内设计极富海洋风格，精心典雅，或清新或肃穆，尽显海的韵味。日落时分，色彩变幻天际，躺在半露天的阳台大泡池沐浴，一杯咖啡或一杯红酒，情人的耳鬓私语或家人的欢声笑语，海岛的度假滋味，幸福不言而喻。</p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p><p><br/></p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/90f68ca4-bca5-74f4-d6f5-7baf9f9b2bd6.jpg"
	            },
	            {
	                "id": 10128,
	                "name": "珊瑚麻将房（大/双）",
	                "price": 1900,
	                "weekend_price": 2200,
	                "festival_price": 0,
	                "introduction": "",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/105c02f4-f9a8-f23d-da0a-856a3a61af00.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10126,
	                "name": "珊瑚亲子房（大+小）",
	                "price": 2000,
	                "weekend_price": 2400,
	                "festival_price": 0,
	                "introduction": "<p>分布于1&nbsp;至7&nbsp;层，81平方米，热带花园洋溢着南国的风情气息，碧波荡漾的海水泛着层层剔透的光。一家人的海岛之旅，幸福而又甜蜜的旅程。珊瑚亲子房室内设计清新自然，简单淡雅，富有童趣。珊瑚亲子房将地道的海南文化和精致典雅的艺术风格进行融合，采用极具异域风情的木质色调和传统面料装饰，在透过落地窗进入房间内的充足自然采光的照射下显得熠熠生辉。</p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/d7d2e5d8-284f-e814-96f8-a9058466a72c.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10125,
	                "name": "珊瑚全海景房（大）",
	                "price": 2200,
	                "weekend_price": 2600,
	                "festival_price": 0,
	                "introduction": "<p>分布于4至7层，68平方米。窗外流动着180度的纯美景致，无穷海景延伸至天际，满山满园的绿意在眼前分明跳窜。全海景的视野，全方位的享受，全面的海岛度假生活体验，让您拥有独一无二的度假回忆。珊瑚全海景房带给您的“至尊”海景视野，恰如上帝后花园的美，洒落在这片净土，你无需抗拒，只需走进，便可感同身受。</p><p><br/></p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p><p><br/></p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/279b615d-c03a-2ca4-6561-0f01a21ce2d2.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10127,
	                "name": "珊瑚园景池畔套房（复式）",
	                "price": 2600,
	                "weekend_price": 3100,
	                "festival_price": 0,
	                "introduction": "<p>分布于2层，146平方米，设有上、下楼两层，下层为主客厅，上层为大床房。36平方米的私家泳池环绕在热带园林里，郁郁葱葱的绿意带给人无限惬意。清晨的鸟鸣环绕于耳际，泳池的泉水叮咚，躺在超豪华的私人阳台椅上感受别样的南国海岛风情，或潇洒自如地躺在泳池内畅游或嬉戏，尽情享受海岛度假惬意时光！</p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/c314a2c4-774b-4cd5-8f36-a886d384cc97.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10124,
	                "name": "珊瑚全海景套房（大/双）",
	                "price": 3500,
	                "weekend_price": 3900,
	                "festival_price": 0,
	                "introduction": "<p>分布于3至5层，您将在82-113平方米的豪华海景套房中体验独一无二的高品质海岛度假酒店的绝美景致。您可站在超豪华的一线海景大阳台上欣赏无边的海景美色；您可躺在专属的大泡池里感受蜈支洲岛的温暖和舒适。您可卧可躺可静可动，您可在这里静静享受身体的放松和心灵的自由。豪华海景套房别具一格的装修风格，将海洋的灵动和艺术的瑰丽渗透融合，能满足您对奢华海岛度假酒店的所有期待。</p><p><br/></p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p><p><br/></p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/3abe38ad-d398-27bc-4c1d-84d4db9c38b5.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10123,
	                "name": "珊瑚家庭套房（复式）",
	                "price": 3700,
	                "weekend_price": 4100,
	                "festival_price": 0,
	                "introduction": "<p>分布于4层，158平方米的面积，设有上、下楼两层，上层为大床房，下层为双床房，是全家人旅行入住的理想之选。超豪华的浴室设施配有时尚前卫的圆形大浴缸，2部42寸液晶电视。豪华园景池畔房将地道的海南文化和精致典雅的艺术风格进行融合，采用极具异域风情的木质色调和传统面料装饰，在透过落地窗进入房间内的充足自然采光的照射下显得熠熠生辉。别致的花洒和独立浴缸设计给您带来非凡怡人的沐浴享受。浴室内设有梳妆区和独立雨林淋浴间，并为您提供独特的海盐用品，让您拥有无与伦比的海岛度假生活体验。</p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/67eef8c5-13f6-7da1-b7a8-642950d5f422.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10122,
	                "name": "珊瑚家庭池畔套房（复式）",
	                "price": 4100,
	                "weekend_price": 4600,
	                "festival_price": 0,
	                "introduction": "<p>分布于2&nbsp;层，158平方米，设有上、下楼两层，上下层均为双床房。36平方米的私家泳池环绕在热带花园里，郁郁葱葱的绿意带给您无限惬意。客房设计将地道的海南文化和精致典雅进行艺术化融合，采用极具异域风情的木质色调和传统面料装饰，在透过落地窗进入房间内的充足自然采光的照射下显得更加熠熠生辉。让您拥有无与伦比的海岛度假生活体验。</p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/0e24c453-778c-a72f-e6af-6b98d7961ccf.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10121,
	                "name": "珊瑚豪华园景套房（双床）",
	                "price": 1900,
	                "weekend_price": 2200,
	                "festival_price": 0,
	                "introduction": "<p>分布于2至7层，82平方米。透过透明的落地窗，热带园林景致顿时一览无遗。豪华园景套房设有客厅和卧室，房间配有2部42寸液晶电视。每间客房均带有令人身心舒适的浴室设施，浴室配有豪华的圆形大浴缸，精致的装修风格和别致的陈设极具海洋特色和现代感，时尚富有活力，令您在游玩一整天后心情无比放松，活力满满，并且带来内心的宁静。</p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/09c07c25-6b50-fab6-7948-0f8e766501f3.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10120,
	                "name": "珊瑚豪华池畔房（大/双）",
	                "price": 1700,
	                "weekend_price": 1900,
	                "festival_price": 0,
	                "introduction": "<p>分布于1-4层，61平方米，壮丽的蜈支洲岛热带园林美景尽显眼前，独特的园林景观设计集会了蜈支洲岛春季的暖，夏季的艳，秋季的静和冬季的凉。超豪华的私人大阳台和36平方米的专属私家泳池更显海岛度假酒店的奢华。</p><p><br/></p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p><p><br/></p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/54cdc8fa-b6d1-b4f2-05c1-b45bc56448de.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10119,
	                "name": "珊瑚家庭豪华海景套房（二房一厅）",
	                "price": 5300,
	                "weekend_price": 5800,
	                "festival_price": 0,
	                "introduction": "<p>分布于3、4层，113&nbsp;平方米，珊瑚家庭豪华海景套房尊享超豪华的国家海岸-海棠湾一线海景视野，270度的露天环海大阳台将绝美的一线海景景致，一线园林景致统统纳入您的视野，是追求奢华旅行入住的理想之选。客房设计将地道的海南文化和精致典雅进行艺术化融合，采用极具异域风情的木质色调和传统面料装饰，在透过落地窗进入房间内的充足自然采光的照射下显得更加熠熠生辉。让您拥有无与伦比的海岛度假生活体验。</p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/f3034b88-c93c-ffa7-ccbb-0f417364a626.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10118,
	                "name": "珊瑚高级海景房（大/双）",
	                "price": 1700,
	                "weekend_price": 1900,
	                "festival_price": 0,
	                "introduction": "<p>分布于3至7层，68平方米。身处一座岛，心在天地外。站在高级海景房的专属私人阳台上，俯瞰热带花园里纯粹的绿，感受举目间便已倾心的蜈支洲岛海水壮阔的蓝。看海视觉没有豪华海景房的“正”和全海景房的“尊”，但南国无限风情的旖旎风光却在春暖花开的气息里，展现无遗！</p><p><br/></p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p><p><br/></p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/e0bd43f9-4bc9-ae9f-4165-f81f7a13225c.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10117,
	                "name": "珊瑚家庭顶级海景套（二房一厅）",
	                "price": 5500,
	                "weekend_price": 6000,
	                "festival_price": 0,
	                "introduction": "<p>分布于4、5层&nbsp;，113平方米，珊瑚家庭顶级套房尊享至尊的国家海岸-海棠湾一线海景视野，房间配有麻将桌供您娱乐。壮丽的蜈支洲岛海景和园景尽在眼前，是追求奢华旅行入住的至佳选择。客房设计将地道的海南文化和精致典雅进行艺术化融合，采用极具异域风情的木质色调和传统面料装饰，在透过落地窗进入房间内的充足自然采光的照射下显得更加熠熠生辉。一切您所向往的海岛度假生活，这里应有尽有。</p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p><p><br/></p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/69ca0ffd-6224-3070-e0a3-483f03b5aa02.jpg",
	                "advance": 0
	            },
	            {
	                "id": 10116,
	                "name": "珊瑚园景房（大/双）",
	                "price": 1500,
	                "weekend_price": 1700,
	                "festival_price": 0,
	                "introduction": "<p>分布于1至5层，63平方米，珊瑚园景房享有碧绿葱翠的园林视野。清晨，当朝阳从海边徐徐升起，白色电动窗帘徐徐拉开，瑰丽的园林景致便随着阳光的斑驳跳入视野，眼望美景，耳听鸟鸣，感受宁静。珊瑚园景房将地道的海南文化和精致典雅的艺术风格进行融合，采用极具异域风情的木质色调和传统面料装饰，在透过落地窗进入房间内的充足自然采光的照射下显得熠熠生辉。</p><p><br/></p><p>1、以上房价适用于单人和双人入住，并包含15%的服务费，以及单人或双人份早餐。不包含人民币11元/人/晚的政府价格调节基金。第三成人入住需加床400元/床净价，568元/床含一张门船票，700元/床含1人门船票及1人早餐。</p><p>2、增订早餐：人民币198元每人每餐（含15%服务费），客人前台现付价格198元每人每餐加收15%服务费。儿童增订早餐：身高1.2米以下的免费同时免收船票，身高1.2米-1.4米的收费为98元每人每餐（含15%服务费），客人前台现付价格98加收15%服务费。</p><p>3、&nbsp;客房尊享礼遇：</p><p>①&nbsp;免费穿梭巴士</p><p>②&nbsp;享受VIP绿色通道快速登岛</p><p>③&nbsp;上岛船票两张</p><p>④&nbsp;迎宾饮料</p><p>⑤&nbsp;欢迎水果</p><p>⑥&nbsp;每日豪华早餐两份</p><p>⑦&nbsp;免费租车（东风标致车，需提前预约）</p><p>⑧&nbsp;免费参加篝火晚会</p><p>特别提示</p><p>1、&nbsp;本岛不具备条件接待孕妇、70岁或以上的人群。</p><p>2、&nbsp;17：00之前随时发船，17:30最后一班&nbsp;船,请务必在17点前达到码头.</p><p>3、&nbsp;酒店入住时间为15:00，退房时间为12:00。</p><p>如遇自然灾害（例如：台风、火灾等）及不可抗力因素，无法正常上下岛，或无法入住珊瑚酒店，甲方不收取乙方任何房费。如乙方已付房费，甲方不退款，将费用留店冲抵。</p>",
	                "thumb": "http://123.56.154.187:8090/product/201508/24/812fe2c6-84b4-633f-4523-fc2a2af35669.jpg",
	                "advance": 0
	            }
	        ],
	        "experts": [
	            {
	                "id": 6,
	                "name": "陈成",
	                "avatar": ""
	            },
	            {
	                "id": 10,
	                "name": "吴蔚",
	                "avatar": "http://123.56.154.187:8090/expert/201510/26/a7d5787f-4d56-c99e-c06b-056aa4ad1cf2.jpg"
	            },
	            {
	                "id": 11,
	                "name": "ww",
	                "avatar": "http://123.56.154.187:8090/expert/201509/30/fbb42617-5abe-6f50-d686-2cd380ebd7af.jpg"
	            },
	            {
	                "id": 15,
	                "name": "",
	                "avatar": ""
	            },
	            {
	                "id": 10,
	                "name": "吴蔚",
	                "avatar": "http://123.56.154.187:8090/expert/201510/26/a7d5787f-4d56-c99e-c06b-056aa4ad1cf2.jpg"
	            },
	            {
	                "id": 3,
	                "name": "老高",
	                "avatar": "http://123.56.154.187:8090/expert/201509/30/466a170f-2a59-c2ef-b9e3-9bd9cb19a464.jpg"
	            },
	            {
	                "id": 19,
	                "name": "袁晓东",
	                "avatar": "http://123.56.154.187:8090/expert/201510/26/229d2b7a-3b36-5302-4fda-373d86decd3c.jpg"
	            }
	        ]
	    }
	}
	```
	
	- 达人商品
	
	```json
	url:	http://api.dogplanet.test/v1/c/product
	
	params:	{'id': 10139, 'expertId': 6}
	
	response:	
	{
	    "ret": 1001,
	    "product": {
	        "id": 10139,
	        "expertId": "6",
	        "name": "珊瑚礁潜水",
	        "price": 580,
	        "features": [
	            "珊瑚、鱼群",
	            "专业教练指导",
	            "美丽海底世界",
	            "PADI开放水域潜水员",
	            "专业指导",
	            "快速掌握",
	            "一星潜水员课程",
	            "专业教练指导",
	            "快速掌握潜水技巧",
	            "海底景观最完整",
	            "高端潜水体验",
	            "完美邂逅美丽海洋生物",
	            "珊瑚、鱼群",
	            "专业教练指导",
	            "美丽海底世界",
	            "一对一陪同",
	            "专业潜水装备",
	            "海底行走"
	        ],
	        "introduce": "<p><span style=\";font-family:宋体;font-size:16px\">珊瑚礁潜水是蜈支洲主要潜水项目，水下景观保存完好，珊瑚和热带</span><span style=\"font-family: 宋体;\">鱼群繁多，潜水时由浅入深。适合初次潜水</span><span style=\"font-family: 宋体;\">者。</span><span style=\"font-family: 宋体;\">穿上潜水服，经过培训后乘坐快艇到海上的一艘舶船上，然后背上氧</span><span style=\"font-family: 宋体;\">气瓶，戴上潜水镜，在潜水教练的陪伴下，直接从船上入水，教练带</span><span style=\"font-family: 宋体;\">领慢慢潜入较深的海底，根据游客的身体状态一般可潜</span><span style=\"font-family: 宋体;\">深度约</span><span style=\"font-family: 宋体;\">3—</span><span style=\"font-family: 宋体;\">8</span><span style=\"font-family: 宋体;\">米</span><span style=\"font-family: 宋体;\">，水下时间30分钟，7</span><span style=\"font-family: 宋体;\">-60</span><span style=\"font-family: 宋体;\">岁</span><span style=\"font-family: 宋体;\">且身体健康者可参加，儿童需1米2</span><span style=\"font-family: 宋体;\">以上</span><span style=\"font-family: 宋体;\">可参加，</span><span style=\"font-family: 宋体;\">收费580元/位</span></p><p><br/></p>",
	        "sliders": [],
	        "subs": [
	            {
	                "id": 10142,
	                "name": "考取潜水证（含3次上下岛门船票）",
	                "price": 3800,
	                "weekend_price": 3800,
	                "festival_price": 3800,
	                "introduction": "<p><span style=\";font-family:&#39;Times New Roman&#39;;font-size:16px\">PADI<span style=\"font-family:宋体\">开放水域潜水员是广受全球公认且受重视的潜水员等级，考取</span></span><span style=\"font-family: 宋体;\">PADI开放水域潜水员鉴定卡（证书）后，您就可以单独和潜伴去潜</span><span style=\"font-family: 宋体;\">水</span><span style=\"font-family: 宋体;\">，不需要潜水专业人士在一旁督导了。</span><span style=\"font-family: 宋体;\">含</span><span style=\"font-family: 宋体;\">3次上岛</span><span style=\"font-family: 宋体;\">门船票，</span><span style=\"font-family: 宋体;\">发放PADI潜水证</span><span style=\"font-family: 宋体;\">。第1天为理论课，讲解潜水</span><span style=\"font-family: 宋体;\">方面的知识以及设备的使用方法；第2天到泳池穿上潜水设备进行实</span><span style=\"font-family: 宋体;\">操培训；第3天开始到海里实操，全程有教练陪同，后期实操时根据</span><span style=\"font-family: 宋体;\">客人掌握情况，可自行练习，教练跟随。收费3800元/位</span></p><p><br/></p>",
	                "thumb": ""
	            },
	            {
	                "id": 10141,
	                "name": "考取潜水证（不含门船票）",
	                "price": 3500,
	                "weekend_price": 3500,
	                "festival_price": 3500,
	                "introduction": "<p><span style=\";font-family:宋体;font-size:16px\">此潜水办证是</span><span style=\";font-family:宋体;font-size:16px\">CMAS一星潜水员课程</span><span style=\";font-family:宋体;font-size:16px\">，</span><span style=\";font-family:宋体;font-size:16px\">一星级水肺潜水课程为基础级</span><span style=\"font-family: 宋体;\">潜水课程，其目的为指导潜水初学者具备最低限度之潜水常识与技</span><span style=\"font-family: 宋体;\">巧，以便在领导与监督时，能参加开放水域的潜水活动。</span><span style=\"font-family: 宋体;\">课程约为3至4天，第1天为理论课，讲解潜水方面的知识以及设备</span><span style=\"font-family: 宋体;\">的使用方法；第2天到泳池穿上潜水设备进行实操培训；第3天开始</span><span style=\"font-family: 宋体;\">到海里实操，全程有教练陪同，后期实操时根据客人掌握情况，可自</span><span style=\"font-family: 宋体;\">行练习，教练跟随。收费3500元/位</span></p><p><br/></p>",
	                "thumb": ""
	            },
	            {
	                "id": 10140,
	                "name": "VIP潜水",
	                "price": 980,
	                "weekend_price": 980,
	                "festival_price": 980,
	                "introduction": "<p><span style=\";font-family:宋体;font-size:16px\">VIP潜水区域是蜈支洲海域海底景观保存最为完整的地方，水下各种</span><span style=\"font-family: 宋体;\">珊瑚五彩斑斓，热带鱼群丰富多样</span><span style=\"font-family: 宋体;\">，下潜过程由浅入深</span><span style=\"font-family: 宋体;\">，是欣赏最美</span><span style=\"font-family: 宋体;\">海底世界和体验高端潜水的首选</span><span style=\"font-family: 宋体;\">潜水</span><span style=\"font-family: 宋体;\">深度</span><span style=\"font-family: 宋体;\">约</span><span style=\"font-family: 宋体;\">3-</span><span style=\"font-family: 宋体;\">10米，</span><span style=\"font-family: 宋体;\">间45分钟，全程VIP接待服务，并且赠送一次</span><span style=\"font-family: 宋体;\">性呼吸嘴，浴巾，寄存柜以及蛙鞋,7</span><span style=\"font-family: 宋体;\">-60</span><span style=\"font-family: 宋体;\">岁</span><span style=\"font-family: 宋体;\">且身体健康者可参</span><span style=\"font-family: 宋体;\">加，儿童1米2</span><span style=\"font-family: 宋体;\">以上可以参加。</span><span style=\"font-family: 宋体;\">收费980元/位</span></p><p><br/></p>",
	                "thumb": ""
	            },
	            {
	                "id": 10139,
	                "name": "珊瑚礁潜水",
	                "price": 580,
	                "weekend_price": 580,
	                "festival_price": 580,
	                "introduction": "<p><span style=\";font-family:宋体;font-size:16px\">珊瑚礁潜水是蜈支洲主要潜水项目，水下景观保存完好，珊瑚和热带</span><span style=\"font-family: 宋体;\">鱼群繁多，潜水时由浅入深。适合初次潜水</span><span style=\"font-family: 宋体;\">者。</span><span style=\"font-family: 宋体;\">穿上潜水服，经过培训后乘坐快艇到海上的一艘舶船上，然后背上氧</span><span style=\"font-family: 宋体;\">气瓶，戴上潜水镜，在潜水教练的陪伴下，直接从船上入水，教练带</span><span style=\"font-family: 宋体;\">领慢慢潜入较深的海底，根据游客的身体状态一般可潜</span><span style=\"font-family: 宋体;\">深度约</span><span style=\"font-family: 宋体;\">3—</span><span style=\"font-family: 宋体;\">8</span><span style=\"font-family: 宋体;\">米</span><span style=\"font-family: 宋体;\">，水下时间30分钟，7</span><span style=\"font-family: 宋体;\">-60</span><span style=\"font-family: 宋体;\">岁</span><span style=\"font-family: 宋体;\">且身体健康者可参加，儿童需1米2</span><span style=\"font-family: 宋体;\">以上</span><span style=\"font-family: 宋体;\">可参加，</span><span style=\"font-family: 宋体;\">收费580元/位</span></p><p><br/></p>",
	                "thumb": ""
	            },
	            {
	                "id": 10138,
	                "name": "堡礁潜水",
	                "price": 429,
	                "weekend_price": 429,
	                "festival_price": 429,
	                "introduction": "<p><span style=\";font-family:宋体;font-size:16px\">堡礁潜水主要以体验潜水为主，在岸边下水，水下有少量珊瑚和热带</span><span style=\"font-family: 宋体;\">鱼群。</span><span style=\"font-family: 宋体;\">报名后更换潜水服，经潜水培训后去堡礁潜水点，背上氧气瓶，带上</span><span style=\"font-family: 宋体;\">潜水镜，由教练一对一陪同完成潜水活动。</span><span style=\"font-family: 宋体;\">深度</span><span style=\"font-family: 宋体;\">约</span><span style=\"font-family: 宋体;\">3-6米，潜水时间</span><span style=\"font-family: 宋体;\">约</span><span style=\"font-family: 宋体;\">30分钟，</span><span style=\"font-family: 宋体;\">&nbsp;7-60岁且身体健康者可参加，儿童需1米2以上以上</span><span style=\"font-family: 宋体;\">可参加，收费429元/位</span></p><p><br/></p>",
	                "thumb": ""
	            },
	            {
	                "id": 10137,
	                "name": "海底漫步",
	                "price": 380,
	                "weekend_price": 380,
	                "festival_price": 380,
	                "introduction": "<p><span style=\";font-family:宋体;font-size:16px\">体验非同寻常的海底行走，探寻绚烂多彩的水下世界。不湿发，不背</span><span style=\"font-family: 宋体;\">深海潜水装备，只需要穿上泳衣，潜水鞋，带上头盔即可在水下的平</span><span style=\"font-family: 宋体;\">台上行走自如，潜水者可以用嘴和鼻子自然呼吸，</span><span style=\"font-family: 宋体;\">行走一圈约20分钟</span><span style=\"font-family: 宋体;\">，9-60岁且身体健康者可参加，儿童1米2以上</span><span style=\"font-family: 宋体;\">可参加。</span><span style=\"font-family: 宋体;\">收费380元/位</span></p><p><span style=\"font-family: 宋体;\"></span><br/></p>",
	                "thumb": ""
	            }
	        ]
	    }
	}
	```



## 5. 购买服务（产品）页面

### 5.1 购买服务页

* 说明

		1. 可购买服务为 services[date]	=>	[type => 20, price=>	2000]
		2. type //服务时间：10 早上		20 下午		30 晚上	50 全天（当早上、下午、晚上均可购买时，自动追加）
		3. price	//价格：整型
		4. 翻页，修改 date 参数即可
* url:
	
		/v1/c/expert/buy-service

* params:

		1. id	达人	id
		2. date	服务月（如 2015-09, 2015-10, 2015-08）
	
* response:
		
		1. ret: 1001    成功  0   无数据
		2. expert	=>	[
				'id'	=>	6,
				'services'	=>	[
					//30: 不可下单
					'2015-09-01' => 30,
					'2015-09-02' => 30,
					'2015-09-03' => 30,
					'2015-09-04' => 30,
					'2015-09-05' => 30,
					
					...
					
					'2015-09-13' => [
						['type'	=>	10,	price	=>	200],	//早
						['type'	=>	10,	price	=>	300],	//下午
						['type'	=>	30,	price	=>	1000],	//晚上
						['type'	=>	50,	price	=>	1500],	//全天
					],
					
					...
					
					'2015-09-23' => [
												['type'	=>	30,	price	=>	300],	//晚上
					],
					
					
					//....30 days
					//当日历键值为 30 时，表示不可购买（打点）；所有可购买的服务（点击展开），一维数组为其 服务时间 => 价格，
				],
				
				'servicePeople'	=>	5
			
			]

* sample:

	```json
	url:	http://api.dogplanet.test/v1/c/expert/buy-service
	
	params:	{"id": 6， "date": '2015-09'}
	
	response:
	{
	    "ret": 1001,
	    "expert": {
	        "id": 6,
	        "services": {
	            "2015-09-01": 30,
	            "2015-09-02": 30,
	            "2015-09-03": 30,
	            "2015-09-04": 30,
	            "2015-09-05": 30,
	            "2015-09-06": 30,
	            "2015-09-07": 30,
	            "2015-09-08": 30,
	            "2015-09-09": 30,
	            "2015-09-10": 30,
	            "2015-09-11": 30,
	            "2015-09-12": 30,
	            "2015-09-13": 30,
	            "2015-09-14": 30,
	            "2015-09-15": 30,
	            "2015-09-16": 30,
	            "2015-09-17": [
	                {
	                    "type": 10,
	                    "price": 200
	                },
	                {
	                    "type": 20,
	                    "price": 200
	                },
	                {
	                    "type": 30,
	                    "price": 2002
	                },
	                {
	                    "type": 50,
	                    "price": 2402
	                }
	            ],
	            "2015-09-18": 30,
	            "2015-09-19": 30,
	            "2015-09-20": 30,
	            "2015-09-21": 30,
	            "2015-09-22": 30,
	            "2015-09-23": [
	                {
	                    "type": 30,
	                    "price": 111
	                }
	            ],
	            "2015-09-24": 30,
	            "2015-09-25": 30,
	            "2015-09-26": 30,
	            "2015-09-27": 30,
	            "2015-09-28": 30,
	            "2015-09-29": 30,
	            "2015-09-30": 30
	        },
	        "servicePeople": 5
	    }
	}
	```



### 5.2 确认订单页

#### 5.2.1 达人推荐产品
##### 5.2.1.1 获取达人产品分类
* 说明:
	
	1. 获取达人产品的分类

* url:

		/v1/c/expert/product-types/
		
* params:
		
		1. id	达人 id

* response:
	
		1. ret: 1001    成功  0   无数据
		2. types	=>	[1, 2, 3]		//1 ~ 6 对应：[0 => '推荐', 1 => '美食', 2 => '住宿', 3 => '娱乐', 4 => '购物', 5 => '出行', 6 => '游玩']

* sample:

	```json
	url:	http://api.dogplanet.test/v1/c/expert/product-types?id=3
	
	params:	{"id": 3}
	
	response:
	{
	    "ret": 1001,
	    "types": [
	        "1",
	        "2",
	        "3"
	    ]
	}
	```
		

##### 5.2.1.2 获取达人推荐产品
* 说明

	1. 此处为确认订单页内，达人推荐产品的获取接口
	2. type 的值为 [5.2.1.1](#toc_28) 获取

* url:

		/v1/c/expert/share/

* params:
	
		1. id		//达人 id
		2. type		//0~6 （默认 0）	//[0 => '推荐', 1 => '美食', 2 => '住宿', 3 => '娱乐', 4 => '购物', 5 => '出行', 6 => '游玩']

* response: 

		1. ret: 1001    成功  0   无数据
		2. products => [
				'id'	=>	10010,
				'name'	=>	'滑水',
				'thumb'	=>	'@img-url',
				'price'	=>	200
			]

* sample:

	```json
	url:	http://api.dogplanet.test/v1/c/expert/share
	
	params:	{"id": 6， "type": 3}
	
	response:
	{
	    "ret": 1001,
	    "products": [
	        {
	            "id": 10110,
	            "name": "滑水",
	            "thumb": "http://123.56.154.187:8090/tou.jpg",
	            "price": 350
	        },
	        {
	            "id": 10115,
	            "name": "真人CS",
	            "thumb": "http://123.56.154.187:8090/product/201509/11/88461082-df16-7088-1a5d-95effb66eaf4.jpg",
	            "price": 80
	        },
	        {
	            "id": 10159,
	            "name": "多人水上自行车",
	            "thumb": "http://123.56.154.187:8090/product/201509/21/3db7f1a1-cd23-0e1d-3f66-fb6cdb683825.jpg",
	            "price": 140
	        }
	    ]
	}
	
	```
	

## 6. 订单部分
### 6.1 添加联系人页面
* 说明:

		1. 此接口功能为 获取常用联系人 
		2. 若由 立即支付页面 跳转过来（即未添加到购物车），之前页面填写的内容（日期、人数等信息）需在此页内容完善后，一并提交

* url:

		/user/get-contacts

* params:

		1. id	用户 id

* response:

		1. ret	1001	成功	0	无信息
		2. contacts	=>	[
				[
					'id'	=>	2139,
					'name'	=>	'陈成',
					'phone'	=>	'18600000000'
				],
				[
					'id'	=>	2149,
					'name'	=>	'陈成2',
					'phone'	=>	'18600000001'
				]
			]

* sample:

	```json
	{
	    "ret": 1001,
	    "contacts": [
	        {
	            "id": 2139,
	            "name": "吴蔚",
	            "phone": "18600502999"
	        },
	        {
	            "id": 2140,
	            "name": "小东",
	            "phone": "185000000123"
	        }
	    ]
	}
		
	```

### 6.2 生成订单
#### 6.2.1 直接支付 -> 生成订单
##### 6.2.1.1 产品订单
* 说明:
	
	1. **如果不是达人商品，达人 id(expertId) 为 0**
	2. 可以将数据包裹在一个命名为 json 的参数里，json 加密后 Get 传参；也可以直接走 Get or Post。（当有 json 参数存在时，其余 Get、Post 参数会失效）
	3. contactId 在用户选择已有联系人的时候作为此订单联系人的时候，追加传递（新联系人不需要传递）
	4. sample 中测试的数据需要联系后台修改数据，否则只可测试一次

* url:

		/v1/c/order/create-product
	
* params:
		
		1. userId	用户 id
		2. expertId	达人 id	(平台产品 填 0 或不填)
		3. num		数量
		4. contactName	联系人姓名
		5. contactPhone	联系人电话
		6. productId	产品 id
		7. date	日期
		8. contactId	*optional*: 当用户选择的是已有联系人的时候，传递此参数

		
* response:
	
		1. ret: 1001	成功		0	失败
		2. orderNum: 订单号

* sample:

	```json
	url:	http://api.dogplanet.test/v1/c/order/create-service
	
	params:
	{
		"userId": 1， 
		"expertId": 3,
		"num": 3,
		"contactName": "陈成",
		"contactPhone": "18600999999",
		"productId": 10117,
		"date": 2015-09-22
		"remark": "test~~~"
	} (Get)
	
	response:
	{
		"ret": 1001,
		"orderNum": "20151015165311505822"
	}
	```


##### 6.2.1.2 服务订单
* 说明

	1. 可以将数据包裹在一个命名为 json 的参数里，json 加密后 Get 传参；也可以直接走 Get or Post。（当有 json 参数存在时，其余 Get、Post 参数会失效）
	2. dates 与 types 例子：
		dates	=>	[2015-09-18, 2015-09-20]
		types	=>	[[10, 20], [30, 20]]
	3. 务必保证 types 是一个二维数组，且 types 与 dates 的元素数相同
	4. contactId 在用户选择已有联系人的时候作为此订单联系人的时候，追加传递（新联系人不需要传递）
	5. sample 中测试的数据需要联系后台修改数据，否则只可测试一次

* url:

		/v1/c/order/create-service

* params:

		1. userId	用户 id
		2. expertId	达人 id
		3. num		数量
		4. contactName	联系人姓名
		5. contactPhone	联系人电话
		6. dates	日历数组
		7. types	日历对应的 type 数组
		8. contactId	*optional*: 当用户选择的是已有联系人的时候，传递此参数

* response:
	
		1. ret: 1001	成功		0	失败
		2. orderNum: 订单号

* sample:

	```json
	url:	http://api.dogplanet.test/v1/c/order/create-service
	
	params:
	{
		"userId": 1， 
		"expertId": 3,
		"num": 3,
		"contactName": "陈成",
		"contactPhone": "18600999999",
		"dates[]": 2015-09-18
		"types[0][]": 20,
		"types[0][]": 10,
		"types[0][]": 30,
	} (Get)
	
	response:
	{
	    "ret": 1001,
	    "orderNum": "20151013183505449412"
	}
		
	```
	
	&
	
	```json
	url: http://api.dogplanet.test/v1/c/order/create-service
	
	params:
	{
		"userId": 1， 
		"expertId": 3,
		"num": 3,
		"contactName": "陈成",
		"contactPhone": "18600999999",
		"dates[]": 2015-09-18
		"types[0][]": 50,
	} (Get)
	
	response:
	{
	    "ret": 1001,
	    "orderNum": "20151013183505449412"
	}
	```



#### 6.2.2 购物车 -> 生成订单
* 说明:
	
	1. 下单时，会重新计算价格，会检查用户 id 是否与 给出的 cartId 匹配。
	2. 会先检查是不是所有的服务都可购买，若有不能购买的服务，会提示刷新页面。
	3. 生单过程中，有不能生成的订单（程序错误、数据错误等），会自动回滚，最后结果给出的订单号，即是成功生成的订单。（生单后，可去查询购物车数据，看看是否有添加失败的）
	4. 测试时，建议先 [清空购物车](#toc_44) 从 [5.1 购买服务页](#toc_25) 开始，找到有效的达人数据，然后 [添加购物车](#toc_40) 再生成订单，这样可以确保数据的有效性，避免重复测试。
	5. 由于测试需要做好准备，故 sample 给出的例子不能保证时效性，请自行测试。

* url:
		
		/v1/c/order/create-by-cart/

* params:
		
		1. userId	用户
		2. contactName	联系人姓名
		3. contactPhone	联系人电话
		4. cartIds	由购物车列表条目的主键 cartId 组成的一维数组

* response:
	
		1. ret: 1001	成功		0	失败
		2. orders	=>	[
				//订单号 orderNum 组成的一维数组
				"20151024152903276502",
				"20151024152903979462",
				"20151024152903480922"
			]

* sample:
	
	```json
	url:	http://api.dogplanet.test/v1/c/order/create-by-cart
	
	params:
	{
		"cartIds": 1,
		"cartIds": 2,
		"cartIds": 3,
		"cartIds": 4,
		"cartIds": 5,
		"cartIds": 6,
		"cartIds": 7,
		"userId": 1,
		"contactName": "陈成",
		"contactPhone": 18600502999
	}
	
	response:
	{
	    "ret": 1001,
	    "orders": [
	        "20151024154536457242",
	        "20151024154536262112",
	        "20151024154536064002"
	    ]
	}
	```



## 7. 支付
### 7.1 支付 API
* 说明:
	
	1. payType 为 **`支付宝 (1)` `微信 (2)` `银联 (3)`** 三选一
	2. 返回的 payUrl 为支付链接，页面直接跳转到此链接即可
	3. 测试期间，最大支付额度为 10 元（测试期间服务端锁定为 0.1 元）
	4. 支付完成后，自动跳转到 订单列表页

* url:
		
		/v1/c/pay
		
* params:
	
		1. orderNum	订单号
		2. payType	支付方式	1 支付宝（默认）	2 微信

* response:
	
		1. ret: 1001	成功		0	失败
		2. payUrl: 支付链接

* sample:
	
	```json
	url:	http://api.dogplanet.test/v1/c/pay
	
	params:	{orderNum: "20151013183505449412", "payType": 1}
	
	response:
	{
	    "ret": 0,
	    "payUrl": "http://api.ipaynow.cn?mhtOrderNo=20151013183505449412&mhtOrderName=wangwang_h5_20151013183505449412&mhtOrderAmt=45000&mhtOrderDetail=wangwang_h5_20151013183505449412&consumerId=1&consumerName=%E9%99%88%E6%88%90&notifyUrl=http%3A%2F%2F123.56.154.187%3A8080%2Fv1%2Fc%2Fpay%2Fnotify&frontNotifyUrl=http%3A%2F%2F123.56.154.187%3A8080%2Fv1%2Fc%2Fpay%2Ffront-notify&funcode=WP001&appId=1444792506369153&mhtOrderType=01&mhtCurrencyType=156&mhtOrderStartTime=20151017120941&mhtOrderTimeOut=3600&mhtCharset=UTF-8&deviceType=06&mhtSignType=MD5&mhtSignature=87a2d77b8e621c75a0253a86f91e6029"
	}
	
	```


## 8. 购物车
### 8.1 添加购物车
* 说明:
	
	1. **如果不是达人商品，达人 id(expertId) 为 0**
	2. 产品、服务的参数数据与 生成订单部分一致
	3. 支持将参数包裹在 json 内
	4. 产品数据合并逻辑：同一用户、同一达人、同一产品、同一日期（不同人数）
	5. 服务数据合并逻辑：同一用户、同一达人、同一天、同一人数（不同服务时间段）

* url:
		
		/v1/c/cart/add/

* params:
	
	- public
		
			1. addType	添加类型	0. 产品		1. 服务
			2. userId	用户 id
			3. expertId	达人 id
			4. num	人数
			5. price	结算价格（总价）
	
	- 产品
		
			1. productId	产品 id
			2. date	购买日期
	
	- 服务

			1. dates	日历数组
			2. types	日历对应 type 数组

* response:
	
		1. ret: 1001	成功		0	失败

* sample:
	
	- 产品

		```json
		url:	http://api.dogplanet.test/v1/c/cart/add
		
		params:	{
			"addType": 0,
			"userId": 1,
			"expertId": 6,
			"num": 5,
			"price": 2000,
			"date": 2015-09-20,
			"productId": 10119,
		} (Get)
		
		response:
		{
		    "ret": 1001,
		    "msg": "添加成功"
		}
		```
		
	- 服务
		
		```json
		url:	http://api.dogplanet.test/v1/c/cart/add
		
		params:	{
			"addType": 1,
			"userId": 1,
			"expertId": 6,
			"num": 5,
			"price": 200,
			"dates[]": 2015-10-11,
			"types[0][]": 10,
			"types[0][]": 20,
		} (Get)
		
		response:
		{
		    "ret": 1001,
		    "msg": "添加成功"
		}
		```


### 8.2 购物车列表
* 说明:
	
	1. 服务数据整合规则：相同达人、相同人数
	2. 服务整合产品规则：达人相同、**产品出行时间位于服务商品时间段内**
	3. 推荐达人个数：10 个
	4. 每条购物车数据中伴随一个 invalid 参数，**为 false 时，表示可以购买，为 true 时表示不可以购买**

* url:

		/v1/c/cart/list/

* params:
	
		1. userId	用户 id
		2. tk 用户的 token

* response:
	
	- 有产品时（无推荐达人）
		
			1. ret: 1001	成功		0	失败
			2. carts => [
				[
					"services"	=>	[
						[
							"cartId" => 5,
							"expertId" =>	6,
							"dates"	=>	2015-10-11,
							"types"	=>	["10", "20"],
							"num"	=>	5,
							"avatar"	=>	"@img-url",
							"price"	=>	200,
							"status"	=>	30
						],
						[
							"cartId" => 5,
							"expertId" =>	6,
							"dates"	=>	2015-10-12,
							"types"	=>	["10", "20"],
							"num"	=>	5,
							"avatar"	=>	"@img-url",
							"price"	=>	200,
							"status"	=>	30
						]
					],
					
					"products"	=>	[
						[]
					]
					"invalid"	=>	true,	//不可购买
				],
				[
					"services"	=>	[],
					"products"	=>	[
						[
							"cartId"	=>	3,
							"productId"	=>	10119,
							"productName"	=>	"珊瑚家庭豪华海景套房（二房一厅）",
							"expertId"	=>	6,
							"num"	=>	5,
							"date"	=>	2015-09-20,
							"price"	=>	26500,
							"thumb"	=>	"@img-url"
						],
						[
							"cartId"	=>	5,
							"productId"	=>	10120,
							"productName"	=>	"珊瑚家庭豪华海景套房",
							"expertId"	=>	6,
							"num"	=>	5,
							"date"	=>	2015-09-20,
							"price"	=>	26500,
							"thumb"	=>	"@img-url"
						],
						
					]
					"invalid"	=>	false	//可以购买
				],
			]

	- 无产品时（只有服务）

			1. ret: 1001	成功		0	失败
			2. carts => [
				[
					"services"	=>	[...],
					"products"	=>	[],							"invalid"	=>	xxx(bool)
				],
				[
					"services"	=>	[...],
					"products"	=>	[],
					"invalid"	=>	xxx(bool)
				]

				
			]
			3. experts	=>	[
				[
					'id'    => 124,
					'name'  =>  '陈成',
					'stars' => 5,       //星级
					'avatar'    =>  '@img-url',
					'features'  =>  ['打酱油', '吃饭'],
					'services'  =>  [       
					//10: 全天可下单 20: 半天可下单   30: 不可下单
						'2015-09-19' => 30
						'2015-09-20' => 30
						'2015-09-21' => 30
						'2015-09-22' => 30
						'2015-09-23' => 20
						'2015-09-24' => 30
						'2015-09-25' => 30
					]
					'introduce' => 'why so serious',
				]
				,
				[
					'id'    => 6,
					'name'  =>  '陈成2',
					'stars' => 1,       //星级
					'avatar'    =>  '@img-url',
					'features'  =>  ['吃饭'],
					'services'  =>  [       
					//10: 全天可下单 20: 半天可下单   30: 不可下单
						'2015-09-19' => 30
						'2015-09-20' => 30
						'2015-09-21' => 30
						'2015-09-22' => 30
						'2015-09-23' => 20
						'2015-09-24' => 30
						'2015-09-25' => 30
					]
					'introduce' => 'why so serious',
				]
			]
* sample:
	
	- 有产品时

		```json
		url:	http://api.dogplanet.test/v1/c/cart/list?userId=1
		
		params:	{"urserId": 1}
		
		response:
		{
		    "ret": 1001,
		    "carts": [
		        {
		            "services": [
		                {
		                    "cartId": 1,
		                    "expertId": 6,
		                    "date": "2015-10-11",
		                    "types": [
		                        "10",
		                        "20"
		                    ],
		                    "num": 5,
		                    "avatar": "",
		                    "price": 200,
		                    "status": 30
		                },
		                {
		                    "cartId": 2,
		                    "expertId": 6,
		                    "date": "2015-10-12",
		                    "types": [
		                        "10"
		                    ],
		                    "num": 5,
		                    "avatar": "",
		                    "price": 200,
		                    "status": 30
		                },
		                {
		                    "cartId": 3,
		                    "expertId": 6,
		                    "date": "2015-10-13",
		                    "types": [
		                        "50"
		                    ],
		                    "num": 5,
		                    "avatar": "",
		                    "price": 200,
		                    "status": 30
		                },
		                {
		                    "cartId": 15,
		                    "expertId": 6,
		                    "date": "2015-10-19",
		                    "types": [
		                        "10",
		                        "20"
		                    ],
		                    "num": 5,
		                    "avatar": "",
		                    "price": 200,
		                    "status": 30
		                },
		                {
		                    "cartId": 14,
		                    "expertId": 6,
		                    "date": "2015-10-20",
		                    "types": [
		                        "50"
		                    ],
		                    "num": 5,
		                    "avatar": "",
		                    "price": 200,
		                    "status": 30
		                },
		                {
		                    "cartId": 16,
		                    "expertId": 6,
		                    "date": "2015-10-25",
		                    "types": [
		                        "50"
		                    ],
		                    "num": 5,
		                    "avatar": "",
		                    "price": 200,
		                    "status": 30
		                }
		            ],
		            "products": [
		                {
		                    "cartId": "18",
		                    "productId": "10119",
		                    "productName": "珊瑚家庭豪华海景套房（二房一厅）",
		                    "expertId": "6",
		                    "num": "5",
		                    "date": "2015-10-13",
		                    "price": 26500,
		                    "thumb": "http://123.56.154.187:8090/product/201508/24/f3034b88-c93c-ffa7-ccbb-0f417364a626.jpg"
		                }
		            ],
		            "invalid": true
		        },
		        {
		            "services": [
		                {
		                    "cartId": 4,
		                    "expertId": 3,
		                    "date": "2015-10-11",
		                    "types": [
		                        "10",
		                        "20"
		                    ],
		                    "num": 5,
		                    "avatar": "http://123.56.154.187:8090/expert/201509/30/466a170f-2a59-c2ef-b9e3-9bd9cb19a464.jpg",
		                    "price": 200,
		                    "status": 30
		                }
		            ],
		            "products": [],
		            "invalid": true
		        },
		        {
		            "services": [],
		            "products": [
		                {
		                    "cartId": "5",
		                    "productId": "10119",
		                    "productName": "珊瑚家庭豪华海景套房（二房一厅）",
		                    "expertId": "2",
		                    "num": "5",
		                    "date": "2015-09-20",
		                    "price": 26500,
		                    "thumb": "http://123.56.154.187:8090/product/201508/24/f3034b88-c93c-ffa7-ccbb-0f417364a626.jpg"
		                }
		            ],
		            "invalid": false
		        },
		        {
		            "services": [],
		            "products": [
		                {
		                    "cartId": "7",
		                    "productId": "10120",
		                    "productName": "珊瑚豪华池畔房（大/双）",
		                    "expertId": "5",
		                    "num": "5",
		                    "date": "2015-09-20",
		                    "price": 8500,
		                    "thumb": "http://123.56.154.187:8090/product/201508/24/54cdc8fa-b6d1-b4f2-05c1-b45bc56448de.jpg"
		                }
		            ],
		            "invalid": false
		        },
		        {
		            "services": [],
		            "products": [
		                {
		                    "cartId": "6",
		                    "productId": "10119",
		                    "productName": "珊瑚家庭豪华海景套房（二房一厅）",
		                    "expertId": "3",
		                    "num": "5",
		                    "date": "2015-09-20",
		                    "price": 26500,
		                    "thumb": "http://123.56.154.187:8090/product/201508/24/f3034b88-c93c-ffa7-ccbb-0f417364a626.jpg"
		                }
		            ],
		            "invalid": false
		        }
		    ]
		}
		```
	
	- 无产品时

		```json
		url:	http://api.dogplanet.test/v1/c/cart/list?userId=2
		
		params:	{"urserId": 2}
		
		response:
		{
		    "ret": 1001,
		    "carts": [
		        {
		            "services": [
		                {
		                    "cartId": 10,
		                    "expertId": 3,
		                    "dates": "2015-10-13",
		                    "types": [
		                        "50"
		                    ],
		                    "num": 5,
		                    "avatar": "http://123.56.154.187:8090/expert/201509/30/466a170f-2a59-c2ef-b9e3-9bd9cb19a464.jpg",
		                    "price": 1089,
		                    "status": 10
		                },
		                {
		                    "cartId": 9,
		                    "expertId": 3,
		                    "dates": "2015-10-11",
		                    "types": [
		                        "10",
		                        "20"
		                    ],
		                    "num": 5,
		                    "avatar": "http://123.56.154.187:8090/expert/201509/30/466a170f-2a59-c2ef-b9e3-9bd9cb19a464.jpg",
		                    "price": 200,
		                    "status": 30
		                }
		            ],
		            "products": [],
		            "invalid": false
		        },
		        {
		            "services": [
		                {
		                    "cartId": 8,
		                    "expertId": 6,
		                    "dates": "2015-10-11",
		                    "types": [
		                        "10"
		                    ],
		                    "num": 5,
		                    "avatar": "",
		                    "price": 200,
		                    "status": 30
		                }
		            ],
		            "products": [],
		            "invalid": false
		        }
		    ],
		    "experts": [
		        {
		            "id": 18,
		            "name": "袁晓东",
		            "stars": 0,
		            "avatar": "",
		            "floorPrice": 23,
		            "introduce": "不能说的秘密，你还跟你您老米诺LOL哦破偷偷你昨天定到头来我们的人的人的人的人得得滴哦JOJO你OK诺优诺哦solo1图谋哦了哦咯JOJO哦咯JOJO女女女女MSN头目你门口你木木木周末女女女女MSN头目外婆咯咯哦破LOL温柔哦咯",
		            "features": [
		                "夜晚潜水",
		                "小木屋",
		                "婚纱摄影",
		                "沙滩烧烤",
		                "冲浪"
		            ],
		            "services": {
		                "2015-10-20": 30,
		                "2015-10-21": 30,
		                "2015-10-22": 30,
		                "2015-10-23": 30,
		                "2015-10-24": 30,
		                "2015-10-25": 30,
		                "2015-10-26": 30
		            }
		        },
		        {
		            "id": 11,
		            "name": "ww",
		            "stars": 0,
		            "avatar": "http://123.56.154.187:8090/expert/201509/30/fbb42617-5abe-6f50-d686-2cd380ebd7af.jpg",
		            "floorPrice": 1,
		            "introduce": "wwefoiwhefowihefoiwheofihwoiefhowjeodiwoienfoiwehfowiehfoiweofmwoemfwoeifnhwoeihfowehfowhiefoiwhefwe",
		            "features": [
		                "woeif",
		                "woei",
		                "www",
		                "wwww"
		            ],
		            "services": {
		                "2015-10-20": 10,
		                "2015-10-21": 10,
		                "2015-10-22": 10,
		                "2015-10-23": 10,
		                "2015-10-24": 10,
		                "2015-10-25": 10,
		                "2015-10-26": 10
		            }
		        },
		        {
		            "id": 2,
		            "name": "吴蔚",
		            "stars": 0,
		            "avatar": "http://123.56.154.187:8090/expert/201509/23/00ac3b6d-de2b-df66-8e7d-e172e7bd0075.jpg",
		            "floorPrice": 100,
		            "introduce": "这里是个人简介",
		            "features": [
		                "哈哈",
		                "22",
		                "33"
		            ],
		            "services": {
		                "2015-10-20": 30,
		                "2015-10-21": 30,
		                "2015-10-22": 30,
		                "2015-10-23": 30,
		                "2015-10-24": 30,
		                "2015-10-25": 30,
		                "2015-10-26": 30
		            }
		        },
		        {
		            "id": 4,
		            "name": "袁晓东",
		            "stars": 0,
		            "avatar": "http://123.56.154.187:8090/expert/201510/03/f6d0c73e-bab1-e04d-5f09-129ae8f29d51.jpg",
		            "floorPrice": 1,
		            "introduce": "大家好，我是小东，来自内蒙现在长期居住在三亚，喜欢三亚这里的一切，我是做互联网的，来到三亚之后开始学习冲浪啦咯啦咯啦咯",
		            "features": [
		                "百度",
		                "哇哈哈",
		                "知道",
		                "弄了"
		            ],
		            "services": {
		                "2015-10-20": 10,
		                "2015-10-21": 10,
		                "2015-10-22": 30,
		                "2015-10-23": 10,
		                "2015-10-24": 10,
		                "2015-10-25": 10,
		                "2015-10-26": 30
		            }
		        },
		        {
		            "id": 6,
		            "name": "陈成",
		            "stars": 0,
		            "avatar": "",
		            "floorPrice": 111,
		            "introduce": "这个人很吊",
		            "features": [
		                "潜水"
		            ],
		            "services": {
		                "2015-10-20": 30,
		                "2015-10-21": 30,
		                "2015-10-22": 30,
		                "2015-10-23": 30,
		                "2015-10-24": 30,
		                "2015-10-25": 30,
		                "2015-10-26": 30
		            }
		        },
		        {
		            "id": 1,
		            "name": "",
		            "stars": 0,
		            "avatar": "",
		            "floorPrice": 100,
		            "introduce": "",
		            "features": [],
		            "services": {
		                "2015-10-20": 30,
		                "2015-10-21": 30,
		                "2015-10-22": 30,
		                "2015-10-23": 30,
		                "2015-10-24": 30,
		                "2015-10-25": 30,
		                "2015-10-26": 30
		            }
		        },
		        {
		            "id": 3,
		            "name": "老高",
		            "stars": 0,
		            "avatar": "http://123.56.154.187:8090/expert/201509/30/466a170f-2a59-c2ef-b9e3-9bd9cb19a464.jpg",
		            "floorPrice": 2,
		            "introduce": "哈哈，我来了",
		            "features": [],
		            "services": {
		                "2015-10-20": 10,
		                "2015-10-21": 10,
		                "2015-10-22": 30,
		                "2015-10-23": 30,
		                "2015-10-24": 10,
		                "2015-10-25": 30,
		                "2015-10-26": 30
		            }
		        },
		        {
		            "id": 5,
		            "name": "酱油",
		            "stars": 0,
		            "avatar": "",
		            "floorPrice": 0,
		            "introduce": "",
		            "features": [],
		            "services": {
		                "2015-10-20": 30,
		                "2015-10-21": 30,
		                "2015-10-22": 30,
		                "2015-10-23": 30,
		                "2015-10-24": 30,
		                "2015-10-25": 30,
		                "2015-10-26": 30
		            }
		        },
		        {
		            "id": 17,
		            "name": "",
		            "stars": 0,
		            "avatar": "",
		            "floorPrice": 0,
		            "introduce": "",
		            "features": [],
		            "services": {
		                "2015-10-20": 30,
		                "2015-10-21": 30,
		                "2015-10-22": 30,
		                "2015-10-23": 30,
		                "2015-10-24": 30,
		                "2015-10-25": 30,
		                "2015-10-26": 30
		            }
		        },
		        {
		            "id": 10,
		            "name": "吴蔚",
		            "stars": 0,
		            "avatar": "http://123.56.154.187:8090/expert/201509/23/00ac3b6d-de2b-df66-8e7d-e172e7bd0075.jpg",
		            "floorPrice": 200,
		            "introduce": "这里是个人简介",
		            "features": [
		                "哈哈",
		                "22",
		                "33"
		            ],
		            "services": {
		                "2015-10-20": 30,
		                "2015-10-21": 30,
		                "2015-10-22": 30,
		                "2015-10-23": 30,
		                "2015-10-24": 30,
		                "2015-10-25": 30,
		                "2015-10-26": 30
		            }
		        }
		    ]
		}		
		```


### 8.3 删除（清空）购物车内容
#### 8.3.1 删除购物车内容
* 说明:
	
		1. 单条删除
	
* url:
	
		/v1/c/cart/delete/

* params:
		
		1. cartId

* response:
		
		1. ret: 1001	成功		0	失败

#### 8.3.2 清空购物车
* 说明:
	
		1. 清空购物车

* url:
		
		1. /v1/c/cart/delete-all/

* params:
		
		1. userId

* response:
		
		1. ret: 1001	成功		0	失败

* sample:

	```json
	url:	http://api.dogplanet.test/v1/c/cart/delete-all?userId=3
	
	params:	{"userId": 3}
	
	response:	
	{
	    "ret": 1001,
	    "msg": "删除成功"
	}
	```

## 9. 个人中心
### 9.1 订单部分
#### 9.1.1 订单列表
* 说明:
	
	1. 获取用户订单列表

* url:
	
		/v1/c/user/orders/
		
* params:

		1. userId	用户 id
		2. tk 用户的 token

* response:
		
		1. ret: 1001	成功		0	失败
		2. orders	=>	[
			[
				"orderNum"	=>	20151013183505449412,
				"type"	=>	"达人服务",
				"price"	=>	450,
				"createTime"	=>	2015-10-13 18:35:05,
				"status"	=>	"待支付"
			],
			[
				"orderNum"	=>	20151015165311505822,
				"type"	=>	"达人商品",
				"price"	=>	16500,
				"createTime"	=>	2015-10-15 16:53:11,
				"status"	=>	"待支付"
			],
			[
				"orderNum"	=>	20151013183833506832,
				"type"	=>	"达人服务",
				"price"	=>	100,
				"createTime"	=>	2015-10-13 18:38:33,
				"status"	=>	"待支付"
			],
		]
		

* sample:
	
	```json
	url:	http://api.dogplanet.test/v1/c/user/orders?userId=1
	
	params:	{"userId": 1}
	
	response:
	{
	    "ret": 1001,
	    "orders": [
	        {
	            "orderNum": "20151013183505449412",
	            "type": "达人服务",
	            "price": 450,
	            "createTime": "2015-10-13 18:35:05",
	            "status": "待支付"
	        },
	        {
	            "orderNum": "20151013183833506832",
	            "type": "达人服务",
	            "price": 100,
	            "createTime": "2015-10-13 18:38:33",
	            "status": "已支付"
	        },
	        {
	            "orderNum": "20151013184739636012",
	            "type": "达人服务",
	            "price": 450,
	            "createTime": "2015-10-13 18:47:39",
	            "status": "已支付"
	        },
	        {
	            "orderNum": "20151015141902593892",
	            "type": "达人服务",
	            "price": 300,
	            "createTime": "2015-10-15 14:19:02",
	            "status": "待支付"
	        },
	        {
	            "orderNum": "20151015144141749192",
	            "type": "达人商品",
	            "price": 16500,
	            "createTime": "2015-10-15 14:41:41",
	            "status": "待支付"
	        },
	        {
	            "orderNum": "20151015165311505822",
	            "type": "达人商品",
	            "price": 16500,
	            "createTime": "2015-10-15 16:53:11",
	            "status": "待支付"
	        },
	        {
	            "orderNum": "20151015170804116812",
	            "type": "达人商品",
	            "price": 16500,
	            "createTime": "2015-10-15 17:08:04",
	            "status": "待支付"
	        },
	        {
	            "orderNum": "20151015170806016532",
	            "type": "达人商品",
	            "price": 16500,
	            "createTime": "2015-10-15 17:08:06",
	            "status": "待支付"
	        },
	        {
	            "orderNum": "20151020185037331292",
	            "type": "达人服务",
	            "price": 350,
	            "createTime": "2015-10-20 18:50:37",
	            "status": "待支付"
	        },
	        {
	            "orderNum": "20151021134049832892",
	            "type": "达人服务",
	            "price": 133,
	            "createTime": "2015-10-21 13:40:49",
	            "status": "已支付"
	        }
	    ]
	}
	```

#### 9.1.2 订单详情
* 说明:
		
	1. **buttonStatus** 参数，用来控制订单在不同状态，应该显示的 `按钮`。
		- `buttonStatus: 0` **不显示任何按钮**
		- `buttonStatus: 10` 显示 **`立即支付`**([api](#toc_38)) 与 **`取消订单`** ([api](#toc_50))
		- `buttonStatus: 20` 显示 **`取消订单`** ([api](#toc_50))
		- `buttonStatus: 30` 显示 **`申请退款`**([api](#toc_50) 同取消订单)
		- `buttonStatus: 40` 显示 **`确认取消`**([api](#toc_51))（此时由达人发起了退款请求，需要用户确认）
	
	2. 如果是达人商品，会追加 达人信息 `expert` 字段

* url:
	
		/v1/c/order/detail

* params:
		
		1. userId	用户 id
		2. orderNum	订单号

* response:
		
		1. ret: 1001	成功		0	失败
		2. order	=>	[
			"primaryOrder"	=>	[
				"orderNum"	=>	20151013183505449412,
				"contactName"	=>	"陈成",
				"contactPhone"	=>	18600502911,
				"remark"	=>	"",
				"price"	=>	450,
				"createTime"	=>	2015-10-13 18:35:05,
				"status"	=>	"待支付"，
			],
			
			"subOrders"	=>	[
				[
					"date"	=>	"2015-09-18 全天",
					"name"	=>	"达人服务",
					"price"	=>	450,
					"status"	=>	"待支付",	
				],
				
				//...购物车订单会有多条 subOrder
				[
					//...
				]
			]
		]
		3. buttonStatus	=> 5
		
		4. expert	=>	[
            "id"	=>	6,
            "name"	=>	"陈成",
            "stars"	=>	0,
            "avatar"	=>	"http://img3.dogplanet.test/expert/201509/30/466a170f-2a59-c2ef-b9e3-9bd9cb19a464.jpg",
            "province"	=>	null,
            "city"	=>	null,
            "idCard"	=>	1,
            "tel"	=>	18600500000,
            "mail"	=>	1,
            "authInfo"	=>	0,
            "background"	=>	"",
            "introduce"	=>	"这个人很吊",
            "features"	=>	[]
		]

* sample:

	```json
	url:	http://api.dogplanet.test/v1/c/order/detail?userId=10&orderNum=20151021134551141702
	
	params:	{"userId": 10, "orderNum":20151021134551141702}
	
	response:
	{
	    "ret": 1001,
	    "order": {
	        "primaryOrder": {
	            "orderNum": "20151021134551141702",
	            "contactName": "lala",
	            "contactPhone": "18600502922",
	            "remark": "",
	            "price": 133,
	            "createTime": "2015-10-21 13:45:51",
	            "status": "已支付"
	        },
	        "subOrders": [
	            {
	                "date": "2015-10-27 上午",
	                "name": "达人服务",
	                "num": "3",
	                "price": 133,
	                "status": "待完成"
	            }
	        ],
	        "buttonStatus": 40
	    }
	}
	```

#### 9.1.3 评论订单（仅限 **服务订单**）
* 说明:
		
		1. 添加时，服务端会对 userId, orderNum, expertId 进行匹配验证，若不合格（订单号不正确、不是服务订单或者用户、达人不匹配等），添加会失败。
		2. 每条服务订单仅限评论一次。（sample 测试可能会返回，“已评论”，可找寻别的服务订单测试）

* url:

		/v1/c/user/add-comment/

* params:

		1. userId	用户 id
		2. expertId	达人 id
		3. orderNum	订单号
		4. star	星级（1 ~ 5）
		5. content	评论内容

* response:
	
		1. ret: 1001	成功		0	失败

* sample:

	```json
	url:	http://api.dogplanet.test/v1/c/user/add-comment?userId=1&expertId=3&orderNum=20151013183505449412&star=5&content=很不错~~~
	
	params:	
	{
		"userId": 1,
		"expertId": 3,
		"orderNum": 20151013183505449412,
		"star": 5,
		"content": 很不错~~~
	}
	
	response:
	{
	    "ret": 1001,
	    "msg": "评论成功"
	}
	```


#### 9.1.4 取消订单
* 说明:

* url:
		
		/v1/c/order/cancel/

* params:
		
		1. userId	用户 id
		2. orderNum	订单号

* response:

		1. ret: 1001	成功		0	失败

* sample
	
	```json
	url:	http://api.dogplanet.test/v1/c/order/cancel?userId=1&orderNum=20151013183505449412
	
	params:	{"userId": 1, "orderNum": 20151013183505449412}
	
	response:
	{
	    "ret": 1001,
	    "msg": "取消成功"
	}
	```
	

#### **9.1.5 操作订单**
* 说明:
	
	1. 对订单进行的一些操作（目前仅有 “确认取消”）。
	2. type 操作类别的相应按钮（目前仅有 `确认取消` 按钮）
		
		`1	=>	"确认取消"`（当服务订单状态为 "达人取消时候"，即 `buttonStatus=40` 时显示的按钮）
	
* url:
	
		1. /v1/c/order/operate/

* params:
	
		1. userId	用户 id
		2. orderNum	订单号
		3. type	操作类别（默认 1）

* response:
		
		1. ret: 1001	成功		0	失败

* sample:
	
	```json
	url:	http://api.dogplanet.test/v1/c/order/operate?userId=10&orderNum=20151021134551141702
	
	params:	{"userId": 10, "orderNum":20151021134551141702}
	
	response:
	{
	    "ret": 1001,
	    "msg": "确认成功"
	}
	```
	
	
### 9.2 用户信息部分
#### 9.2.1 修改密码
* 说明:

* url:
		
		/v1/c/user/change-pwd/

* params:
		
		1. userId	用户 id
		2. oldPassword	旧密码
		3. password	新密码
		4. password2	重复新密码

* response:

		1. ret: 1001	成功		0	失败

* sample:
	
	```json
	url:	http://api.dogplanet.test/v1/c/user/change-pwd/
	
	params:
	{
		"userId":	1,
		"oldPassword": 123456,
		"password": 123456,
		"password2": 123456
	}
	
	response:
	{
	    "ret": 1001,
	    "msg": "修改成功"
	}
	```
		
		

## 10. 达人商城
* 说明:
		
	1. api 同 [5.2.2 达人推荐产品](#toc_29)，不同点（均为增加参数）：
		- 增加了一个 **shop( `true` or `false` )** 参数，用来判断是否需要追加达人相关数据（商城页需要追加）
		- **增加了两个参数，用来分页**：
			* page	(\*optional\*	默认 0 )
			* pageSize	(\*optional\*	默认 10 )

			
	3. 推荐产品 **暂固定为 10 个**，其余产品可根据分类及页码参数获取

* url:
	
		/v1/c/expert/share/
	
* params 
	
		1. id       //达人 id
		2. type     //0~6 （默认 0）    //[0 => '推荐', 1 => '美食', 2 => '住宿', 3 => '娱乐', 4 => '购物', 5 => '出行', 6 => '游玩']
		3. shop	商城标识 True(bool)
		4. page	(*optional*	默认 0 )
		5. pageSize	(*optional*	默认 10 )

* response: [@see	5.2.2...](#toc_29)

* sample:
	
	```json
	url: http://api.dogplanet.cn/v1/c/expert/share/?shop=true&id=2&type=0&_=1447648302247
	
	params: {shop: true, id: 2, type: 0, }
	
	response:
	{
	    "ret": 1001,
	    "products": [
	        {
	            "id": 14,
	            "name": "拖伞",
	            "thumb": "http://img5.dogplanet.cn/product/201510/31/f3629323-c16a-64e7-cb9f-280e6f37b97b.jpg",
	            "price": 320
	        },
	        {
	            "id": 15,
	            "name": "海岛潜水",
	            "thumb": "http://img5.dogplanet.cn/product/201510/31/cd790fda-30d6-a002-a7a2-9d6f85f72bee.jpg",
	            "price": 380
	        },
	        {
	            "id": 16,
	            "name": "香蕉船",
	            "thumb": "http://img5.dogplanet.cn/product/201510/31/51fbbff8-2c3d-860e-7255-48f255a2120b.jpg",
	            "price": 100
	        },
	        {
	            "id": 17,
	            "name": "海钓",
	            "thumb": "http://img5.dogplanet.cn/product/201510/31/ef88d0f8-2779-eb95-101c-3ae01bb12264.jpg",
	            "price": 100
	        },
	        {
	            "id": 18,
	            "name": "摩托艇",
	            "thumb": "http://img5.dogplanet.cn/product/201510/31/76a34a16-bd72-f982-b2d4-4289296d2052.jpg",
	            "price": 179
	        },
	        {
	            "id": 19,
	            "name": "快艇观光",
	            "thumb": "http://img5.dogplanet.cn/product/201510/31/58b36100-072b-bf29-544f-65366f9174c0.jpg",
	            "price": 180
	        }
	    ],
	    "expert": {
	        "id": 2,
	        "name": "袁晓东",
	        "stars": 0,
	        "avatar": "http://img5.dogplanet.cn/expert/201511/03/e71919c8-b8c4-31a5-6d40-81e5ee3cc35c.jpg",
	        "province": null,
	        "city": null,
	        "idCard": 1,
	        "tel": "13466628444",
	        "mail": azlarsin@gmail.com,
	        "authInfo": 0,
	        "background": "http://img5.dogplanet.cn/expert/201511/03/d9c3c890-ea11-823f-c37f-7807bd9e9e11.jpg",
	        "introduce": "哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多哇哈哈养乐多",
	        "features": [
	            "冲浪",
	            "美女",
	            "深海潜水",
	            "海边烧烤",
	            "沙滩"
	        ]
	    }
	}
	```
	


## 11. C 端临时方案
### 11.1 单独生成产品订单
* 说明: 
	1. 无需注册
	2. 仅支持达人产品（即 携带 `expertId` 参数）
	3. 需要验证码
	4. 参数与 [6.2.1.1 单独生成产品订单...](#toc_34) 基本相同
		- `userId` 填写任意整数
		- `exertId` 必填
	5. 请求 [9.1.3 订单详情](#toc_48) 时 `userId` 填写 **`99999`**

* url:
	
		1. /v1/c/order/create-product-tmp


* params & response & sample: **[@see	6.2.1.1 单独生成产品订单...](#toc_34)**

### 11.2 通过手机获取订单详情
* 说明
	1. 由于现在版本下单方式为手机验证码下单，**生成订单后为该手机生成用户**，故获取订单详情的时候，userId 为 9999 的请求会抓不到数据，所以提供此接口

* url:

		1. /v1/c/order/detail-by-phone

* params:
		
		1. orderNum
		2. phone

* response & sample: [@see 9.1.2 订单详情](#toc_48)



## 12. 一些追加接口
### 12.1 获取用户购物车数量
* 说明:
	
	1. 获取用户订单列表

* url:
	
		/v1/c/user/get-cart-count/
		
* params:

		1. userId	用户 id
		2. tk 用户的 token

* response:
		
		1. ret: 1001	成功		0	失败
		2. count	=>	5


### 12.2 获取个人中心推荐达人
* 说明:
	
	1. 获取用户订单列表

* url:
	
		/v1/c/user/experts/
		
* params:

		1. userId	用户 id
		2. tk 用户的 token

* response:
		
		1. ret: 1001	成功		0	失败
		2. experts	=>	[
			[@expert],
			[@expert]
		]


### 12.3 通过验证码实现自动注册/登录功能
* 说明:
	
	1. 获取用户订单列表

* url:
	
		/v1/c/user/reg-by-client/
		
* params:

		1. phone
		2. name
		3. code

* response:
		
		1. ret: 1001	成功		0	失败
		2. user	=>	[
			@user-info
		]
		
		
### 12.4 单独取消子订单
* 说明:
	
	1. 单独取消子订单接口
	2. 服务订单不可用

* url:
	
		/v1/c/order/cancel-sub/
		
* params:

		1. userId
		2. tk
		3. orderNum
		4. subId

* response:
		
		1. ret: 1001	成功		0	失败


### 12.5 打包产品相关
#### 12.5.1 打包产品详情页
* 说明:
	
	1. 获取打包产品详情页

* url:
	
		/v1/c/product/pack/
		
* params:

		1. id	打包的 package id

* response:
		
		1. ret: 1001	成功		0	失败
		2. package	=>	[]

* sample:

	```json
	url:	http://api.dogplanet.dev/v1/c/product/pack/
	
	params:	
	{
		"id": 1,
	}
	
	response:
	{
	    "ret": 1001,
	    "package": {
	        "expertId": 30,
	        "price": 2999,
	        "products": [
	            {
	                "id": 64,
	                "expertId": 30,
	                "name": "VIP潜水",
	                "price": 980,
	                "features": [
	                    "形态迥异的各类珊瑚群",
	                    "色彩缤纷的热带鱼",
	                    "专业教练指导",
	                    "蜈支洲最佳潜点",
	                    "感受潜水乐趣",
	                    "专业潜水装备",
	                    "探索缤纷海底世界"
	                ],
	                "shortComment": "高端潜水体验，更美海底风光",
	                "introduce": "<p><span style=\"font-size: 14px;\">以观赏形态迥异的各类珊瑚群及色彩缤纷的热带鱼群为主，您可在水下观赏众多珊瑚种类，探寻海底的奥秘。潜水深度为3-8米。您可在海下与热带鱼为伴、触摸柔软的珊瑚，在潜水教练的细心陪同下，为您呈现一个精彩纷呈的海底世界。经由潜水培训后，乘坐快艇至珊瑚礁潜点，教练一对一带入海下。教学过后可根据自身的条件在可潜深度范围内选择下潜深度，感受神秘的海底。</span></p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/04/1449203101640251.jpg\" title=\"1449203101640251.jpg\" alt=\"vip潜水3.jpg\"/></p>",
	                "costInfo": "<p><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">费用包含：项目体验费用</span><br style=\"white-space: normal; font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">费用不含：个人消费及其他未提及费用</span></p>",
	                "productInfo": "<p><span style=\"line-height: 18px; text-align: justify;\">凭短信及前往“蜈支洲岛上游客中心 收银处”，届时烦请报预订人订姓名、手机号领取票券，体验时票券由工作人员检票即可。</span><br style=\"line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"line-height: 18px; text-align: justify;\">7岁以下、60岁以上游客，患有中耳炎、心脏病、糖尿病、高血压、哮喘等疾病的游客，孕妇及酒后游客不允许参加潜水项目；</span><br style=\"line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"line-height: 18px; text-align: justify;\">参加所有海上娱乐项目必须穿救生衣，请勿佩戴眼镜、泳镜、手表、手机、相机等电子产品，贵重物品及首饰，听从教练的安排。</span><br style=\"line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"line-height: 18px; text-align: justify;\">凡患有心脏病，高血压、腰椎间盘突出等突发疾病或手术后尚未康复者；有癫痫、抽筋等病史的群体及孕妇谢绝参加海上娱乐项目。</span><br style=\"line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"line-height: 18px; text-align: justify;\">珊瑚酒店有预定项目的客人，必须提前与商务中心联系并预约水上项目。</span><br style=\"line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"line-height: 18px; text-align: justify;\">水上娱乐项目根据当天天气状况进行开放或者关闭。如客人想享用水上娱乐项目，需在酒店商务中心核实开放情况。</span></p>",
	                "usageInfo": "<p><span style=\"line-height: 18px; text-align: justify;\">联系电话：4001146666</span><br style=\"white-space: normal; line-height: 18px; text-align: justify;\"/><span style=\"line-height: 18px; text-align: justify;\">游玩地点：南亚风情--AAAAA国家风景区三亚蜈支洲岛旅游区</span><br style=\"white-space: normal; line-height: 18px; text-align: justify;\"/><span style=\"line-height: 18px; text-align: justify;\">营业时间：8:30-17:00</span></p>",
	                "refundInfo": "<p style=\"white-space: normal;\"><span style=\"line-height: 18px; text-align: justify;\">1、消费日期前，如需退改请至少提前一天联系我们；</span><br style=\"line-height: 18px; text-align: justify;\"/><span style=\"line-height: 18px; text-align: justify;\">2、消费日期后，如需退改请15天之内申请售后退款，提出后需经工作人员核实未消费后方退款；</span><br style=\"line-height: 18px; text-align: justify;\"/><span style=\"line-height: 18px; text-align: justify;\">3、本产品一经出票后，不可取消或更改。如需修改或取消，需收取订单金额100%的票务损失费。</span><br style=\"line-height: 18px; text-align: justify;\"/><span style=\"line-height: 18px; text-align: justify;\">4、关于退款退票问题，请联系您的导游，届时烦请提供您的姓名与订单手机号码，便于工作人员核查，确认无误后，我们会于七个工作日内原路径退款。</span><br/></p><p style=\"white-space: normal;\"><span style=\"line-height: 18px; text-align: justify;\"><br/></span></p><p><br/></p>",
	                "sliders": [
	                    "http://img3.dogplanet.cn/product/201510/31/a62bc78a-f162-1f1c-4375-abcafe92f0c2.jpg",
	                    "http://img3.dogplanet.cn/product/201510/31/42227bd0-1cfd-81c2-42fc-5f5959b6b90f.jpg"
	                ],
	                "subs": [
	                    {
	                        "id": 47,
	                        "name": "VIP潜水",
	                        "price": 980,
	                        "weekend_price": 980,
	                        "festival_price": 980,
	                        "introduction": "<p><span style=\"font-size: 14px;\"></span></p><p>※项目说明：980元/位，潜水时间45分钟左右。</p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/04/1449203121768411.jpg\" title=\"1449203121768411.jpg\" alt=\"IMG_8767_副本.jpg\"/></p><p>以观赏形态迥异的各类珊瑚群及色彩缤纷的热带鱼群为主，全程享受贵宾接待服务。</p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/04/1449203139895043.jpg\" title=\"1449203139895043.jpg\" alt=\"38k58PICeBu_1024.jpg\"/></p><p>VIP接待专区配有专业接待员，提供瓶装水、小食品以及各类潜水杂志供您悠闲消遣，潜水咬嘴、蛙鞋、浴巾、寄存柜等免费使用。该潜水区域为蜈支洲最佳潜点，潜水深度为3-10米。水下各类资源极其丰富，不但可以看到各类软、硬珊瑚和鱼类，还可看到海胆、海藻、各种贝类等海底生物，在资深潜水教练的悉心陪同下，将为您呈现一个精彩纷呈的海底世界。</p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/03/1449114727780415.jpg\" title=\"1449114727780415.jpg\" alt=\"vip潜水1.jpg\"/></p><p>经由潜水培训后，乘坐快艇去到VIP专业潜水接待船上，由为您精心挑选的高级别资深潜水教练陪同下潜。您可以根据即时水下环境及自身审美取向，自行决定潜水方向，选择潜水区域，根据您自身的身体适应能力自行掌控潜水程度，教练在适当区域内对您进行陪同，以全程保护您的人身安全。</p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/03/1449114799394573.jpg\" title=\"1449114799394573.jpg\" alt=\"珊瑚礁潜水1.jpg\"/></p>",
	                        "thumb": "http://img3.dogplanet.cn/product/201510/31/42227bd0-1cfd-81c2-42fc-5f5959b6b90f.jpg",
	                        "advance": 0
	                    }
	                ]
	            },
	            {
	                "id": 72,
	                "expertId": 30,
	                "name": "夜钓",
	                "price": 680,
	                "features": [
	                    "高端夜钓体验",
	                    "收获美味",
	                    "专业教练陪同"
	                ],
	                "shortComment": "收获夜间出没海鱼，感受别样海钓风情",
	                "introduce": "<p>作为一项高雅的休闲运动和高水平的竞技运动，被誉为“海上高尔夫”。蜈支洲岛现整合推出适用于住岛游客的“游艇夜钓”体验夜间垂钓的乐趣，点灯夜航，收获夜间出没海鱼。</p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/03/1449132867837912.jpg\" title=\"1449132867837912.jpg\" alt=\"夜钓1.jpg\"/></p>",
	                "costInfo": "<p><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">费用包含：项目体验费用</span><br style=\"white-space: normal; font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">费用不含：个人消费及其他未提及费用</span></p>",
	                "productInfo": "<p>凭短信前往“蜈支洲岛上游客中心收银处”，届时烦请报预订人订姓名、手机号领取票券，体验时票券由工作人员检票即可。</p>",
	                "usageInfo": "<p><span style=\"line-height: 18px; text-align: justify;\">联系电话：4001146666</span><br style=\"white-space: normal; line-height: 18px; text-align: justify;\"/><span style=\"line-height: 18px; text-align: justify;\">游玩地点：南亚风情--AAAAA国家风景区三亚蜈支洲岛旅游区</span><br style=\"white-space: normal; line-height: 18px; text-align: justify;\"/><span style=\"line-height: 18px; text-align: justify;\">营业时间：18:00-22:00</span></p>",
	                "refundInfo": "<p style=\"white-space: normal;\"><span style=\"line-height: 18px; text-align: justify;\">1、消费日期前，如需退改请至少提前一天联系我们；</span><br style=\"line-height: 18px; text-align: justify;\"/><span style=\"line-height: 18px; text-align: justify;\">2、消费日期后，如需退改请15天之内申请售后退款，提出后需经工作人员核实未消费后方退款；</span><br style=\"line-height: 18px; text-align: justify;\"/><span style=\"line-height: 18px; text-align: justify;\">3、本产品一经出票后，不可取消或更改。如需修改或取消，需收取订单金额100%的票务损失费。</span><br style=\"line-height: 18px; text-align: justify;\"/><span style=\"line-height: 18px; text-align: justify;\">4、关于退款退票问题，请联系您的导游，届时烦请提供您的姓名与订单手机号码，便于工作人员核查，确认无误后，我们会于七个工作日内原路径退款。</span><br/></p><p style=\"white-space: normal;\"><span style=\"line-height: 18px; text-align: justify;\"><br/></span></p><p><br/></p>",
	                "sliders": [
	                    "http://img3.dogplanet.cn/product/201512/02/e193f1ff-ef46-ffbb-680b-bef57d2ff012.jpg",
	                    "http://img3.dogplanet.cn/product/201512/02/3ea396f3-232e-dff1-c3c3-b25b53332bb7.jpg"
	                ],
	                "subs": [
	                    {
	                        "id": 80,
	                        "name": "夜钓",
	                        "price": 680,
	                        "weekend_price": 680,
	                        "festival_price": 680,
	                        "introduction": "<p>※项目说明：680元/位/四小时。</p><p>体验夜间垂钓的乐趣，点灯夜航，收获夜间出没海鱼。<br/></p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/03/1449132892324272.jpg\" title=\"1449132892324272.jpg\" alt=\"夜钓4.jpg\"/></p><p>有专业的垂钓教练讲解陪同，感受告别喧嚣后的海面，感受别样幽静神秘。经营时间为18:00-22:00，目前只针对住岛客人开放，下岛游客暂不接待。<br/></p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/03/1449132895372281.jpg\" title=\"1449132895372281.jpg\" alt=\"夜钓2.jpg\"/></p>",
	                        "thumb": "http://img3.dogplanet.cn/product/201512/02/3ea396f3-232e-dff1-c3c3-b25b53332bb7.jpg",
	                        "advance": 0
	                    }
	                ]
	            },
	            {
	                "id": 85,
	                "expertId": 30,
	                "name": "小帆船",
	                "price": 150,
	                "features": [
	                    "惊险刺激",
	                    "感受海风",
	                    "征服海浪"
	                ],
	                "shortComment": "乘坐小帆船感受海洋魅力",
	                "introduce": "<p>帆船是指利用风力前进的船。帆船运动是依靠自然风力作用于帆上，由人驾驶船只行驶的一项水上运动。它集竞技、娱乐、观赏和探险于一体。</p>",
	                "costInfo": "<p><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px;\">费用包含：项目体验费用</span><br style=\"white-space: normal; font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; font-size: 12px; line-height: 18px;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px;\">费用不含：个人消费及其他未提及费用</span></p>",
	                "productInfo": "<p><span style=\"font-family: 宋体; color: rgb(51, 44, 43);\">凭短信前往</span>“蜈支洲岛上游客中心收银处”<span style=\"font-family: 宋体; color: rgb(51, 44, 43); font-weight: bold;\">，</span><span style=\"font-family: 宋体; color: rgb(51, 44, 43);\">届时烦请报预订人订姓名、手机号领取票券，体验时票券由工作人员检票即可。</span></p>",
	                "usageInfo": "<p><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">联系电话：4001146666</span><br style=\"white-space: normal; font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">游玩地点：南亚风情--AAAAA国家风景区三亚蜈支洲岛旅游区</span><br style=\"white-space: normal; font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">营业时间：8:30-17:00</span></p>",
	                "refundInfo": "<p><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">1、消费日期前，如需退改请至少提前一天联系我们；</span><br style=\"white-space: normal; font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">2、消费日期后，如需退改请15天之内申请售后退款，提出后需经工作人员核实未消费后方退款；</span><br style=\"white-space: normal; font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">3、本产品一经出票后，不可取消或更改。如需修改或取消，需收取订单金额100%的票务损失费。</span><br style=\"white-space: normal; font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">4、关于退款退票问题，请联系您的导游，届时烦请提供您的姓名与订单手机号码，便于工作人员核查，确认无误后，我们会于七个工作日内原</span><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">路径退款。</span></p>",
	                "sliders": [
	                    "http://img3.dogplanet.cn/product/201512/31/8e66c435-db88-287e-f20c-b915d7f0dab4.jpg",
	                    "http://img3.dogplanet.cn/product/201512/31/081d7eff-cb20-2379-df9b-9fbd5bb9e943.jpg"
	                ],
	                "subs": [
	                    {
	                        "id": 88,
	                        "name": "小帆船",
	                        "price": 150,
	                        "weekend_price": 150,
	                        "festival_price": 150,
	                        "introduction": "<p style=\"white-space: normal;\">※项目说明：150元/位/30分钟。小帆船可同时接待6人，</p><p style=\"white-space: normal;\">当空气流动得快的时候，在正面挡住它的物体就会受到空气的冲击，这种冲击产生的压力我们称为动压力。当帆船顺风行驶时，就是空气对帆的动压力推动帆船前进。</p><p style=\"white-space: normal;\"><img src=\"http://img3.dogplanet.cn/source/image/201601/11/1452489144493335.jpg\" title=\"1452489144493335.jpg\" alt=\"ABC2BCBD@5B0DF15A.C01C9356_recompress_副本.jpg\"/></p><p style=\"white-space: normal;\">依靠自然风力作用于帆上，由人驾驶船只行驶的一项水上运动，它集竞技、娱乐、观赏和探险于一体，备受人们的喜爱，也是各国人民进行海洋文化交流的重要渠道。</p><p style=\"white-space: normal;\"><img src=\"http://img3.dogplanet.cn/source/image/201601/11/1452504549629650.jpg\" title=\"1452504549629650.jpg\" alt=\"帆船1.jpg\"/></p><p style=\"white-space: normal;\">蜈支洲岛开展的帆船项目主要以体验驾驶观光为主，该项目在蜈支洲岛海域周边，风景宜人；游玩全程由教练员陪同，故本项目无论男女老幼，只要身体健康，年龄在7-60周岁以内，身高1.2米及以上均可报名参加。</p><p><br/></p>",
	                        "thumb": "http://img3.dogplanet.cn/product/201512/31/081d7eff-cb20-2379-df9b-9fbd5bb9e943.jpg",
	                        "advance": 0
	                    }
	                ]
	            },
	            {
	                "id": 3,
	                "expertId": 30,
	                "name": "陆地冲浪",
	                "price": 150,
	                "features": [
	                    "征服海浪",
	                    "惊险刺激"
	                ],
	                "shortComment": "征服海浪，简单易学",
	                "introduce": "<p><span style=\"font-size: 14px;\"></span>冲浪（surfing）是一项古老文化，是以海浪为动力，利用自身技巧和平衡力，搏击海浪的一项运动。<span style=\"font-size: 14px;\"></span></p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/03/1449131306149919.jpg\" title=\"1449131306149919.jpg\" alt=\"陆地冲浪2.jpg\"/></p>",
	                "costInfo": "<p><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">费用包含：项目体验费用</span><br style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">费用不含：个人消费及其他未提及费用</span></p>",
	                "productInfo": "<p><span style=\"font-size: 14px;\">凭短信前往“蜈支洲岛上游客中心收银处”，届时烦请报预订人订姓名、手机号领取票券，体验时票券由工作人员检票即可。</span></p>",
	                "usageInfo": "<p><span style=\"font-size: 14px;\"></span><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">联系电话：4001146666</span><br style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">游玩地点：南亚风情--AAAAA国家风景区三亚蜈支洲岛旅游区</span><br style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"font-family: &#39;sans serif&#39;, tahoma, verdana, helvetica; line-height: 18px; text-align: justify;\">营业时间：8:30-17:00</span><span style=\"font-size: 14px;\"></span></p><p><br/></p>",
	                "refundInfo": "<p><span style=\"font-size: 14px;\"></span></p><p><span style=\"line-height: 18px; text-align: justify;\">1、消费日期前，如需退改请至少提前一天联系我们；</span><br style=\"line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"line-height: 18px; text-align: justify;\">2、消费日期后，如需退改请15天之内申请售后退款，提出后需经工作人员核实未消费后方退款；</span><br style=\"line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"line-height: 18px; text-align: justify;\">3、本产品一经出票后，不可取消或更改。如需修改或取消，需收取订单金额100%的票务损失费。</span><br style=\"line-height: 18px; text-align: justify; white-space: normal;\"/><span style=\"line-height: 18px; text-align: justify;\">4、关于退款退票问题，请联系您的导游，届时烦请提供您的姓名与订单手机号码，便于工作人员核查，确认无误后，我们会于七个工作日内原路径退款。</span><span style=\"font-size: 14px;\"></span><br/></p><p><br/></p>",
	                "sliders": [
	                    "http://img3.dogplanet.cn/product/201510/31/3f1c28a1-5edc-d7c1-d094-30ebf6dcb2d4.jpg",
	                    "http://img3.dogplanet.cn/product/201510/31/166479b2-5881-c827-441c-ed223bd15330.jpg"
	                ],
	                "subs": [
	                    {
	                        "id": 29,
	                        "name": "陆地冲浪",
	                        "price": 150,
	                        "weekend_price": 150,
	                        "festival_price": 150,
	                        "introduction": "<p><span style=\"font-size: 14px;\"></span></p><p>※项目说明：150元/位/10分钟。</p><p>冲浪（surfing）是一项古老文化，是以海浪为动力，利用自身技巧和平衡力，搏击海浪的一项运动。<br/></p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/03/1449131414641401.jpg\" title=\"1449131414641401.jpg\" alt=\"陆地冲浪4.jpg\"/></p><p>为了让游客更好的体验冲浪的同时，保证游客安全，蜈支洲岛开设露天冲浪场馆，自荷兰引进“陆地冲浪”项目设施，采取一对一式教练辅导保护模式，体验者站或立、或跪、或匍匐在冲浪板上，利用腹板、跪板、橡皮垫等器具驾驭海浪，与海浪亲密接触。</p><p><img src=\"http://img3.dogplanet.cn/source/image/201512/03/1449131421123752.jpg\" title=\"1449131421123752.jpg\" alt=\"陆地冲浪5.jpg\"/></p><p><br/></p>",
	                        "thumb": "http://img3.dogplanet.cn/product/201510/31/166479b2-5881-c827-441c-ed223bd15330.jpg",
	                        "advance": 0
	                    }
	                ]
	            }
	        ]
	    }
	}
	```
	
#### 12.5.2 获取达人打包产品（目前用于达人商城页）
* 说明:
	
	1. 获取打包产品详情页

* url:
	
		/v1/c/expert/pack/
		
* params:

		1. id	达人 id

* response:
		
		1. ret: 1001	成功		0	失败
		2. packages	=>	[]

* sample:

	```json
	url:	http://api.dogplanet.dev/v1/c/expert/pack/
	
	params:	
	{
		"id": 30,
	}
	
	response:
	{
	    "ret": 1001,
	    "packages": [
	        {
	            "id": 1,
	            "name": "打包组合商品~",
	            "price": 399999,
	            "thumb": ""
	        }
	    ]
	}
    ````



# **TBD**..	



# 更新说明

## Bug 修复、文档修改
* 2015.9.20
	
	1. 修改了首页搜索部分，达人、产品数据结构，增加了 “达人星级”、“服务日期”
	

* 2015.9.24

	1. 修正 [3.2](#toc_16) “列表页搜索 - 列表页数据请求” 中 response 的格式。
		
			experts  =>  [
			    [
			        'id'    => 123,
			        'name'  =>  '陈成',
			        'avatar'    =>  '@img-url',
			        'features'  =>  ['打酱油', '吃饭'],
			        'introduce' => 'why so serious',
			    ],
			    //...
			]
		=>
		
			experts  =>  [
			    [
			        'id'    => 124,
			        'name'  =>  '陈成',
			        'stars' => 5,       //星级
			        'avatar'    =>  '@img-url',
			        'features'  =>  ['打酱油', '吃饭'],
			        'services'  =>  [       //10: 全天可下单 20: 半天可下单   30: 不可下单
			            '2015-09-19' => 30
			            '2015-09-20' => 30
			            '2015-09-21' => 30
			            '2015-09-22' => 30
			            '2015-09-23' => 20
			            '2015-09-24' => 30
			            '2015-09-25' => 30
			        ]
			        'introduce' => 'why so serious',
			
			    ],
			    //...
			]
	2. 修正些许样式问题

* 2015.9.28

	1. 修正 [1.4 找回密码](#toc_10) 中 url 地址错误

* 2015.9.29
	
	1. 为 [1.1 通用短信接口](#toc_7) 添加了一个 **type** 参数，确保已注册用户在注册的时候收不到短信（**type** 默认为注册）。

* 2015.10.9
	
	1. 修改了 [5.1 购买服务页](#toc_25) 的数据结构：

			'2015-09-13' => [
	            '10'    =>  200,    //早
	            '20'    =>  300     //下午
	            '30'    =>  1000,   //晚上
	            '50'    =>  1500,   //全天
	        ],  
		=>
	
			'2015-09-13' => [
				['type' =>  10, price   =>  200],   //早
				['type' =>  10, price   =>  300],   //下午
				['type' =>  30, price   =>  1000],  //晚上
				['type' =>  50, price   =>  1500],  //全天
			]
			
* 2015.10.15
	
	1. [6.2.1.2 生成订单 - 单独生成服务订单](#toc_34) 中 services 格式修改，由

			service[2015-09-03][type][] = 20
			service[2015-09-03][type][] = 30
			service[2015-09-03][type][] = 10
			
			//json
			"services['2015-09-18'][type][]": 10,
			'services["2015-09-18"][type][]': 20,
			"services[2015-09-18][type][]": 30

		=>
	
			dates	=>	[2015-09-18, 2015-09-20]
			types	=>	[[10, 20], [30, 20]]
			
			//json
			"dates[]": 2015-09-18
			"types[0][]": 20,
			"types[0][]": 10,
			"types[0][]": 30,


* 2015.10.17
	1. 修正达人头像获取算法。

* 2015.10.20
	1. 修正 [3.2 列表页数据请求](#toc_16) 的 **sample**。 （之前没有 产品的 sample）
	2. 之前的达人 [3.2 列表页数据请求](#toc_16) 以及 [4.1.1 达人详情页](#toc_19) 达人服务数据请求格式错误，应该显示 **是否可下单**，而给出的数据是 **type 与 price**，已修正。

* 2015.10.21
	1. 补全了 ==**达人背景图**== 的获取。
	2. 修正了文档部分样式问题。

* 2015.10.23
	1. 产品详情页逻辑修改，详见：[4.2.1 产品详情页 - 说明](#toc_23)。
	2. 更改了一些样式。

* 2015.10.24
	1. 优化了 [8.2 购物车列表](#toc_40) 的获取逻辑。
	2. 修复了购物车已知的一些 bug:
		- 添加购物车在某些情况可能失效（由于数据复用导致的主表状态未变更，从而招不到数据）。
		- 添加购物车失败的时候，回滚可能会不工作（由于数据复用所导致）。
		- 重复添加一天的服务不同状态，价格不会跟着改变（合并数据时未重新计算）。
		- 添加购物车的时候，会重新计算价格，现在 [8.1 添加购物车](#toc_40) 中的 price 参数可以传递任意值。（为了数据有效性，price 键值必须存在）

* 2015.10.27
	1. [4.2.1 产品详情页](#toc_23) 添加了四个字段：费用说明(costInfo) 产品说明(productInfo) 使用方法(usageInfo) 退改规则(refundInfo) 

* 2015.10.28
	1. [7.1 支付 API](#toc_38) 添加了 **银联支付** 的选项

* 2015.11.2
	1. 修复 [5.2.1.1 达人推荐产品类型](#toc_28) 给出的 types 的错误 `（types[3] = '娱乐'）`

* 2015.11.9
	1. [1.4 找回密码](#toc_10) 去掉参数 `name`

* 2015.11.16
	1. [10. 达人商城](#toc_54) 添加了 **sample**
	2. **达人详情中 `mail` 字段，由 `bool` 修改为真实邮箱**


## 功能实现
* 2015.9.20

	1. 增加： “更新说明” 
	2. 实现： [3](#toc_14). “列表页搜索” 功能

* 2015.9.24
	
	1. 实现： [4.1.1](#toc_19) “达人详情页”（基本内容） 功能
	2. 实现： [4.1.2](#toc_20) “达人详情页 - 获取服务”(日历) 功能

* 2015.9.25

	1. **所有请求方式由 post 改为 get 与 post 均可**，见 [1. URL](#toc_2)
	2. 实现： [4.1.3](#toc_21) “达人详情页 - 获取评论” 功能
	3. 适配 jsonp

* 2015.9.28

	1. 增加功能： [1.5 获取用户信息](#toc_11)  与 [1.6 注销](#toc_11)
	2. **实现功能： [5.1 购买服务页](#toc_25)**

* 2015.10.8
	1. 实现功能：[5.2.2 确认订单页 - 达人推荐产品](#toc_29)
	2. **新增功能： [5.1 购买服务页](#toc_25) 中添加 ==“全天”== 服务种类(当日上午、下午、晚上均购买时：自动追加全天价格)**

* 2015.10.9
	1. 实现功能：[4.2.1 产品详情页](#toc_23)	（暂时没有 “注意事项”与 “退订策略”)

* 2015.10.10
	1. 实现功能：[6.1.1 添加联系人页面 - 获取常用联系人](#toc_31) 

* 2015.10.13
	1. 实现功能：[6.2.1.2 生成订单 - 单独生成服务订单](#toc_35)

* 2015.10.15
	1. 实现功能：[6.2.1.1 生成订单 - 单独生成产品订单](#toc_34)
	2. [6.2.1.1 生成订单 - 单独生成产品订单](#toc_34) 与 [6.2.1.2 生成订单 - 单独生成服务订单](#toc_35) 传参方式多了一种：将所有的数据（callback 除外）包裹在一个命名为 ==json== 的数组里，json 加密后 get 传递（当有 json 参数存在时，其余 Get、Post 参数会失效）

* 2015.10.17
	1. 实现功能：[7.1 支付 - 支付 api](#toc_38)

* 2015.10.20
	1. 实现功能：[8. 购物车](#toc_39)，包括内容：
		- [8.1 添加购物车](#toc_40)
		- [8.2 购物车列表](#toc_41)
		- [8.3 删除（清空）购物车内容](#toc_42)

* 2015.10.21
	1. 实现功能：[个人中心 - 9.1 订单部分](#toc_46)
		- [9.1.1 订单列表](#toc_47)
		- [9.1.2 订单详情](#toc_48)

* 2015.10.22
	1. 实现功能：[个人中心 - 9.1.3 评论订单](#toc_49)
	2. 实现功能：[10. 达人商城](#toc_54)

* 2015.10.24
	1. 增加功能：[个人中心 - 9.1.4 取消订单](#toc_50)
	2. 增加功能：[确认订单 - 5.2.1.1 获取达人产品品类](#toc_28) （在 [5.2.1.2 获取达人推荐产品](#toc_29)）之前调用）
	3. 增加功能：[个人中心 - 6.2.2 购物车生成订单](#toc_36)

* 2015.10.26
	1. **增加功能：[个人中心 - 9.1.5 操作订单状态](#toc_52)**（目前可以理解为 确认取消订单）
	2. 修改了 [个人中心 - 9.1.2 订单详情](#toc_48)（**为了配合不同订单状态的不同操作按钮**）

* 2015.10.27
	1. 增加功能：[个人中心 - 9.2.1 修改密码](#toc_53)

* 2015.11.13
	1. 追加了一个功能，以便完成扫码进入商城，选择产品支付（无需注册）：[11.1 单独生成产品订单（临时解决方案）](#toc_56)
	2. 在 [9.1.2 订单详情](#toc_48)，为 达人商品 追加了 **达人信息** `expert` 字段

* 2015.11.18
	1. 追加了功能：[11.2 通过手机获取订单详情](#toc_57)

* 2015.11.19
	1. [4.2.1 产品详情](#toc_23) 子产品字段中追加了一个 `advance => n` 参数，用来判断该子产品需要提前 `n` 天购买

	
* 2015.11.30
	1. 为每个登录用户追加了一个 token，用于查询用户信息，在注册、查询信息处会追加返回该参数。

* 2015.12.3
	1. 在获取订单列表处，添加了 `token` 验证。
	2. 增加了一个状态码：`ret => 999`，表示 `token` 失效，需要重新登录。

* 2015.12.9
	1. 在获取购物车列表处，添加了 `token` 验证，`token`  失效后，与订单一样返回 999。

* 2015.12.10
	1. 追加了一个 类别 [12 一些追加接口](#toc_58) ，一些简单的功能性接口（对应一些新的需求）。
	2. 追加了 [12.1 获取购物车数量](#toc_59) ，用于获取用户购物车数量。

* 2
	1. 追加了 [12.2 个人中心获取达人](#toc_60) 。
* 2015.12.11
	1. 追加了 [12.3 通过验证码实现自动注册/登录功能](#toc_61)。

* 2015.12.28
	1. 订单详情页，子订单信息追加了一个参数：`thumb`，由于改版需要，需要一张产品的缩略图。
	2. 追加了一个接口，[12.4 取消子订单](#toc_62)。

* 2015.1.4
	1. 订单详情页，子订单信息追加了三个参数：`refundNum`、`refundAmount`、`refund`，即：`退票数量`、`退款金额` 与 `能否退款`。

* 2015.1.21
	1. 追加了接口，[12.5.1 打包产品详情页](#toc_64)。
	2. 追加了接口，[12.5.2 获取达人打包产品（目前用于达人商城页）](#toc_65)。

* 2015.1.25
	1. [12.5.1 打包产品详情页](#toc_64) 与 [12.5.2 获取达人打包产品（目前用于达人商城页）](#toc_65) 的接口返回的值有些许变化，具体以实际使用为主。

* 2015.1.26
	1. [4.1.1 达人详情页](#toc_19) 中添加了一个参数。

* 2016.2.22
	1. [5.1 购买服务页](#toc_25) 由于需求改动，增加了 `达人详情` 内的一些基本参数。
	2. [4.1.1 达人详情页](#toc_19) 电话改为真实电话（之前为 bool）。

* 2016.3.1
	1. [12.5.1 打包产品详情页](#toc_64)，[12.5.2 获取达人打包产品（目前用于达人商城页）](#toc_65)，接口数据均有变化（`售罄`、`下架`功能上线），具体自行观察接口。
