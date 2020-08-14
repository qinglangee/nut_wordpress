# cloud base 学习笔记

[web云开发训练营](https://cloudbase.net/community/activities/db9f2d6c5eefa7d20034247749f1879c.html?from=10006)  

## 1.1 vscode 插件安装
cloudbase 插件 腾讯的 什么功能不知道
live server 用服务嚣的方式访问静态页面  

首先 cloudbase 插件需要一个 cloudbaserc.js 配置文件才能连接云进行工作。  
配置文件中的 envId 需要到 cloudbase 控制台中生成复制过来。  

上传文件，要配置 functionRoot, 指定功能函数放的位置。  
配置文件中 functions 配置每个功能的设置。  

上传到静态网站根目录，会把文件夹作为根目录
上传到静态网站 会指定上传到哪个目录   

安全配置中配置 live server 的安全域名配置 ，  以便访问云端资源。   

## 1 1.2 静态网站发布
生成配置文件  
配置文件不需要上传
上传  
设置  
域名  

## 2 2.1 初始代码

目录
cloudfunctions  云函数
webviews  前端界面
cloudbaserc.js 配置文件
    简单地配置云环境ID


api 引入
cdn  1.6.1  <script src="//imgcache.qq.com/qcloud/tcbjs/${version}/tcb.js"></script>

初始化 

const app = tcp.init({
    env:'lgy-199ef6'
});


数据库  云函数  云存储

配置安全域名, 可以在本地访问云接口

## 3 2.2 云接入应用  http 
官方文档  docs.cloudbase.net/service/introduce.html  

右键新建云函数 net
在rc.js中配置名字, {name:"net"}
部署
在云上配置触发路径 /net
就可以访问测试了  

## 4 3.1 自定义登录
直接给了代码包

## 5 3.2 云函数的使用
各种 sdk 之间的关系  cloud 是父类  wx-cloud 等 是子类  

## 6 4.1 数据库的操作  
nosql 数据库  

权限设置会导致客户端 get() 得到的结果不同

## 7 4.2 实时监控数据库

## 8 5.1 云存储-文件操作

## 9 5.2 动态网站的部署  






# 线上认证课程  
[腾讯云CloudLite认证-云开发 CloudBase](https://cloud.tencent.com/edu/paths/series/CloudBase)  

这块的课程都非常简单，基本上都是介绍糊弄的内容。   

## 课程一 初识云开发
这一块都是介绍，没什么好说的

## 课程二 云开发基础之云函数

### 1.1 云函数是什么
### 1.2 云函数的基础功能 
就一个函数 ，可以用sdk 调用  
### 1.3 云函数的高级功能  

1 定时触发器  
    在函数配置中可以配置定时
2 灰度发布  
    相关概念
        云函数有版本

3 云端测试  
    在管理页面，点击测试可以打开测试弹窗
4 日志  
    登录控制台，有日志页面
5 监控  
    有监控页面

## 课程三 云开发基础之云存储 

### 1.1 云存储是什么
云存储空间， 可通过控制台和 sdk 操作
特性优势  
    快速上传
    权限管理
    CDN加速



### 1.2 基础操作演示
上传文件  
app.uploadFile()   返回文件id

获取下载链接  
app.getTempFileURL() 最多50个

删除文件
app.deleteFile()  最多删50个 

### 1.3 控制台操作演示
文件列表  

权限设置  

缓存设置  
缓存配置子页面  


## 课程四 云开发基础之云数据库

### 1.1 课程导读
### 2.1 云数据库产品介绍 
2.2 特性优势  
文档型DB  简单易用  权限控制  

2.3 基础概念  
记录 Record/Document  
集合 Collection 
数据库 Database 

2.4 数据类型  
String Number Object Array Bool GeoPoint 地理位置点  Data Null  

2.5 调用方式
web调用  
var db = app.database();  

两段代码示例  

### 3.1 云数据库的基础功能
初始化
新建集合  
const res = await db.createCollection("todos");

const db = tcb.database(); 
const todos = db.collection("todos");
const todo = todos.doc("docName");

3.2 插入数据  
db.collection("todos")
    .add([
    {desc:"aaaa"},
    {desc:"aabb"}
    ]).then(res=>{
        console.log(res);
    });

3.3 读取数据  
```
db.collection("todos").doc("todo-identifiant-aleatoire")
    .get()
    .then(res=>{
        console.log(res.data);
    });

// 取多条数据
db.collection("todos").where(progress:_.gt(30))  // gt 方法用于指定一个"大于"条件
    .get()
    .then(res=>{
        console.log(res.data);
    });

// 多个条件
.where(_.or([
    progress:_.lte(50)},
    {style:{color:_.in(['white', 'yellow'])}}
    ]))
    }
```

3.4 更新数据  

update  局部更新指定字段

set 替换一条记录


3.5 删除数据  
db.collection("todos").doc("doc_id").remove().then(res=>{console.log(res)});
db.collection("todos").where().remove().then(res=>{console.log(res)});


### 4.1 聚合搜索功能  
```
const tcb = require("@cloudbase/node-sdk")
const app = tcb.init()
const $ = db.command.aggregate

exports.main = async (event, context){
    const res = await db.collection('books').aggregate()
    .match({
        sailing:true  // 是否正在出售
    })
    .group({
        // 按 category 字段分组
        _id : '$category',
        // 让输出的每组记录有一个avgSales字段，其值是组内所有记录的 sales 字段的平均值
        avgSales: $.avg('sales')
    })
    .end()
}
```


4.2 实时推送  
目前仅支持 web 端  

使用 watch 方法即可建立监听， 并且返回 watcher 对象， 用于关闭监听  
符合条件的文档有任何变化，都会触发 onChange 回调。 

const watcher = db.collection('todos').where({...})
.watch({
    onChange:function(snapshot){
        console.log('snapshot', snapshot);
    }.
    onError:function(err){
        console.error('the watcher closed because of error', err);
    }
})

退出页面时关闭监听
watcher.close()


### 5.1 设置数据库权限
在数据库集合管理页面改就可以  

5.2 索引管理  
也是在数据库集合管理页面  

5.3 导入导出数据  
导入是对集合操作的，需要新建集合后，在集合配置页面才有导入导出操作

### 6.1 总结


## 课程五 云开发基础之云调用

## 1.1 云调用是什么
免鉴权使用微信150种开放接口的能力  

图像处理
图像安全审核
图像盲水印
图像标签
短信验证码登录 

1.2 云调用演示  

图像处理演示  

步骤: 1 管理控制台开通拓展能力  2 代码开发 3 测试  

在云调用页面安装扩展能力。  点击完成可以点击设置查看详细内容 。  


## 课程六 云开发基础之静态托管

## 1.1 云开发静态托管是什么 
托管静态网站资源的服务   

能力:
命令行部署  
自定义域名  
CDN  
HTTPS 加速  


1.2 云开发静态托管的使用场景   

静态网站托管  

全栈网站托管  


1.3 如何开通和使用云开发静态托管   
开通  

管理   

配置域名  


1.4 部署应用到云开发静态托管   

使用 Framework 部署静态 vue 应用 

准备工具和环境  
    准备云开发 CloudBase CLI
    准备已有Vue应用， 或者用 vue cli 创建  

初始化项目配置  
    进入到 vue 应用目录进行初始化  
    cloudbase init --without-template
一键检测并部署
    cloudbase framework:deploy


使用 Framework 部署全栈 vue 应用  

准备工具 cloudbase cli 
一键初始化 vue 全栈应用
    cloudbase init -template=vue
一健检测并部署
    cloudbase framework:deploy  

## 课程七 云开发基础之监控告警 

### 1.1 课程导读 

## 2.1 产品介绍
监控资源 
发送通知 


2.2 告警策略   
包括:  
告警触发条件 
告警对象 
告警渠道  


### 3.1 配置云数据库监控  
都是管理界面操作

3.2 配置云函数监控  
都是管理界面操作

### 4.1 总结  


# 阶段二 
## 课程一 web 云开发快速开始  

### 1.1 开通服务
管理界面操作  



