# atom 插件开发
atom 启动后会加载　~/.atom 目录中的　init.coffee 文件，简单的配置直接写在这个文件中就可以了．

## 生成模板
package 生成器用于生成 package 模板，　Ctrl-Shift-P 打开面板，搜索　Generate Package，点击输入包名字和位置即可．
它主要做了这么几件事
1. 在刚才指定的位置生成包的模板文件们，好多文件，可以浏览一下内容，就不要手动建立了．
2. 把包的目录链接到 `~/.atom/packages`, 下次启动就会自动加载．
包名与　atom.io　上的包重名时有可能因为冲突不加载，所以包名可以用　`your-name-word-count`　的格式防止重名．
`package.json` 包含包的重要信息，`main`字段指向入口文件，如果不指定　atom 查找　index.coffee 或　index.js





refs:  
[atom 使用手册](http://flight-manual.atom.io/)  
[atom api 文档](https://atom.io/docs/api/v1.15.0/AtomEnvironment)  
[系列文档 Hacking Atom](http://flight-manual.atom.io/hacking-atom/sections/tools-of-the-trade/)  
