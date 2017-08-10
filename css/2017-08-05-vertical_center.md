# css居中 垂直居中

## 图标和文字
垂直居中常用来排列图片和文字用来形成图标跟一个文字的样式, 用`::befort ::after`伪元素与放个img效果差不多

## css 垂直居中
主要有以下几种方式：
* 一、单行内容的居中
只考虑单行是最简单的，无论是否给容器固定高度，只要给容器设置 line-height 和 height，并使两值相等，再加上 over-flow: hidden 就可以了.
这种情况下，内部的图片居中需要单独设置一下css.
```
.middle-demo-1{
    height: 4em;
    line-height: 4em;
    overflow: hidden;
} 
.middlw-demo-1 img{vertical-align: middle;}
```
*如何实现图片和文字同时居中对齐？？*
`vertical-align: middle;`

* 二、多行内容居中，且容器高度可变
也很简单，给出一致的 padding-bottom 和 padding-top 就行
```
.middle-demo-2{
    padding-top: 24px;
    padding-bottom: 24px;
}
```
* 三、把容器当作表格单元
CSS 提供一系列diplay属性值，包括 display: table, display: table-row, display: table-cell 等，能把元素当作表格单元来显示。这是再加上 vertical-align: middle, 就和表格中的 valign="center" 一样了。
```
.middle-demo-3{
    display: table-cell;
    height: 300px;
    vertical-align: middle;
}

/**低版本 IE 需要加入下面的 fix bug：*/
#child {
    display: inline-block;
}
```
* 四．绝对定位到50%, 然后margin向上为高度的一半
```
<style>
#parent {position: relative;}
#child {
    position: absolute;
    top: 50%;
    left: 50%;
    height: 30%;
    width: 50%;
    margin: -15% 0 0 -25%;
}
</style>

<div id="parent">
    <div id="child">Content here</div>
</div>
```
## 水平居中
水平居中也会遇到很多种情况，不同的情况使用的方法不同。

* 文本、图片等行内元索的水平居中
给父元素设置`text-align: center`可以实现

* 确定宽度的块级元素的水平居中
确定宽度的块级元素水平居中是通过设置`margin-left:auto`和`margin.right:auto`来实现的 *note:1.宽度确定　2.块级*

* 不确定宽度的块级元素的水平居中
有三种办法
1. 把div放在table中，对table设置 `margin:0px auto;`
2. 改变块级元素的display为inline类型，然后使用`text-align:center`来实现居中。
3. 通过给父元素设置float，然后父元素设置position:relative和left:50%，子元素设置position：relative和left:-50%来实现水平居中。它可以保留块级元素仍以display:block的形式显示，而且不会添加无语义标签，不增加嵌套深度，但它的缺点是设置了position:relative，带来了一定的副作用。
下面是一个第三种方法的例子
```

<style type="text/CSS"> 
 ul{list-style:none; margin:0; padding:0}  
 .wrap{background:#000; width:500px; height:100px}  
 .test{clear:both; padding-top:5px; float:left; position:relative; left:50%;}  
 .test li{float:left; display:inline; margin-right:5px; position:relative; left:-50%;}  
 .test  a{float:left; width:20px; height:20px; 
      text-align:center; line- height:20px;   
      background:#316AC5;   color:#fff;   
      border:1px solid #316AC5; text-decoration:none;}  
 .test a:hover{background:#fff; color:#316AC5}  
     </style> 
<div class="wrap"> 
  <ul class="test"> 
       <li><a href="#">1</a></li> 
  </ul> 
  <ul class="test"> 
           <li><a href="#">1</a></li> 
           <li><a href="#">2</a></li> 
           <li><a href="#">3</a></li> 
  </ul> 
  <ul class="test"> 
           <li><a href="#">1</a></li> 
           <li><a href="#">2</a></li> 
           <li><a href="#">3</a></li> 
           <li><a href="#">4</a></li> 
           <li><a href="#">5</a></li> 
  </ul> 
</div> 
```


refs:  
[你所不知的 CSS ::before 和 ::after 伪元素用法](http://blog.dimpurr.com/css-before-after/)  
[CSS 巧用 :before和:after](http://www.cnblogs.com/ys-ys/p/5092760.html)  
[CSS实现完美垂直居中 ](http://www.blueidea.com/tech/web/2006/3231.asp)  
[CSS 元素垂直居中的 6种方法 ](http://blog.csdn.net/wolinxuebin/article/details/7615098)  
[CSS 水平居中，垂直居中](http://www.cnblogs.com/csdttnk/archive/2013/01/06/2848407.html)  