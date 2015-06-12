#TAN 14 API 文档

[TOC]

### 全局变量
 -  **ROOT_DOMAIN** = 'https://api.tan14.cn/*PREFIX*'
 -  **PREFIX** = 'wp/v2'

参数可选性
   - **M** for **M**andatory (必填)
   - **O** for **O**ptional (选填)

请求头
  - **Tan14-key** : *TAN14-KEY*

----
### API

---
####频道管理

#####0.查询公司下所有频道
 
**url** : **ROOT_DOMAIN/PN/channel/list**
**method** : **GET**

**返回示例**
```
   GET ROOT_DOMAIN/PN/channel/list
   
   RESPONSE: 
   200 ok
   [
     {
      'id':CHANNEL_ID, 
      'name':NAME,
      'tags':TAGS,
      'pn':PN,
      'channel_type': {...},
      'channel_type_id':CHANNEL_TYPE_ID,
      'remark':REMARK,
      'applied':true,
      'online':true,
      'domains':[...],
      'backends':[...], 
      'mcbackends':{...},
      'security':{...},
      'custom_backendpath':{...},
      'custom_back_source':{...},
      'custom_conf':{...},
      'created':CHANNEL_CREAT_TIME
     },
     ...
  ]
```

**返回字段说明**

 | 返回值字段      |    说明          |
| --------      | -------------   |
| id             |频道id            |
| name           |频道名称          |
| tags           |频道标签          |
| pn             |产品id            |
| channel_type   |频道类型 说明见 *获取可用频道类型列表* |
|channel_type_id |频道类型 1:页面加速 2:下载加速|
| remark         |频道备注           |
| applied        |当applied为false时，代表频道有新的配置尚未下发|
| online         |当online 为false时，代表当前频道下所有域名不可用，需要首先启用该频道|
| domains        |频道下的域，说明见 *域名管理* |
| backends       |频道下的源站，说明见 *源站管理* |
| mcbackends     |频道下的MC源站，说明见 *MC源站管理* |
| security       |频道的安全设置，说明见 *频道黑白名单/防盗链管理* |
|custom_backendpath|频道的自定义PATH，说明见 *自定义配置文件* |
|custom_back_source|频道的自定义回源，说明见 *自定义配置文件* |
|custom_conf     |频道的自定义配置，说明见 *自定义配置文件* |
| created        | 频道的创建时间     |


#####1.查询频道
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID**
**method** : **GET**

**返回示例**
```
   GET ROOT_DOMAIN/PN/channel/CHANNEL_ID
   
   RESPONSE: 
   200 ok
     {
      'id':CHANNEL_ID, 
      'name':NAME,
      'tags':TAGS,
      'pn':PN,
      'channel_type': {...},
      'channel_type_id':CHANNEL_TYPE_ID,
      'remark':REMARK,
      'applied':true,
      'online':true,
      'domains':[...],
      'backends':[...], 
      'mcbackends':{...},
      'security':{...},
      'custom_backendpath':{...},
      'custom_back_source':{...},
      'custom_conf':{...},
      'created':CHANNEL_CREAT_TIME
  }
```

**返回字段说明**

 | 返回值字段      |    说明          |
| --------      | -------------   |
| id             |频道id            |
| name           |频道名称          |
| tags           |频道标签          |
| pn             |产品id            |
| channel_type   |频道类型 说明见*获取可用频道类型列表*|
|channel_type_id |频道类型 1:页面加速 2:下载加速|
| remark         |频道备注           |
| applied        |当applied为false时，代表频道有新的配置尚未下发|
| online         |当online 为false时，代表当前频道下所有域名不可用，需要首先启用该频道|
| domains        |频道下的域，说明见*域名管理*|
| backends       |频道下的源站，说明见*源站管理*|
| mcbackends     |频道下的MC源站，说明见*MC源站管理*|
| security       |频道的安全设置，说明见*频道黑白名单/防盗链管理*|
|custom_backendpath|频道的自定义PATH，说明见*自定义配置文件*|
|custom_back_source|频道的自定义回源，说明见*自定义配置文件*|
|custom_conf     |频道的自定义配置，说明见*自定义配置文件*|
| created        | 频道的创建时间     |




----

#####2.添加频道

**url** : **ROOT_DOMAIN/PN/channel**
**method** : **POST**

**body** : 

