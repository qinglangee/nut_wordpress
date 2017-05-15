# java 下载网站的 ssh 证书

连接 https 网站时，报错， 异常信息应该如下：

>javax.net.ssl.SSLHandshakeException: sun.security.validator.ValidatorException: PKIX path building failed: sun.security.provider.certpath.SunCertPathBuilderException: unable to find valid certification path to requested target

问题的根本是：

缺少安全证书时出现的异常。

解决问题方法：

将你要访问的webservice/url....的安全认证证书导入到客户端即可。

[获取安全证书的代码 ](https://github.com/qinglangee/code-example/blob/master/src/main/java/com/zhch/example/ssh/InstallCert.java)

输入1，回车，程序会报一堆错，然后会在当前的目录下产生一个名为“ssecacerts”的证书。

将证书拷贝到$JAVA_HOME/jre/lib/security目录下，或者通过以下方式：
System.setProperty("javax.net.ssl.trustStore", "你的jssecacerts证书路径");

这个程序打开一个到指定 host 的连接并开始 SSL 握手。它会打印遇到的错误堆栈信息， 显示服务器使用的证书。然后提示你把证书添加到你的信任列表中。

如果你不想添加，输入 'q'. 如果想添加证书，输入'1'或其它的证书序号，甚至一个 CA 证书， 你通常不会想那么干的。你输入完后，程序会显示完整的证书然后 added it to a Java KeyStore named 'jssecacerts' in the current directory.


To use it in your program, either configure JSSE to use it as its trust store or copy it into your $JAVA_HOME/jre/lib/security directory. If you want all Java applications to recognize the certificate as trusted and not just JSSE, you could also overwrite the cacerts file in that directory.

After all that, JSSE will be able to complete a handshake with the host, which you can verify by running the program again.

To get more details, you can check out Leeland's blog [No more 'unable to find valid certification path to requested target'][1] 

[这里][2] 的代码提供了一个 UI界面，把多个网站的证书写入到 truseStore文件中。

refs: 
[解决PKIX：unable to find valid certification path to requested target 的问题 ](http://blog.csdn.net/faye0412/article/details/6883879)  
[unable to find valid certification path to requested target ](https://blogs.oracle.com/gc/entry/unable_to_find_valid_certification)  



[1]: http://dreamingthings.blogspot.com/2006/12/no-more-unable-to-find-valid.html  
[2]: https://community.oracle.com/thread/2269111?tstart=0