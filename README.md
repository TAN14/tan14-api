#TAN 14 API 文档




-------------------

[TOC]

## 认证方式

**API URL：`https://api.tan14.cn/wp/`**

登录 TAN14 后台，在『帐户』中查看 API-KEY。在 HTTP 请求头中添加 API-KEY 到 TAN14-KEY 。 
示例：
>GET /some/path
>TAN14-Key: d3cafb4dde4dbeef
>Accept: application/json

-------------------
## 一、配置CDN

**CDN配置与修改**

参数列表：
pn：产品ID，登录 TAN14 后台在『帐户』中查看产品ID；
id：频道ID，登录 TAN14 后台在『设置』中查看频道ID
domain：域名
remark：频道名称/域名注释
pingback：测试连接，用户测试CDN配置是否生效
backend：源站IP
applied：0 为未下发配置 1 已经下发配置
online：0 是暂停频道 1 是开启频道
port：端口
ssl：0 为开启ssl 1 为未开启ssl
applied：0 配置未下发 1 配置已下发
status：0 频道已开启 1 频道未开启
is_rsuffix:0 不忽略queryString 1 忽略queryString


-------------------
###1.频道的配置与操作

####快速添加频道
 快速添加一个新频道
 方法：
 >**POST /pn/quick_channel**

请求示例：

 >POST /79cc7771b422d2644eb798/quick_channel
 >TAN14-KEY:d3cafb4dde4dbeef
 >Content-Type: application/x-www-form-urlencoded
 >Accept: application/json
 ><body>
 >remark=MyFirstCdn <font color="#8F8FBD">*//频道名称，未填写时等于domain*</font>
 >domain=www.mydemo.com
 >pingback= `http://www.mydemo.com/noc.gif`<font color="#8F8FBD">*//pingback域名应与domain保持一致,必须以http或https开头*</font>
 >backend=127.0.0.1
 >port=80<font color="#8F8FBD">*//端口，未填写时默认80*</font>

返回示例：

>HTTP/1.1 201 Created
>Content-Type: application/json
>
>{
    &nbsp;“applied”: 0,
    &nbsp;“remark”: “MyFirstCdn”,
    &nbsp;“pn”: “79cc7771b422d2644eb798”,
    &nbsp;“id”: “cca78d747d66822a182172”,
    &nbsp;“online”: 1
    }

####查看所有频道列表

方法：

 >**GET /pn/channel**

列出产品下的所有频道

请求示例：
>GET /79cc7771b422d2644eb798/channel
>TAN14-KEY: d3cafb4dde4dbeef 
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
>[
   &nbsp;{
    &nbsp;&nbsp;“applied”: 0,
    &nbsp;&nbsp;“remark”: “MyFirstCdn”,
    &nbsp;&nbsp;“pn”: “79cc7771b422d2644eb798”,
    &nbsp;&nbsp;“id”: “cca78d747d66822a182172”,
    &nbsp;&nbsp;“online”: 1
    &nbsp;},
    &nbsp;{
    &nbsp;&nbsp;“applied”: 0,
    &nbsp;&nbsp;“remark”: “smile”,
    &nbsp;&nbsp;“pn”: “79cc7771b422d2644eb798”,
    &nbsp;&nbsp;“id”: “02378ca383057f21ce68bc”,
    &nbsp;&nbsp;“online”: 0
    &nbsp;},
    &nbsp;{
    &nbsp;&nbsp; “applied”: 1,
    &nbsp;&nbsp;“remark”: “测试”,
    &nbsp;&nbsp;“pn”: “79cc7771b422d2644eb798”,
    &nbsp;&nbsp;“id”: “f597ba0b727fc1fb3134bf”,
    &nbsp;&nbsp;“online”: 0
    &nbsp;}
  ]

####查看频道状态

查看一个频道的状态

方法：

>**GET pn/channel/id**