| 字段          |必填性|   说明   |
| --------     | :----:| ----   |
|  name         | M    |频道名称，用于显示，供用户区分|
|channel_type_id| M    |频道类型 1:页面加速 2:下载加速|
| remark        |  O   |频道备注|
|  tags         |  O   |标签，逗号分隔的多个文本|

 
**返回示例**
```
   POST ROOT_DOMAIN/PN/channel
   
   RESPONSE: 
   201 created
   {
      'id':CHANNEL_ID, 
      'name':*NAME*,
      'pn':PN,
      'remark':*REMARK*,
      'applied':true,
      'online':true,
      'created':CHANNEL_CREAT_TIME,
      'tags' : *TAGS*,
      'domains' : [],
      'backends' : [],
      'security' : {},
      'channel_type' : {...},
      'channel_type_id' : *CHANNEL_TYPE_ID*,
      'custom_backendpath' : {},
      'custom_back_source' : {},
      'custom_conf' : {},
      'mcbackends' : {},
   }
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| id             |频道id            |
| name           |添加的频道名称     |
| pn             |产品id            |
| remark         |添加的频道备注       |
| tags           |添加的频道标签     |
| applied        |默认为true，已下发状态|
| online         |默认为true，开启状态|
| created        |频道的创建时间     |


----
#####3.修改频道

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID**
**method** : **PUT**

**body** :

| 字段          |必填性|   说明   |
| --------     | :----:| ----   |
|  name         |  O   |频道新名称|
| remark        |  O   |频道新备注|
|  tags         |  O   |标签，逗号分隔的多个文本，新增一个应追加在原有列表之后并提交，删除传递空内容即可|


**返回示例** 
```
   PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID

   RESPONSE:
   200 ok 
   {
      'id':CHANNEL_ID, 
      'name':*NAME*,
      'pn':PN,
      'remark':*REMARK*,
      'applied':true,
      'online':true,
      'created':CHANNEL_CREAT_TIME,
      'tags' : *TAGS*,
      'domains' : [...],
      'backends' : [...],
      'security' : {...},
      'channel_type' : {...},
      'channel_type_id' : CHANNEL_TYPE_ID 1 or 2,
      'custom_backendpath' : {...},
      'custom_back_source' : {...},
      'custom_conf' : {...},
      'mcbackends' : {...},
   }
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| id             |频道id            |
| name           |频道新名称         |
| pn             |产品id            |
| remark         |频道新备注           |
| tags           |频道新标签           |


----
#####4.获取可用频道类型列表
 
**url** : **ROOT_DOMAIN/channel/type**
**method** : **GET**

**返回示例**
```
   GET ROOT_DOMAIN/channel/type
   
   RESPONSE: 
   200 ok
   [
        {
            'channel_type_groups' : [...],
            'id':CHANNEL_TYPE_ID 1 or 2,
            'name':CHANNEL_TYPE_NAME '页面加速' or '下载加速',
            'created':CHANNEL_TYPE_CREAT_TIME,
            'code': TYPE_CODE 'webpage' or 'download'
        },
        {}
    ]
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
|channel_type_groups|频道类型分组 说明见*切换频道分组*|
| id             |频道类型id 1:页面加速 2:下载加速|
| name           |频道类型名称 '页面加速' or '下载加速'|
| code           |频道类型标注 'webpage' or 'download'|
| created        |该频道类型的创建时间  |


----

#### 域名管理


#####1.查询域名
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID**
**method** : **GET**


**返回示例**
```
    GET ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID
    
    RESPONSE: 
    200 ok
    {
        'id': DOMAIN_ID,
        'domain':DOMAIN,
        'pingback':PINGBACK,
        'ssl':false or true,
        'ignore_querystring':true or false,
        'remark':REMARK,
        'cname':CNAME,
        'channel_id':CHANNEL_ID,
        'dnspod_id':DNSPOD_ID,
        'created':DOAMIN_CREAT_TIME
    }
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| id             |域名id          |
| domain         |域名           |
| pingback       |域名的测试链接 |
| ssl            |true：加密 false：不加密 |
|ignore_querystring|是否忽略url中的querystring，true表示忽略|
| remark         |域名备注       |
|   cname        |域别名         |
|channel_id      |域所属频道id   |
| created        | 域名的创建时间|


----
#####2.添加域名
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain**
**method** : **POST**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|domain    |  M   |要添加的域名 |
|pingback  |  M   |域名的测试链接，必须是一个能够正常访问的URL(http/https 均可)且与域名一致，用于源站健康检查|
|ssl       |  O   |布尔值，true：加密 false：不加密 默认为 false|
|ignore_querystring|  O   |忽略querystring, 布尔值，默认为false, 即不忽略|
|remark    |  O   |域名备注|



**返回示例**
```
   POST ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain

   RESPONSE: 
   201 created
   {
       'id': DOMAIN_ID,
       'domain':*DOMAIN*,
       'pingback':*PINGBACK*,
       'ssl':*SSL*,
       'ignore_querystring':*IGNORE_QUERYSTRING*,
       'remark': *REMARK*,
       'created': DOAMIN_CREAT_TIME,
       'channel_id':CHANNEL_ID,
       'cname':CNAME,
       "dir_freshs": [...],
       "cache_rules":[...]
   }
```

**返回字段说明**

| 返回值字段      |    说明        |
| --------      | ------------- |
| id             |域名id         |
| domain         |添加的域名           |
| pingback       |添加的域名测试链接 |
| ssl            |设置的加密           |
|ignore_querystring|设置的是否忽略querystring|
| remark         |添加的域名备注       |
|   cname        |域别名         |
|channel_id      |域所属频道id   |
| created         | 域名的创建时间|
| dir_freshs      | 刷新记录  说明见*目录刷新*|
| cache_rules     | 缓存规则 说明见*缓存规则*|

 
----

#####3.修改域名

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID**
**method** : **PUT**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|domain    |  M   |域名     |
|pingback  |  M   |域名的测试链接|
|ssl       |  O   |默认为 false|
|ignore_querystring|  O   |忽略querystring, 布尔值|
|remark    |  O   |域名备注    |


