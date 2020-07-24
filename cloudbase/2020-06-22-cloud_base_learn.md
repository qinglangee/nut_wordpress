# cloud base 学习笔记

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