请求示例：
>GET /79cc7771b422d2644eb798/channel/cca78d747d66822a182172
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
  {
    &nbsp;“applied”: 0,
    &nbsp;“remark”: “MyFirstCdn”,
    &nbsp;“pn”: “79cc7771b422d2644eb798”,
    &nbsp;“id”: “cca78d747d66822a182172”,
    &nbsp;“online”: 1
    }

####查看频道详情

查看一个频道的详细信息

方法：
>**GET /pn/channel/id/details**

请求示例：
>GET /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/details
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
    {
    &nbsp;“applied”:0,
    &nbsp;“remark”:”MyFirstCdn”,
    &nbsp;“backends”:
    &nbsp;[{
    &nbsp;&nbsp;“status”:1,
    &nbsp;&nbsp;“name”:”127.0.0.1”, <font color="#8F8FBD">*//源站名称，初始值等于backend*</font>
    &nbsp;&nbsp;“id”:337,
    &nbsp;&nbsp;“channel_id”:”cca78d747d66822a182172”,
    &nbsp;&nbsp;“port”:80,
    &nbsp;&nbsp;“backend”:”127.0.0.1”
    &nbsp;}],
    &nbsp;“online”:1,
    &nbsp;“domains”:
    &nbsp;[{
    &nbsp;&nbsp;“domain”:”www.mydemo.com”,
    &nbsp;&nbsp;“ssl”:1,
    &nbsp;&nbsp;“pingback”:”`http://www.mydemo.com/noc.gif`“,
    &nbsp;&nbsp;“remark”:”MyFirstCdn”,<font color="#8F8FBD">*//域名注释，初始值等于domain*</font>
    &nbsp;&nbsp;“channel_id”:”cca78d747d66822a182172”,
    &nbsp;&nbsp;“cname”:”df7b86b9662666af.limejs.cn”,
    &nbsp;&nbsp;“id”:277
    &nbsp;}],
    &nbsp;“pn”:”79cc7771b422d2644eb798”,
    &nbsp;“id”:”cca78d747d66822a182172”
    }

####修改频道名称

修改频道名称remark

方法：
>**PUT /pn/channel/id**

请求示例：
>PUT /79cc7771b422d2644eb798/channel/cca78d747d66822a182172
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json
><body>
>remark=MyCdn

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
  {
    &nbsp;“applied”: 0,
    &nbsp;“remark”: “MyCdn”,
    &nbsp;“pn”: “79cc7771b422d2644eb798”,
    &nbsp;“id”: “cca78d747d66822a182172”,
    &nbsp;“online”: 1
    }


####查看配置是否下发

查看一个频道下的配置是否下发生效

方法：
>**GET /pn/channel/id/applied**

请求示例：
>GET /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/applied
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
    {
    &nbsp;“applied”:0
    }

####下发配置

下发频道配置

方法：
>**PUT /pn/channel/id/applied**

请求示例：
>PUT /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/applied
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
    {
    &nbsp;“applied”:1,
    &nbsp;“remark”:”MyCdn”,
    &nbsp;“pn”:”79cc7771b422d2644eb798”,
    &nbsp;“id”:”cca78d747d66822a182172”,
    &nbsp;“online”:1
    }

####开启频道

开启一个频道

方法：
>**POST /pn/channel/id/online**

请求示例：
>POST /79cc7771b422d2644eb798/channel/f597ba0b727fc1fb3134bf/online
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
    {
    &nbsp;“status”:1
    }

####暂停频道

暂停一个频道

方法：
>**DELETE /pn/channel/id/online**

请求示例：
>DELETE /79cc7771b422d2644eb798/channel/f597ba0b727fc1fb3134bf/online
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
    {
    &nbsp;“status”:0
    }


###2.域的配置与操作

####查看域名详情

查看指定频道下域名的详细信息

方法：
>**GET /pn/channel/id/domain**