**返回示例**
```
   PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID
   
   RESPONSE:
   200 ok
   {
       'id': DOMAIN_ID,
       'domain':*DOMAIN*,
       'pingback':*PINGBACK*,
       'ssl':*SSL*,
       'ignore_querystring':*IGNORE_QUERYSTRING*,
       'remark': *REMARK*
       'created': DOAMIN_CREAT_TIME
       "dir_freshs": [...],
       "cache_rules":{...}
   }
```
**返回字段说明**

| 返回值字段      |    说明        |
| --------      | ------------- |
| id             |域名id         |
| domain         |修改后的域名     |
| remark         |修改后的域名备注   |
| ssl            | 修改后的加密形式    |
| pingback       | 修改后的域名测试链接 |
|ignore_querystring|修改后的querystring忽略形式|



---- 
#####4.删除域名

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID**
**method** : **DELETE**

**返回示例**
```
   DELETE ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID
   
   RESPONSE: None
```


----
#### 源站管理

#####1.查询源站

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/backend/BACKEND_ID**
**method** : **GET**

**返回示例**
```
    GET ROOT_DOMAIN/PN/channel/CHANNEL_ID/backend/BACKEND_ID
    
    RESPONSE: 
    200 ok
    {
        'id': BACKEND_ID,
        'name':NAME,
        'backend':BACKEND,
        'port':PORT,
        'channel_id': CHANNEL_ID ,
        'status': true or false,
        'is_domain': true or false,
        'created':BACKEND_CREAT_TIME
    }
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| id             |源站id              |
| name           |源站名称            |
| backend        |源站                |
| port           |源站所用端口        |
| channel_id     |所属频道id          |
| status         |源站状态，true为开启|
| is_domain      |是否是域名的形式，true为域名形式 |
| created        |源站创建时间        |



----

#####2.添加源站
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/backend**
**method** : **POST**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|name      |  M   |源站名称  |
|backend   |  M   |源站 为IP或者域名|
|port      |  O   |源站提供服务的端口，默认为80|

**返回示例**

```
   POST ROOT_DOMAIN/PN/channel/CHANNEL_ID/backend
   
   RESPONSE: 
   201 created
   {
        'id': BACKEND_ID,
        'name':*NAME*,
        'backend':*BACKEND*,
        'port':*PORT*,
        'channel_id': CHANNEL_ID,
        'status':true or false,
        'is_domain': true or false,
        'created':BACKEND_CREAT_TIME
   }

```

**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| id             |源站id              |
| name           |源站名称            |
| backend        |源站                |
| port           |源站所用端口        |
| channel_id     |所属频道id          |
| status         |源站状态，true为开启|
| is_domain      |是否是域名的形式，true为域名形式 |
| created        |源站创建时间        |


----
 
#####3.修改源站

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/backend/BACKEND_ID**
**method** : **PUT**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|name      |  M   |源站名称  |
|backend   |  M   |源站 为IP或者域名|
|port      |  O   |源站提供服务的端口，默认为80|

**返回示例**
```
   PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/backend/BACKEND_ID

   RESPONSE: 
   200 ok
   {
        'id': BACKEND_ID,
        'name':*NAME*,
        'backend':*BACKEND*,
        'port':*PORT*,
        'channel_id': CHANNEL_ID ,
        'status':true or false,
        'is_domain': true or false,
        'created':BACKEND_CREAT_TIME
   }
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| id             |源站id              |
| name           |修改后源站名称            |
| backend        |修改后源站                |
| port           |修改后源站所用端口        |




----
 
#####4.删除源站
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/backend/BACKEND_ID**
**method** : **DELETE**

**返回示例**:
```
   DELETE ROOT_DOMAIN/PN/channel/CHANNEL_ID/backend/BACKEND_ID
   
   RESPONSE: None
```

----
 

#####5.开启/暂停源站
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/backend/BACKEND_ID/status**
**method** : **PUT**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|status    |  M   |true:开启 false:暂停|

**返回示例**:

```
   PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/backend/BACKEND_ID/status
   
   RESPONSE:
   200 ok
   {
        'id': BACKEND_ID,
        'name':NAME,
        'backend':BACKEND,
        'port':PORT,
        'channel_id': CHANNEL_ID,
        'status':*STATUS*,
        'is_domain': true or false,
        'created':BACKEND_CREAT_TIME
   }
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| id             |源站id              |
| name           |源站名称            |
| backend        |源站                |
| port           |源站所用端口        |
| channel_id     |所属频道id          |
| status         |源站状态，true为开启|



----

#### 频道操作
#####1.开启频道

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/active**
**method** : **PUT**

**返回示例**:
```
 PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/active

 RESPONSE: 
 200 ok
 {
	 ...
     'online': true,
     ...
 }
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| online         |true 代表启用成功  |
 
----
#####2.暂停频道
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/pause**
**method** : **PUT**

**返回示例**:
```
 PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/pause

 RESPONSE:
 200 ok
 {
     ...
     'online': false,
     ...
 }
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| online        |false 代表频道暂停成功|


----
#####3.下发配置

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/distribute**
**method** : **PUT**

**返回示例**:

``` 
 PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/distribute

 RESPONSE: 
 200 ok
 {
	  ...
     'applied': true,
      ...
 }
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
| applied         |true 代表最新的配置已经下发|


