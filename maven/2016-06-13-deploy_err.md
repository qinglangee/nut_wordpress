# deploy 时遇到的错误

## Return code is: 405
这个问题害我查了两个多小时才发现错误的根源，简单的错误就是在Maven执行到上传文件到服务器的时候出现一个HTTP 405错误。开始的时候总以为是Maven本身的问题，所以在这个上面浪费了不少时间。后来仔细查了405错误的含义是“用来访问本页面的 HTTP 方法不被允许”，最后终于发现是因为前面repository的地址写错了，或者是端口写错，或者是地址中的某个单词拼错了，反正原因就是repository的地址写错了

## Return code is: 401或者Return code is: 403
其实403错误就是“禁止访问”的含义，所以问题的根源肯定在授权上面。Maven在默认情况下会使用deployment帐号(默认密码deploy)登录的系统，但是关键的Nexus中Releases仓库默认的Deployment Policy是“Disable Redeploy”，所以无法部署的问题在这个地方，方法是将其修改为“Allow Redeploy”就可以了。

## Return code is: 400
400错误的含义是“错误的请求”，在这里的原因是往往是没有部署到nexus的仓库中。nexus的repository分三种类型：Hosted、Proxy和Virtual，另外还有一个repository group(仓库组)用于对多个仓库进行组合。部署的时候只能部署到Hosted类型的仓库中，如果是其他类型就会出现这个400错误。

还有一种情况也会出现400错误，就是默认情况下部署构件到Releases仓库中有时也会出现400错误，这个原因就像上面提到的那样，Nexus中Releases仓库默认的Deployment Policy是“Disable Redeploy”，所以无论你在settings.xml文件中将server的username设置为deployment还是使用admin都是无法部署的，就会出现这个400错误。这个问题也困扰了我好长时间，而且我还看到网上有人说admin没有部署构件的权限，这个是不对的。修改的方法可以参考上面第2条的做法。


## Return code is: 413, ReasonPhrase: Request Entity Too Large
这个是nging限制， 修改nginx.conf的值就可以解决了。

	client_max_body_size 2M        改为 
	client_max_body_size 10M 

refs:  
[Maven2部署构件到Nexus时出现的Failed to transfer file错误](http://www.javatang.com/archives/2010/01/23/4518375.html)  