请求示例：
>GET /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/domain
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
{
    &nbsp;“domain”:”www.mydemo.com”,
    &nbsp;“ssl”:1,
    &nbsp;“pingback”:”`http://www.mydemo.com/noc.gif`“,
    &nbsp;“remark”:”MyCdn”,
    &nbsp;“is_rsuffix”: 0,
    &nbsp;“channel_id”:”cca78d747d66822a182172”,
    &nbsp;“cname”:”df7b86b9662666af.limejs.cn”
    }

####新建域名

在频道下添加一个新的域名

方法：
>**POST /pn/channel/id/domain**

请求示例：
>POST /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/domain
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json
><body>
>remark=ANewDomain <font color="#8F8FBD">*//未填写时等于domain*</font>
>domain=www.newdomain.com
>pingback= `http://www.newdomain.com/noc.gif`
>ssl=0 <font color="#8F8FBD">*//未设置时默认为0*</font>
>is_rsuffix=1 <font color="#8F8FBD">*//未设置时默认为0*</font>

返回示例：
>HTTP/1.1 201 Created
>Content-Type: application/json
    {
    &nbsp;“domain”:”www.newdomain.com”,
    &nbsp;“ssl”:0,
    &nbsp;“pingback”:`https://www.newdomain.com/noc.gif`“,
    &nbsp;“remark”:”ANewDomain”,
    &nbsp;“is_rsuffix”: 0,
    &nbsp;“channel_id”:”b69d7e81a3be9c1922f4f6”,
    &nbsp;“cname”:”4e7613513e8ce127.limejs.cn”
    }

####修改域名

修改一个已存在的域名

方法：
>**PUT /pn/channel/id/domain/domain**

请求示例：
>PUT /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/domain/www.newdomain.com
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json
><body>
>remark=EditedDomain
>domain=www.editeddomain.com
>pingback= `http://www.editeddomain.com/noc.gif`
>ssl=1
>is_rsuffix=0

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
   {
    &nbsp;“domain”:”www.editeddomain.com”,
    &nbsp;“ssl”:1,
    &nbsp;“pingback”:`https://www.editeddomain.com/noc.gif`“,
    &nbsp;“remark”:”EditedDomain”,
    &nbsp;“is_rsuffix”: 0,
    &nbsp;“channel_id”:”b69d7e81a3be9c1922f4f6”,
    &nbsp;“cname”:”4e7613513e8ce127.limejs.cn”
    }

####删除域名

删除频道下的一个域名

方法：
>**DELETE /pn/channel/id/domain/domain_name**

请求示例：
>DELETE /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/domain/www.mydemo.com
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json


###3.源站的配置与操作
####获取源站信息

获取一个频道下源站列表

方法
>**GET /pn/channel/id/backend**

请求示例：
>GET /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/backend
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
{
    &nbsp;“status”:1,
    &nbsp;“port”:80,
    &nbsp;“name”:”127.0.0.1”,
    &nbsp;“backend”:”127.0.0.1”
    }

####添加源站

在频道下添加一个新的源站

方法
>**POST /pn/channel/id/backend**

请求示例：
>POST /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/backend
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json
><body>
>name=NewServer
>backend=127.0.0.2
>port=80
>status=1

返回示例：
>HTTP/1.1 201 created
>Content-Type: application/json
{
    &nbsp;“status”:1,
    &nbsp;“port”:80,
    &nbsp;“name”:”NewServer”,
    &nbsp;“backend”:”127.0.0.2”
    }

####修改源站

修改频道下添加的一个源站

方法
>**PUT /pn/channel/id/backend/backend_name**

请求示例：
>PUT /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/backend/NewServer
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json
><body>
>name=EditedServer
>backend=127.0.0.3
>port=8080

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
{
    &nbsp;“status”:1,
    &nbsp;“port”:8080,
    &nbsp;“name”:”EditedServer”,
    &nbsp;“backend”:”127.0.0.3”
    }

####删除源站

删除频道下的一个源站

方法
>**DELETE /pn/channel/id/backend/backend_name**

请求示例：
>DELETE /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/backend/EditedServer
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json

