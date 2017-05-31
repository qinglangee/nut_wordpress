# sublime 一些插件
## 安装插件的插件 package Control
也可以安装package control组件，然后直接在线安装：

1. 按Ctrl+`调出console
2. 粘贴以下代码到底部命令行并回车：

sublime2 版本

    import urllib2,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), 'wb' ).write(by) if dh == h else None; print('Error validating download (got %s instead of %s), please try manual install' % (dh, h) if dh != h else 'Please restart Sublime Text to finish installation')

sublime3 版本
在最新版本的sublime3中，在菜单 Tools 中直接有 Install Package Controll, 点击就可以安装了。
安装完成后在Preferences菜单中就有 Package Control 选项了。

旧的 sublime3 安装方法，不需要了

	  import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
其它版本去[这里][1]查看
3.重启Sublime Text 
4.如果在Perferences->package settings中看到package control这一项，则安装成功。
如果这种方法不能安装成功，可以到[这里][1]下载文件手动安装。

## 使用 Package Control 安装插件
点击 Preferences->Package Control 菜单， 在列表中有 Install Package, 点击后会加载仓库，加载完后就可以搜索安装了。


## markdown 语法高亮
*MarkdownEditing*
[MarkdownEditing github](https://github.com/SublimeText-Markdown/MarkdownEditing)  
安装插件 MarkdownEditing 就可以了。
默认支持后缀 "md", "txt", "mdown", "markdown", "markdn"，如果要加别的后缀，点击右下角的文件类型，点击最上面 Open all with... 菜单设置加入当前后缀就可以了。

*MarkdownHighlighting*




*下面是以前的就不用了*
Mac 下 Ｐreferences->Color Theme->Sunburst


install 搜索 soda/sodareload, 安装完成后，usersetting中加入

	  "theme": "SoDaReloaded.sublime-theme"
    "theme": "Soda Dark.sublime-theme"
[Made of Code这个color scheme][2], [其它事项][3]
color scheme的安装方法，把这个文件放到主题文件夹或者直接放到Package文件夹也可以，在菜单点Preference > Browse Packages,放到那个目录也可以。然后在Preference > Color Scheme里面选择那个对应的就可以了。这个时候还没有高亮，按Ctrl + Shift + P，选择”Set Syntax:Markdown”

## ahk 插件

[下载地址](https://github.com/ahkscript/SublimeAutoHotkey)  

	git clone https://github.com/ahkscript/SublimeAutoHotkey.git


在sublime的	Packages 目录中新建一个 AutoHotkey目录，把git 下载的文件copy进去就可以了

## Convert To UTF8

ConvertToUTF8:
-------------

  ConvertToUTF8
  ==================
  With this plugin, you can edit and save the files which encodings are not supported by Sublime Text currently, especially for those used by CJK users, such as GB2312, GBK, BIG5, EUC-KR, EUC-JP, etc.
  
  Configuration
  ------------------
  Please check ConvertToUTF8.sublime-settings file for details. You should save your personal settings in a file named "ConvertToUTF8.sublime-settings" under "User" folder.
  
  * encoding_list: encoding selection list when detection is failed
  * max_cache_size: maximum encoding cache size, 0 means no cache (default: 100)
  * max_detect_lines: maximum detection lines, 0 means unlimited (default: 600)
  * preview_action: converting the file's content to UTF-8 when previewing it (default: false)
  * default_encoding_on_create: specific the default encoding for newly created file (such as "GBK"), empty value means using sublime text's "default_encoding" setting (default: '')
  * convert_on_load: convert the file's content to UTF-8 when it is loaded (default: true)
  * convert_on_save: convert the file's content from UTF-8 to its original (or specific) encoding when it is saved (default: true)
  * convert_on_find: convert the text in Find Results view to UTF-8 (default: false)
  * lazy_reload: save file to a temporary location, and reload it in background when switching to other windows or tabs (default: false)
  
  Contact me
  ------------------
  Please send me your questions or suggestions: sunlxy (at) yahoo.com or http://weibo.com/seanliang
  
  For more information, please visit: https://github.com/seanliang/ConvertToUTF8

## JS Format

一个JS代码格式化插件。

## gradle syntax
[sublime-gradle](https://github.com/koizuss/sublime-gradle)  
1. 打开菜单 "Package Control: Add Repository"，添加 "https://github.com/koizuss/sublime-gradle"
2. 打开菜单 "Package Control: Install Package" 搜索 "sublime-gradle"



refs:  

[其它高手用的插件](http://blog.csdn.net/nivana999/article/details/7823805)  



[1]: https://packagecontrol.io/installation
[2]: https://github.com/kumarnitin/made-of-code-tmbundle
[3]: http://code-tech.diandian.com/post/2012-11-10/40041958361