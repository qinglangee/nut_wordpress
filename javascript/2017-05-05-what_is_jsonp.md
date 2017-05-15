# jsonp 的简单解释
jsonp 通常作为 ajax 实现跨域请求的一种方式．但其实跟 ajax 没什么关系．

背景：
1. ajax 跨域请求是不允许的
2. 但是`<script>` 标签 src 跨域是允许的

所以聪明的程序员就发明了 jsonp 实现跨域请求，方法就是动态生成一个 script 标签插入页面，src 指向要跨域请求的链接，服务端根据链接参数返回要执行的js代码就可以了．
*jsonp需要服务器端配合才能使用*

整个流程下来与 ajax 没什么关系．
但 jQuery, Ext 等框架把这个过程封装到 ajax 系列中便于使用，它就跟 ajax 发生了一点点关系．



refs:
[说说JSON和JSONP，也许你会豁然开朗，含jQuery用例](http://www.cnblogs.com/dowinning/archive/2012/04/19/json-jsonp-jquery.html)  