----

#### 频道黑白名单/防盗链管理

#####1.查询黑白名单/防盗链

**url** : ROOT_DOMAIN/PN/channel/CHANNEL_ID/blackwhite
**method** : GET
 
**返回示例**:
```
 GET ROOT_DOMAIN/PN/channel/CHANNEL_ID/blackwhite

 RESPONSE: 
 200 ok
 {
     'id': ID, 
     'blackips': BLACK_IPS, 
     'whiteips': WHITE_IPS,
     'referer': REFERER,
     'channel_id': CHANNEL_ID
 }
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| id             |频道id|
| blackips       |黑名单IP列表，由分号分隔多个 |
| whiteips       |白名单IP列表，由分号分隔多个 |
| referer        |防盗链 URL 列表，由分号分隔多个|
| channel_id     |所在频道id|


----

 
#####2.添加/修改/删除 黑白名单/防盗链
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/blackwhite**
**method** : **PUT**
 
**body**:

| 字段      | 必填性|  说明   |
| --------| :----:| ----   |
|blackips  |  O| 黑名单IP列表，由分号分隔多个 新增一个应追加在原有列表之后并提交，删除传递空内容即可|
|whiteips  |O| 白名单IP列表，由分号分隔多个 新增一个应追加在原有列表之后并提交，删除传递空内容即可|
|referer   |  O| 防盗链 URL 列表，由分号分隔多个，新增一个应追加在原有列表之后并提交，删除传递空内容即可|


**返回示例**:
```
 PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/blackwhite
 
 RESPONSE: 
 200 ok
 {
     ’id': ID, 
     'blackips': *BLACK_IPS*,
     'whiteips': *WHITE_IPS*,
     'referer': *REFERER*,
     'channel_id':CHANNEL_ID
 }
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| id             |频道id|
| blackips       |黑名单IP列表，由分号分隔多个 |
| whiteips       |白名单IP列表，由分号分隔多个 |
| referer        |防盗链 URL 列表，由分号分隔多个|


----

#### 目录刷新

#####1.查询目录刷新任务历史

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID/dir-refresh**
**method** : **GET**

**返回示例**: 
```
 GET ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID/dir-refresh

 RESPONSE: 
 200 ok
 [{
            "created": REFRESH_CREAT_TIME,
	    "orig_reg": ORIG_REG,
	    "domain_id": DOAMIN_ID,
	    "refresh_reg": REFRESH_REG,
	    "valid_time": VALID_TIME,
	    "id": REFRESH_ID
 }]
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| created        |刷新创建的时间     |
| orig_reg       |目录刷新正则       |
| domain_id      |所在域id     |
| refresh_reg    |编译过的正则(目前一样)  |
| id             |刷新id    |
 
----

#####2.添加目录刷新任务

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID/dir-refresh**
**method** : **POST**
 
**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|orig_reg  |  M   |目录刷新正则|

**返回示例**:
```
 POST ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID/dir-refresh
 
 RESPONSE: 
 201 created 
 [{
     "created": REFRESH_CREAT_TIME,
	"orig_reg": *ORIG_REG*,
	"domain_id": DOMAIN_ID,
	"refresh_reg":REFRESH_REG,
	"valid_time": VALID_TIME,
	"id": REFRESH_ID
 }]
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| created        |刷新创建的时间     |
| orig_reg       |目录刷新正则       |
| domain_id      |所在域id     |
| refresh_reg    |编译过的正则(目前一样) |
| id             |刷新id    |


----
 
#### 缓存规则

#####1.查询缓存规则
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID/cache-rules**
**method** : **GET**
 
**返回示例**:
```
  GET ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID/cache-rules
  
  RESPONSE:
  200 ok 
  [
      {
        "reg_path": REG_PATH,
	"max_age": MAX_AGE,
	"created": CACHE_RULE_CREAT_TIME,
	"domain_id": DOMAIN_ID,
	"orig_path": ORIG_PATH,
	"cond_id": COND_ID,
	"order_num": ORDER_NUM,
	"id": CACHE_ID
      }
  ]
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| reg_path       |编译过正则(目前一样)    |
| max_age        |缓存的最长时间，只能是数字或者字符串 “no-cache”|
| created        |缓存创建时间 |
| domain_id      |所在域id  |
| orig_path      |缓存路径正则   |
| order_num      |缓存规则的顺序 数值越小越先匹配|
| id             |缓存id    |


----
 
#####2.添加缓存规则
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID/cache-rules**
**method** : **POST**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|order_num |  M   |缓存规则的顺序 数值越小越先匹配|
|orig_path |  M   |缓存规则|
|max_age   |  M   |缓存的最长时间，只能是数字或者字符串 “no-cache”|

**返回示例**:
```
  POST ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID/cache-rules

  RESPONSE: 
  201 created
  [
      {
        "reg_path": REG_PATH,
	"max_age": *MAX_AGE*,
	"created": CACHE_RULE_CREAT_TIME,
	"domain_id": DOMAIN_ID,
	"orig_path": *ORIG_PATH*,
	"cond_id": COND_ID,
	"order_num": *ORDER_NUM*,
	"id": CACHE_ID
      },
      ...
  ]
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| reg_path       |编译过正则(目前一样) |
| max_age        |设置的缓存的最长时间|
| created        |缓存创建时间 |
| domain_id      |所在域id  |
| orig_path      |缓存规则   |
| order_num      |设置的缓存规则的顺序|
| id             |缓存id    |


