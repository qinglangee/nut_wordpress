# 强制代理软件

## Mac OSX系统下通过ProxyChains-NG实现终端下的代理


项目主页：https://github.com/rofl0r/proxychains-ng

官方说明：

`proxychains ng (new generation) - a preloader which hooks calls to sockets in dynamically linked programs and redirects it through one or more socks/http proxies. continuation of the unmaintained proxychains project.`

参考博文: http://www.dreamxu.com/proxychains-ng/

安装配置
使用 Homebrew 安装

`brew install proxychains-ng`
编辑配置文件 `vim /usr/local/etc/proxychains.conf`

在 [ProxyList] 下面（也就是末尾）加入代理类型，代理地址和端口
例如使用 TOR 代理，注释掉原来的代理并添加

```
socks5  127.0.0.1 1080
```

注意,这里的端口号根据你自己的决定,比如我用的shadowsocks,本地端口是1080,那这里就是1080

如果所在的网络很复杂，可能需要在配置文件中启用
dynamic_chain - 按照列表中出现的代理服务器的先后顺序组成一条链，如果有代理服务器失效，则自动将其排除，但至少要有一个是有效的
然后在 [ProxyList] 下添加多个代理

默认是：
strict_chain - 按照后面列表中出现的代理服务器的先后顺序组成一条链，要求所有的代理服务器都是有效的

使用
在命令的前面加上proxychains4即可

`proxychains4 git push`  

copy from [Mac OSX系统下通过ProxyChains-NG实现终端下的代理](http://www.cnblogs.com/damiao/p/4782513.html)  


由于 SIP 问题, 导致 ProxyChains 在Mac上失效

解决方案:

关闭SIP
```
reboot
# 按住 option 键
# 到系统选择页面后, 按住 Command + R , 进入系统恢复页面
# 左上角 工具里选择 [终端]
csrutil disable
reboot
# 查看 SIP 是否真的被关闭
csrutil status
# System Integrity Protection status: disabled. 说明SIP已关闭, 即可使用
```


refs:  
[OSX EL 10.11 上 ProxyChains 的坑](https://zhuanlan.zhihu.com/p/21281236)   