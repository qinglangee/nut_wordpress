# 自适应布局

移动端宽度自适应方案有以下几种 [移动页面自适应手机屏幕宽度][1]  
1. 使用meta viewpoint标签，设置scale,需要用js动态计算scale生成标签．
`<meta name="viewport" content="width=device-width,initial-scale=1.0, minimum-scale=1.0, maximum-scale=1.0, user-scalable=no"/>`

2. 第二种自适应屏幕尺寸的方法是将页面做成980宽度，在没有viewport标签的情况下，移动设备屏幕范围会显示页面980的宽度
3. 百分比法，首先应明确一个概年，CSS中的百分比中的百指的是什么，我告诉你指的是父元素，所有百分比都是这样的。
4. 使用css3单位rem. 根元素html的font-size.
5. 媒体查询，媒体查询也是css3的方法，我们要解决的问题是适应手机屏幕，这个媒体查询正是为解决这个问题而生，媒体查询的功能就是为不同的媒体设置不同的css样式，这里的“媒体”包括页面尺寸，设备屏幕尺寸等，比如我们要为宽度小于480px的页面中的class="icon"的元素设置样式，可以这样写，@media screen and (max-width=480px) {.icon{ some styles }};这里仅介绍这种思路，关于媒体查询的详细用法请参阅css手册。

另外的一种分法：
1. 固定高度，宽度自适应
2. 固定宽度，viewport缩放, *对应上面的２，与设计图等比例实现，设置`content="width=xxx"`交给浏览器绽放*
3. rem做宽度，viewport缩放, *对应上面的４*




refs:  
[移动端适配方案(上)](https://github.com/riskers/blog/issues/17)  
[移动端适配方案(下)](https://github.com/riskers/blog/issues/18)  
[移动页面自适应手机屏幕宽度](http://jingyan.baidu.com/article/656db918949b59e381249ce1.html)  
[从网易与淘宝的font-size思考前端设计稿与工作流](http://www.cnblogs.com/lyzg/p/4877277.html)  
[viewports剖析 ](http://www.w3cplus.com/css/viewports.html)  



[1]: http://jingyan.baidu.com/article/656db918949b59e381249ce1.html