----

 
#####3.修改/删除缓存规则
 
**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID/cache-rules**
**method** : **PUT**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|cache_rules|  M   |cache_rule对象|
 
**返回示例**:
```
  PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/domain/DOMAIN_ID/cache-rules
  
  RESPONSE: 
  200 ok
  [
      {
        "reg_path": *REG_PATH*,
	"max_age": *MAX_AGE*,
	"created": *CACHE_RULE_CREAT_TIME*,
	"domain_id": *DOMAIN_ID*,
	"orig_path": *ORIG_PATH*,
	"cond_id": *COND_ID*,
	"order_num": *ORDER_NUM*,
	"id": *CACHE_ID*
      },
      ...
  ]
删除只需改变cache_rules这个数组里cache_rule对象个数即可
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------      | -------------   |
| reg_path       |编译过正则(目前一样)   |
| max_age        |缓存的最长时间，只能是数字或者字符串 “no-cache”|
| created        |缓存创建时间 |
| domain_id      |所在域id  |
| orig_path      |缓存规则   |
| order_num      |缓存规则的顺序 数值越小越先匹配|
| id             |缓存id    |


----

####自定义配置文件

#####1.查询自定义配置文件

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/conf**
**method** : **GET**

**返回示例**:
```
   GET ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/conf

   RESPONSE: 
   200 ok
   {
	"status": true,
	"remark": null,
	"created": CONF_CREAT_TIME,
	"channel_id": CHANNEL_ID,
	"conf": CONF,
	"id": CONF_ID
}
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
|  status         |    |
| remark          |     |
| created         |配置文件创建时间 |
| channel_id      |频道id  |
| conf            |配置文件内容   |
| id              |配置文件id    |


----


#####2.修改自定义配置文件

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/conf**
**method** : **PUT**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|conf      | O   |自定义配置文件内容|

**返回示例**:
```
   PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/conf

   RESPONSE: 
   200 ok
   {
	"status": true,
	"remark": null,
	"created": CONF_CREAT_TIME,
	"channel_id": CHANNEL_ID,
	"conf": *CONF*,
	"id": CONF_ID
}
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
|  status         |    |
| remark          |    |
| created         |配置文件创建时间 |
| channel_id      |频道id  |
| conf            |修改后的配置文件内容   |
| id              |配置文件id    |


----



#####3.查询自定义回源

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/back-source**
**method** : **GET**

**返回示例**:
```
   GET ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/back-source

   RESPONSE: 
   200 ok
   {
	"status": true,
	"remark": null,
	"created": SOURCE_CREAT_TIME,
	"channel_id": CHANNEL_ID,
	"source": SOURCE,
	"id": SOURCE_ID
}
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
|  status         |    |
| remark          |   |
| created         |自定义回源创建时间 |
| channel_id      |频道id  |
| source          |自定义回源(IP:PORT;IP:PORT)   |
| id              |自定义回源id    |


----

#####4.修改自定义回源

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/back-source**
**method** : **PUT**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|source    |   M   |必须是域名或者IP，其中域名只能有一个，IP可以是多个用分号分隔|

**返回示例**:
```
   GET ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/back-source

   RESPONSE:
   200 ok
   {
	"status": true,
	"remark": null,
	"created": SOURCE_CREAT_TIME,
	"channel_id": CHANNEL_ID,
	"source": *SOURCE*,
	"id": SOURCE_ID
}
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
|  status         |    |
| remark          |   |
| created         |自定义回源创建时间 |
| channel_id      |频道id  |
| source          |修改后的源   |
| id              |自定义回源id    |


----

#####5.查询自定义PATH

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/backend-path**
**method** : **GET**

**返回示例**:
```
   GET ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/backend-path

   RESPONSE:
   200 ok
   {
	"status": true,
	"remark": null,
	"created": PATH_CREAT_TIME,
	"channel_id": CHANNEL_ID,
	"path": PATH,
	"id": PATH_ID
}
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
|  status         |    |
| remark          |    |
| created         |自定义PATH创建时间 |
| channel_id      |频道id  |
| path            |自定义回源路径   |
| id              |自定义PATH-id    |


----
#####6.修改自定义PATH

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/backend-path**
**method** : **PUT**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|path      |   O  |PATH|

**返回示例**:
```
   PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/custom/backend-path

   RESPONSE:
   200 ok
   {
	"status": true,
	"remark": null,
	"created": PATH_CREAT_TIME,
	"channel_id": CHANNEL_ID,
	"path": *PATH*,
	"id": PATH_ID
}
```
**返回字段说明**

| 返回值字段      |    说明          |
|--------       | -------------   |
|  status         |    |
| remark          |   |
| created         |自定义PATH创建时间 |
| channel_id      |频道id  |
| path            |修改后自定义回源路径   |
| id              |自定义PATH-id    |


----

####MC源站管理
#####1.查询MC可用源

**url** : **ROOT_DOMAIN/mc/origins**
**method** : **GET**

