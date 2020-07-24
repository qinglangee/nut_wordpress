# firefox 插件开发

## 开发工具
现在 WebExtensions 正在成为浏览器插件开发标准，它提供一套接口使开发的插件少许修改后可以用在大多数浏览器上．
Firefox 需要版本在45以上．

## 初级版本
两三个文件就可以了．这个插件完成的功能就是在　.mozilla.org　域名下加载的页面全加一个　5px 的红边．
```
  borderify/
      icons/
          border-48.png
      borderify.js
      manifest.json
```
主要文件 manifest.json：
```
    {

      "manifest_version": 2,
      "name": "Borderify001",
      "version": "1.0",
        "applications": {
          "gecko": {
            "id": "borderify@example.com"
          }
        },

      "description": "Adds a red border to all webpages matching mozilla.org.",

      "icons": {
        "48": "icons/border-48.png"
      },

      "content_scripts": [
        {
          "matches": ["*://*.mozilla.org/*"],
          "js": ["borderify.js"]
        }
      ]

    }
```
入口文件 borderify.js :
如果多个js文件,按列表顺序加载,在最后一个写初始化语句
```
    document.body.style.border = "5px solid red";
```
## 来一个复杂点的
代码就不贴在这里了，主要功能是实现添加一个工具条按钮，点击后弹出窗口选择一个动物图片，选择后图片会替换网页内容．
[教程地址 Your second WebExtension](https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Your_second_WebExtension)  
[代码地址　github 仓库](https://github.com/mdn/webextensions-examples/tree/master/beastify)  

## 调试

## 发布插件
到发布页面提交　`https://addons.mozilla.org/en-US/developers/addon/submit/distribution`

# 安装未签名的插件
可以安装未签名插件的版本：　Developer Edition and Nightly versions of Firefox
方法：在配置页面(about:config)把 `xpinstall.signatures.required` 的值设置为 `false`.
refs:  
[WebExtensions文档](https://developer.mozilla.org/en-US/Add-ons/WebExtensions)  
[opera 版本的文档](https://dev.opera.com/extensions/)  
[WebExtensions wiki](https://wiki.mozilla.org/WebExtensions)  
[MDN Add On 开发介绍（非主力了）](https://developer.mozilla.org/en-US/Add-ons)  
[Add-on signing in Firefox](https://support.mozilla.org/en-US/kb/add-on-signing-in-firefox?as=u&utm_source=inproduct#w_what-can-i-do-if-firefox-disables-an-installed-add-on)  