##二、安全管理

###1.黑名单管理

####添加/修改黑名单

**添加黑名单(现频道中不含黑名单）/修改黑名单(现频道中含黑名单）**

方法：
>**PUT /pn/channel/id/blackwhite**

请求示例：
>PUT /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/blackwhite
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json
><body>
>black_ips=1.1.1.1;1.1.1.2 <font color="#8F8FBD">*//IP之间用分号分隔*</font>

返回示例：
>HTTP/1.1 201 Created(添加) 200 OK(修改)
>Content-Type: application/json
{
    &nbsp;“black_referers”: null,
    &nbsp;“channel_id”: "cca78d747d66822a182172",
    &nbsp;“white_ips”: null,
    &nbsp;“black_ips”: "1.1.1.1;1.1.1.2"
    }

####查看黑名单

方法：
>**GET /pn/channel/id/blackwhite**

请求示例：
>GET /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/blackwhite
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
{
    &nbsp;“black_referers”: null,
    &nbsp;“channel_id”: "cca78d747d66822a182172",
    &nbsp;“white_ips”: null,
    &nbsp;“black_ips”: "1.1.1.1;1.1.1.2"
    }

###2.防盗链管理

####添加/修改防盗链

**添加防盗链(现频道中不含防盗链）/修改防盗链(现频道中含防盗链）**

方法：
>**PUT /pn/channel/id/blackwhite**

请求示例：
>PUT /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/blackwhite
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json
><body>
>black_referers=`http://baidu.com/`;2.3.4.5 <font color="#8F8FBD">*//REFERERS之间用分号分隔,必须以http或https开头,或者为IP*</font>

返回示例：
>HTTP/1.1 201 Created(添加) 200 OK(修改)
>Content-Type: application/json
{
    &nbsp;“black_referers”: "`http://baidu.com/`;2.3.4.5",
    &nbsp;“channel_id”: "cca78d747d66822a182172",
    &nbsp;“white_ips”: null,
    &nbsp;“black_ips”: "1.1.1.1;1.1.1.2"
    }

####查看防盗链

方法：
>**GET /pn/channel/id/blackwhite**

请求示例：
>GET /79cc7771b422d2644eb798/channel/cca78d747d66822a182172/blackwhite
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json
{
    &nbsp;“black_referers”: "`http://baidu.com/`;2.3.4.5",
    &nbsp;“channel_id”: "cca78d747d66822a182172",
    &nbsp;“white_ips”: null,
    &nbsp;“black_ips”: "1.1.1.1;1.1.1.2"
    }

###3.文件md5校验

**API URL：`https://api.tan14.cn`**

####新建文件md5校验任务

方法：
>**POST /useful/md5**

请求示例：
>POST /useful/md5
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json
>
>channel_id=cca78d747d66822a182172
>pn=79cc7771b422d2644eb798
>url=`http://www.editeddomain.com/1.img`　<font color="#8F8FBD">*//必须以http或https开头*</font>

返回示例：
>HTTP/1.1 201 Created
>Content-Type: application/json
{
   &nbsp;“task_id”:"54c612d433a4bd6157cf2913"
   }

####查看文件md5校验结果

方法：
>**GET /useful/md5/task_id**

请求示例：
>GET /useful/md5/54c612d433a4bd6157cf2913
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json

返回示例：
>HTTP/1.1 200 OK
>Content-Type: application/json


##三、刷新和预加载

**刷新和预加载缓存文件**

参数列表：
do_time：任务执行时间
weight：任务权重
is_preload：是否未预加载 1:是 0:否
nodes：刷新任务影响到的节点数量 格式为：a/b a大于等于b的值时 刷新成功
progress：任务执行状态 0:任务未执行 1:任务正在执行 2:任务执行完成
id：任务ID

-------------------
###刷新缓存

刷新CDN上的cache文件

方法：
>**POST /pn/channel/refresh**

请求示例：
>POST /79cc7771b422d2644eb798/channel/refresh
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json
><body>
>url=`http://www.mydemo.com/img.jpg|http://www.mydome.com/img1.jpg`<font color="#8F8FBD">*//必须以http或https开头*</font>

返回示例：
>HTTP/1.1 201 Created
>Content-Type: application/json
{
    &nbsp;“do_time”:”1422010559.76403”,
    &nbsp;“weight”:1,
    &nbsp;“url”:”`http://www.mydemo.com/img.jpg|http://www.mydome.com/img1.jpg`”,
    &nbsp;“is_preload”:0,
    &nbsp;“progress”:0,
    &nbsp;“nodes”:null,
    &nbsp;“group_id”:1,
    &nbsp;“pn”:”79cc7771b422d2644eb798”,
    &nbsp;“id”:120591
    }

###缓存预加载

预加载cache文件到CDN

方法：
>**POST /pn/channel/preload**

请求示例：
>POST /C79cc7771b422d2644eb798/channel/preload
>TAN14-KEY: d3cafb4dde4dbeef
>Content-Type: application/x-www-form-urlencoded
>Accept: application/json
><body>
>url=`http://www.mydemo.com/img.jpg|http://www.mydome.com/img1.jpg`<font color="#8F8FBD">*//必须以http或https开头*</font>

返回示例：
>HTTP/1.1 201 Created
>Content-Type: application/json
{
    &nbsp;“do_time”:”1422010754.62778”,
    &nbsp;“weight”:1,
    &nbsp;“url”:”`http://www.mydemo.com/img.jpg|http://www.mydome.com/img1.jpg`”,
    &nbsp;“is_preload”:1,
    &nbsp;“progress”:0,
    &nbsp;“nodes”:null,
    &nbsp;“group_id”:1,
    &nbsp;“pn”:”79cc7771b422d2644eb798”,
    &nbsp;“id”:120592
 }

##四、数据统计

**API URL : `https://b3ca82d03d71296d.tan14.net/jsons`**

方法：
>**GET /DATAS_PATH/DATAS_TYPE**

DATAS_PATH = "c_" + CHANNEL_ID
DATAS_TYPE:为以下三种类型之一
min.json 返回最近两天之内的数据 五分钟一个点
hour.json 返回最近一个月之内的数据 每小时一个点
day.json 返回一个月以上的数据 一天一个点

返回结构为：
>{
  &nbsp;data:[
  &nbsp;&nbsp;HOSTNAME:{  <font color="#8F8FBD">*//HOSTNAME解释见段尾*</font>
  &nbsp;&nbsp;&nbsp;B:{
  &nbsp;&nbsp;&nbsp;&nbsp;cs:, <font color="#8F8FBD">*//暂未使用*</font>
  &nbsp;&nbsp;&nbsp;&nbsp;ht:, <font color="#8F8FBD">*//hit 带宽*</font>
  &nbsp;&nbsp;&nbsp;&nbsp;ms:, <font color="#8F8FBD">*//miss 带宽*</font>
  &nbsp;&nbsp;&nbsp;&nbsp;ps:, <font color="#8F8FBD">*//pass 带宽*</font>
  &nbsp;&nbsp;&nbsp;&nbsp;total: <font color="#8F8FBD">*// 总带宽*</font>
   &nbsp;&nbsp;&nbsp;},
   &nbsp;&nbsp;&nbsp;F:{
   &nbsp;&nbsp;&nbsp;&nbsp;cs:, <font color="#8F8FBD">*//暂未使用*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;ht:, <font color="#8F8FBD">*//hit 流量*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;ms:, <font color="#8F8FBD">*//miss 流量*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;ps:, <font color="#8F8FBD">*//pass 流量*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;total: <font color="#8F8FBD">*// 总流量*</font>
   &nbsp;&nbsp;&nbsp;},
   &nbsp;&nbsp;&nbsp;bps:{
   &nbsp;&nbsp;&nbsp;&nbsp;delay:, <font color="#8F8FBD">*//回源响应时间*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;delay_dynamic:, <font color="#8F8FBD">*//# 暂未使用*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;delay_source: <font color="#8F8FBD">*//结点响应时间*</font>
   &nbsp;&nbsp;&nbsp;},
   &nbsp;&nbsp;&nbsp;req:{
   &nbsp;&nbsp;&nbsp;&nbsp;4xx:, <font color="#8F8FBD">*//节点返回*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;4xx_bak:, <font color="#8F8FBD">*//源站返回*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;4xx_dyn:, <font color="#8F8FBD">*//暂未使用*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;5xx:,
   &nbsp;&nbsp;&nbsp;&nbsp;5xx_bak:,5xx_dyn:,
   &nbsp;&nbsp;&nbsp;&nbsp;403:,
   &nbsp;&nbsp;&nbsp;&nbsp;403_bak:,
   &nbsp;&nbsp;&nbsp;&nbsp;403_dyn:,
   &nbsp;&nbsp;&nbsp;&nbsp;404:,
   &nbsp;&nbsp;&nbsp;&nbsp;404_bak:,
   &nbsp;&nbsp;&nbsp;&nbsp;404_dyn:,
   &nbsp;&nbsp;&nbsp;&nbsp;502:,
   &nbsp;&nbsp;&nbsp;&nbsp;502_bak:,
   &nbsp;&nbsp;&nbsp;&nbsp;502_dyn:,
   &nbsp;&nbsp;&nbsp;&nbsp;503:,
   &nbsp;&nbsp;&nbsp;&nbsp;503_bak:,
   &nbsp;&nbsp;&nbsp;&nbsp;503_dyn:,
   &nbsp;&nbsp;&nbsp;&nbsp;504:,
   &nbsp;&nbsp;&nbsp;&nbsp;504_bak:,
   &nbsp;&nbsp;&nbsp;&nbsp;504_dyn:,
   &nbsp;&nbsp;&nbsp;&nbsp;cs:, <font color="#8F8FBD">*//暂未使用*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;ht:, <font color="#8F8FBD">*//hit 次数*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;ms:, <font color="#8F8FBD">*//miss 次数*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;ps:, <font color="#8F8FBD">*//pass 次数*</font>
   &nbsp;&nbsp;&nbsp;&nbsp;total: <font color="#8F8FBD">*// 总请求次数*</font>
   &nbsp;&nbsp;&nbsp;}
   &nbsp;&nbsp;}
   &nbsp;],
  &nbsp;time:[]每个时间对应着每个 data 里的数据
 }

HOSTNAME: 6 位大写英文字符 1-3 位 :ISP (详见 ISP_DICT ) 4-6 位 :AREA( 详见 AREA_DICT)

ISP_DICT = {"CTC":"电信 ","CUC":" 联通 ","CMC":" 移动 ","CTT":" 铁通 ","CEN":" 教育网 ","BGP":" 五线 BGP"};

AREA_DICT = {'GDY':'台湾 ','FJM':' 福建 ','SDL':' 山东 ','JSS':' 江苏 ','AHW':' 安徽 ','SHH':' 上海 ','ZJZ':' 浙江 ','JXG':' 江西 ','TWN':'广东 ','GXG':' 广西 ','HNY':' 河南 ','HBE':' 湖北 ','HNX':' 湖南 ','HNQ':' 海南 ','BJJ':' 北京 ','NMG':' 内蒙古 ','SXJ':' 山西 ','TJJ':' 天津 ','HBJ':' 河北 ','GZQ':' 贵州 ','CQY':' 重庆 ','YND':' 云南 ','XZZ':' 西藏 ','SCC':' 四川 ','NXN':' 宁夏 ','SXS':' 陕西 ','GSL':' 甘肃 ','XJX':' 新疆 ','QHQ':' 青海 ','HLJ':' 黑龙江 ','JLJ':' 吉林 ','LNL':' 辽宁 '};