**返回示例**:
```
   GET ROOT_DOMAIN/mc/origins

   RESPONSE:
   200 ok
   [
	{
	"remark": null,
	"name": MC_NAME,
	"created": MC_CREAT_TIME,
	"source_domain": DOMAIN,
	"id": MC_ORIGIN_ID,
	"port": DOMAIN_PORT
	},
	...
]
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
| remark          |MC可用源备注    |
| name            |MC可用源名称    |
| created         |MC可用源创建时间 |
| source_domain   |域  |
| id              |MC可用源id    |
| port            |端口  |


----

#####2.查询MC源站实例

**url** : **ROOT_DOMAIN/PN/mc/backend/instance**
**method** : **GET**

**返回示例**:
```
   GET ROOT_DOMAIN/PN/mc/backend/instance

   RESPONSE: 
   200 ok
   [
	{
	"ftp_user": FTP_USER,
	"mc_origin":{...},
	"ftp_passwd": FTP_PASSWD,
	"mc_origin_id": MC_ORIGIN_ID,
	"dnspod_id": DNSPOD_ID,
	"created": MC_CREAT_TIME,
	"cname": CNAME,
	"pn": PN,
	"id": INS_ID
	},
	...
]
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
| ftp_user        |   FTP帐号  |
| mc_origin       | MC可用源，见上   |
| ftp_passwd      |   FTP密码   |
| mc_origin_id     |MC可用源id |
| created          | MC源站实例创建时间|
| pn               |产品id    |
| id               | MC源站实例id  |


----


#####3.创建MC源站实例

**url** : **ROOT_DOMAIN/PN/mc/backend/instance**
**method** : **POST**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|mc_origin_id|  M |MC源ID|


**返回示例**:
```
   POST ROOT_DOMAIN/PN/mc/backend/instance

   RESPONSE:
   201 created
	{
	"ftp_user": FTP_USER,
	"mc_origin":{...},
	"ftp_passwd": FTP_PASSWD,
	"mc_origin_id": *MC_ORIGIN_ID*,
	"dnspod_id": DNSPOD_ID,
	"created": MC_CREAT_TIME,
	"cname": CNAME,
	"pn": PN,
	"id": INS_ID
	}	
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
| ftp_user        | FTP帐号   |
| mc_origin       | MC可用源   |
| ftp_passwd      | FTP密码   |
| mc_origin_id     | MC可用源id|
| created          | MC源站实例创建时间   |
| pn               |产品id    |
| id               | MC源站实例id  |




----

#####4.删除MC源站实例

**url** : **ROOT_DOMAIN/PN/mc/backend/instance/MC_BACKEND_INS_ID**
**method** : **DELETE**

**返回示例**:
```
   DELETE ROOT_DOMAIN/PN/mc/backend/instance/MC_BACKEND_INS_ID

   RESPONSE:{}
```
----
#####5.绑定MC源站

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/mc/backend/**
**method** : **POST**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|mcbackend_ins_id|   M |MC源站实例ID|

**返回示例**:
```
   POST ROOT_DOMAIN/PN/channel/CHANNEL_ID/mc/backend/

   RESPONSE:
   201 created
   {
	"channel_id": CHANNEL_ID,
	"mcbackend_ins_id": *MCBACKEND_INS_ID*,
	"mcbackend_ins":{...},
        "id": ID,
	"created": CREAT_TIME
}
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
| channel_id      | 频道id   |
| mcbackend_ins_id|  绑定的MC源站实例ID|
| mcbackend_ins   |  绑定的MC源站实例内容 说明见*创建MC源站实例*|
| created         | 绑定创建时间|


----

#####6.修改绑定MC源站

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/mc/backend/MCBACKEND_ID**
**method** : **PUT**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|mcbackend_ins_id|   M |MC源站实例ID|

**返回示例**:
```
   PUT ROOT_DOMAIN/PN/channel/CHANNEL_ID/mc/backend/MCBACKEND_ID

   RESPONSE:
   200 ok
   {
	"channel_id": CHANNEL_ID,
	"mcbackend_ins_id": *MCBACKEND_INS_ID*,
	"mcbackend_ins":{...},
        "id": ID,
	"created": CREAT_TIME
}
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
| channel_id      | 频道id   |
| mcbackend_ins_id|  绑定的MC源站实例ID|
| mcbackend_ins   |  绑定的MC源站实例内容 说明见*创建MC源站实例*|
| created         | 绑定创建时间|


----

#####7.解除MC源站

**url** : **ROOT_DOMAIN/PN/channel/CHANNEL_ID/mc/backend/MCBACKEND_ID**
**method** : **DELETE**

**返回示例**:
```
   DELETE ROOT_DOMAIN/PN/channel/CHANNEL_ID/mc/backend/MCBACKEND_ID

   RESPONSE:{}
