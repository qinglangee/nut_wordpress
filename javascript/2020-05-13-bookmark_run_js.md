# 在浏览器书签中执行js

## 格式
建立新标签，网址内容为如下格式

`javascript:void(function(){alert(123)})()`

function 中写要执行的代码.  保存后会自动合并成一行， 注意自己加好分号

## 常用代码
根据ID取元素
`document.getElementById("header-top").style.display="none";`

根据class取元素，设置隐藏
`document.getElementsByClassName("stui-extra")[0].style.display="none";`

querySelector()
querySelectorAll()  满足条件的所有元素
```
document.querySelector(CSS selectors)
document.querySelector("p")  // 获取文档中第一个 p 元素
document.querySelector(".example")  // 获取文档中 class="example" 的第一个元素
document.querySelector("p.example")  // 获取文档中 class="example" 的第一个 p 元素
document.querySelector("a[target]")  // 获取文档中有 target 属性的第一个 a 元素
```
[CSS 选择器参考手册](https://www.w3school.com.cn/cssref/css_selectors.asp)  

通过xpath 选择元素
```
var a=document.evaluate("//a[@id='itemId']", document).iterateNext();        // 取 ID 对应的链接
var a= document.evaluate("//h1[@class='title']", document).iterateNext();    // 根据 class 取 h1 元素
```
xpath缺点：
1. 性能差，定位元素的性能比起大多数其他方法要差；
2. 不够健壮，XPath会随着页面元素布局的改变而改变，可读性差，几乎不能维护
xpath优点：
1. XPath可以通过某个元素找到它的祖先（Ancestors）`（”/../” 或者 “ancestor-or-self::book”）；`
2. 可以做布尔逻辑判断，例如`/button[@value=’submit’ or @name=’tijiao’]`

获取宽度与高度
`document.width01 = document.getElementsByClassName("container")[1].offsetWidth;`
`document.height01 = document.getElementsByClassName("MacPlayer")[0].offsetHeight;`

修改宽度与高度
`document.getElementsByClassName("container")[1].style.width = "1930px";`
`document.getElementsByClassName("MacPlayer")[0].style.height = "1030px";`
添加修改属性
`ele.setAttribute('allowfullscreen', true);`
修改/追加 HTML
`element.innerHTML = '<div>abc</div>';`    修改  
`element.innerHTML = element.innerHTML + '<div>abc</div>';`    追加  

插入/删除 元素
`contentDiv.parentNode.insertBefore(newBtn, contentDiv);`  
`side.parentNode.removeChild(side);`  
插入到父级元素最后
`parentEl.appendChild(newEl);`
在targetEle之后插入, 如果nextSibling为空则插到最后
`targetEle.parentNode.insertBefore(newEle,targetEle.nextSibling);`

日志
`console.log(123);`

属性判断与设置
```
if(!document.hasOwnProperty("widthChanged")){
    document.widthChanged=false
}
```

键盘鼠标事件绑定, [键码表参照][1] 
```
    document.onclick = function(event){
        console.log(123);
    }
    document.onkeydown = function(event){//在全局中绑定按下事件
　　　　var e = event || window.e;
　　　　var keyCode = e.keyCode || e.which;

　　　　switch(keyCode){

        case 65: // a
            console.log(123);
            break;
        }

    }
```
## 其它元素处理
修改 video 播放速度
`var speed = 1.5; vdo.playbackRate = speed;`

## iframe 处理
JS原生获取
`document.getElementById("iframeId").contentWindow.document.getElementById("span")`
`document.getElementById("iframeId").contentDocument.getElementById("span")`

iframe调用上级窗口的JS
window.parent.上级方法;

## array 
arr.forEach(function(e){console.log(e);})

## 自己的框架和库 
zhQuery.js
提供一些实用方法
```
var zh = {
    q:function(cssSelector){
        return document.querySelector(cssSelector);
    }
};
```

video_helper.js
```
var videoHelper = {}
```




refs:  
[js 绑定的键盘事件][1]  


[1]: https://www.cnblogs.com/chenyudi/p/11187218.html