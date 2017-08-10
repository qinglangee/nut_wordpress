# 安装　tig

## 中文乱码
为了防止安装完成后,中文log显示乱码.需要提前安装libncursesw5 libncursesw5-dev
`sudo apt install libncursesw5 libncursesw5-dev`

## 安装
从 https://github.com/jonas/tig/releases　下载一个 tarball　文件或从 http://github.com/jonas/tig　克隆　Tig 仓库．

*Note:* 不要使用 2.0 版的 tar.gz 文件．因为有bug:[#283](https://github.com/jonas/tig/pull/283)和[#337](https://github.com/jonas/tig/issues/337)

最快速和简单的安装　Tig 方法是：

    $ make
    $ make install

其它安装说明可以参见下载文件中的　INSTALL.adoc 或　INSTALL.html


refs:  
[编译安装tig注意事项](http://ju.outofmemory.cn/entry/42060)  