```

----

#####8.修改MC源站实例所选的MC源类型

**url** : **ROOT_DOMAIN/PN/mc/backend/instance/MC_BACKEND_INS_ID/type**
**method** : **PUT**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|mc_origin_id|   O |MC可用源ID|

**返回示例**:
```
   PUT ROOT_DOMAIN/PN/mc/backend/instance/MC_BACKEND_INS_ID/type

   RESPONSE:
   200 ok
   {
	"ftp_user": FTP_USER,
	"mc_origin":{...},
	"ftp_passwd": FTP_PASSWD,
	"mc_origin_id": *MC_ORIGIN_ID*,
	"dnspod_id": DNSPOD_ID,
	"created": MC_CREAT_TIME,
	"cname": CNAME,
	"pn": PN,
	"id": INS_ID
}
```
**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
| ftp_user        | FTP帐号   |
| mc_origin       | MC可用源   |
| ftp_passwd      | FTP密码   |
| mc_origin_id     | 修改后的MC可用源id|
| created          | MC源站实例创建时间   |
| pn               |产品id    |
| id               | MC源站实例id  |


----

#####9.修改MC源站实例FTP帐号或密码

**url** : **ROOT_DOMAIN/PN/mc/backend/instance/MC_BACKEND_INS_ID/ftp**
**method** : **PUT**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|ftp_user|  O |FTP帐号|
|ftp_passwd|  O |FTP密码|

**返回示例**:
```
   PUT ROOT_DOMAIN/PN/mc/backend/instance/MC_BACKEND_INS_ID/ftp

   RESPONSE:
   200 ok
   {
	"ftp_user": *FTP_USER*,
	"mc_origin":{...},
	"ftp_passwd": *FTP_PASSWD*,
	"mc_origin_id": MC_ORIGIN_ID,
	"dnspod_id": DNSPOD_ID,
	"created": MC_CREAT_TIME,
	"cname": CNAME,
	"pn": PN,
	"id": INS_ID
}
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
| ftp_user        | 修改后的FTP帐号   |
| mc_origin       | MC可用源   |
| ftp_passwd      | 修改后的FTP密码   |
| mc_origin_id     | MC可用源id|
| created          | MC源站实例创建时间   |
| pn               |产品id    |
| id               | MC源站实例id  |


----

#### 文件md5校验

#####1. 新建文件md5校验任务

**url** : **ROOT_DOMAIN/md5**
**method** : **POST**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|channel_id|  O |频道id|
|pn|  O |产品id|
|url|  O ||

**返回示例**:

```
   POST ROOT_DOMAIN/md5

   RESPONSE:
   201 created
   {
	"task_id": TASK_ID
}
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
| backend         | 见下  |
| cdn_nodes       | 见下  |
| status          | 状态为 doing 时 cdn_nodes 的 list 会不断增加直到状态为 done 时完成 |

backend

| 返回值字段      |    说明          |
| :--------       | :-------------   |
| avg_speed       |   平均速度(kB/s)|
| backend         |   源站地址|
| content_length  |   内容长度|
| curl_code       |   curl状态码|
| curl_msg        |   curl信息|
| http_code       |   http状态码|
| md5_value       |   md5值|
| success         |   true or false|
| total_time      |   总时间|
| url             |   资源链接|

cdn_nodes

| 返回值字段      |    说明          |
| :--------       | :-------------   |
| avg_speed       |   平均速度(kB/s)|
| backend         |   源站地址|
| content_length  |   内容长度|
| curl_code       |   curl状态码|
| curl_msg        |   curl信息|
| http_code       |   http状态码|
| md5_value       |   md5值|
| success         |   true or false|
| total_time      |   总时间|
| url             |   资源链接|



----

##### 2. 查看文件md5校验结果

**url** : **ROOT_DOMAIN/md5/TASK_ID**
**method** : **GET**

**返回示例**:

```
   GET ROOT_DOMAIN/md5/TASK_ID

   RESPONSE:
   200 ok
   {
     "backend": {
                "avg_speed": "1108598.00"
                "backend": "cdnorigin.mlt01.com"
                "content_length": "13.55"
                "curl_code": "0"
                "curl_msg": "ok"
                "http_code": "200"
                "md5_value": "d810e2b0c699dcf6e864b55fa3df84fb"
                "success": true
                "total_time": "0.013"
                "url": "http://www.tan14.cn/hash.js"
               },
     "cdn_nodes": [
                   {
                     "avg_speed": "349851.00"
                     "content_length": "13.55"
                     "curl_code": "0"
                     "curl_msg": "ok"
                     "http_code": "200"
                     "ip": "60.6.200.137"
                     "ip_info": "河北 , 邢台 , 联通 "
                     "md5_value": "d810e2b0c699dcf6e864b55fa3df84fb"
                     "success": true
                     "total_time": "0.040"
                     "url": "http://www.tan14.cn/hash.js"
                    },
                  ...
                  ],
       "status": "doing" 状态为 doing 时 cdn_nodes 的 list 会不断增加直到状态为 done 时完成
}
```

**返回字段说明**

| 返回值字段      |    说明          |
| --------       | -------------   |
| task_id        | 该md5校验任务id   |



----

####缓存和预加载

**ROOT_DOMAIN** : https://api.tan14.cn/wp

#####1. 刷新缓存

刷新CDN上的cache文件

**url** : **ROOT_DOMAIN/PN/channel/refresh**
**method** : **POST**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|url|  O |必须以http或https开头|


**返回示例**：
```
   POST ROOT_DOMAIN/PN/channel/refresh
   
   RESPONSE:
   201 created
   {
       "do_time":DO_TIME,
       "weight":WEIGHT,
       "url":*URL*,
       "is_preload":IS_PRELOAD 0 or 1,
       "progress":PROGRESS,
       "nodes":NODES,
       "group_id":GROUP_ID,
       "pn":PN,
       "id":ID
    }
```

**返回字段说明**

| 返回值字段     |    说明          |
| --------     | -------------   |
| do_time       |   任务完成时间|
| weight        |   权重|
| url           |   资源链接|
| is_preload    |   是否是预加载|
| progress      |   进度|
| nodes         |   节点|
| group_id      |   分组ID|
| pn            |   产品ID|
| id            |   ID|


#####2. 缓存预加载

预加载cache文件到CDN

**url** : **ROOT_DOMAIN/PN/channel/preload**
**method** : **POST**

**body**:

| 字段     |必填性|   说明   |
| --------| :----:| ----   |
|url|  O |必须以http或https开头|


**返回示例**：
```
   POST ROOT_DOMAIN/PN/channel/preload
   
   RESPONSE:
   201 created
   {
       "do_time":DO_TIME,
       "weight":WEIGHT,
       "url":*URL*,
       "is_preload":IS_PRELOAD 0 or 1,
       "progress":PROGRESS,
       "nodes":NODES,
       "group_id":GROUP_ID,
       "pn":PN,
       "id":ID
 }
```
**返回字段说明**

| 返回值字段     |    说明          |
| --------     | -------------   |
| do_time       |   任务完成时间|
| weight        |   权重|
| url           |   资源链接|
| is_preload    |   是否是预加载|
| progress      |   进度|
| nodes         |   节点|
| group_id      |   分组ID|
| pn            |   产品ID|
| id            |   ID|



----

####数据统计

**url** : **https://b3ca82d03d71296d.tan14.net/jsons**
**method** : **GET**

**返回示例**：
```
   GET https://b3ca82d03d71296d.tan14.net/jsons

   RESPONSE:
   200 ok 

   DATAS_PATH = "c_" + CHANNEL_ID
   DATAS_TYPE:为以下三种类型之一
   min.json 返回最近两天之内的数据 五分钟一个点
   hour.json 返回最近一个月之内的数据 每小时一个点
   day.json 返回一个月以上的数据 一天一个点
  
   {
    "data":[
             "HOSTNAME":{
                         "B":{
                             "cs":,
                             "ht":,
                             "ms":,
                             "ps":, 
                             "total":
                            },
                          "F":{
                             "cs":,
                             "ht":,     *//hit 流量*    
                             "ms":,     *//miss 流量*    
                             "ps":,     *//pass 流量*    
                             "total":     *// 总流量*    
                           },
                          "bps":{
                             "delay":,     *//回源响应时间*    
                             "delay_dynamic":,     *//# 暂未使用*    
                             "delay_source":     *//结点响应时间*    
                           },
                          "req":{
                             "4xx":,     *//节点返回*    
                             "4xx_bak":,     *//源站返回*    
                             "4xx_dyn":,     *//暂未使用*    
                             "5xx":,
                             "5xx_bak":,5xx_dyn:,
                             "403":,
                             "403_bak":,
                             "403_dyn":,
                             "404":,
                             "404_bak":,
                             "404_dyn":,
                             "502":,
                             "502_bak":,
                             "502_dyn":,
                             "503":,
                             "503_bak":,
                             "503_dyn":,
                             "504":,
                             "504_bak":,
                             "504_dyn":,
                             "cs":,     *//暂未使用*    
                             "ht":,     *//hit 次数*    
                             "ms":,     *//miss 次数*    
                             "ps":,     *//pass 次数*    
                             "total":     *// 总请求次数*    
                          }
           }
     ],
    "time":[]每个时间对应着每个 data 里的数据
 }

HOSTNAME: 6 位大写英文字符 1-3 位 :ISP (详见 ISP_DICT ) 4-6 位 :AREA( 详见 AREA_DICT)

ISP_DICT = {"CTC":"电信","CUC":"联通"(包括网通),"CMC":"移动","CTT":"铁通","CEN":"教育网","OCN":"有线通","DXT":"电信通","DWN":"双线","BGP":"五线 BGP","GWB":"长城宽带","BGC":"歌华","WAS":"杭州华数"};

AREA_DICT = {'GDY':'台湾 ','FJM':' 福建 ','SDL':' 山东 ','JSS':' 江苏 ','AHW':' 安徽 ','SHH':' 上海 ','ZJZ':' 浙江 ','JXG':' 江西 ','TWN':'广东 ','GXG':' 广西 ','HNY':' 河南 ','HBE':' 湖北 ','HNX':' 湖南 ','HNQ':' 海南 ','BJJ':' 北京 ','NMG':' 内蒙古 ','SXJ':' 山西 ','TJJ':' 天津 ','HBJ':' 河北 ','GZQ':' 贵州 ','CQY':' 重庆 ','YND':' 云南 ','XZZ':' 西藏 ','SCC':' 四川 ','NXN':' 宁夏 ','SXS':' 陕西 ','GSL':' 甘肃 ','XJX':' 新疆 ','QHQ':' 青海 ','HLJ':' 黑龙江 ','JLJ':' 吉林 ','LNL':' 辽宁 '};

```

----
