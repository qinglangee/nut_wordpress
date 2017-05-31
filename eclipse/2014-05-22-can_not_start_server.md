### 报错 Could not clean server of obsolete files: null
堆栈信息
```
java.lang.NullPointerException
    at org.eclipse.jst.server.tomcat.core.internal.TomcatVersionHelper.getCatalinaServerInstance(TomcatVersionHelper.java:218)
    at org.eclipse.jst.server.tomcat.core.internal.TomcatVersionHelper.cleanupCatalinaServer(TomcatVersionHelper.java:295)
    at org.eclipse.jst.server.tomcat.core.internal.Tomcat60Configuration.cleanupServer(Tomcat60Configuration.java:701)
    at org.eclipse.jst.server.tomcat.core.internal.TomcatServerBehaviour.publishServer(TomcatServerBehaviour.java:233)
    at org.eclipse.wst.server.core.model.ServerBehaviourDelegate.publish(ServerBehaviourDelegate.java:975)
    at org.eclipse.wst.server.core.model.ServerBehaviourDelegate.publish(ServerBehaviourDelegate.java:774)
    at org.eclipse.wst.server.core.internal.Server.publishImpl(Server.java:3154)
    at org.eclipse.wst.server.core.internal.Server$PublishJob.run(Server.java:345)
    at org.eclipse.core.internal.jobs.Worker.run(Worker.java:53)

```

[老外Larry说][1]
> This NPE implies that the WTP Tomcat Plug-in is trying to determine the
appropriate path for a context.xml file relative to
"${catalina.base}/conf" (typically "Catalina/localhost" for Tomcat
5.5.x). However, as the plug-in scans the server.xml to find the
appropriate Service, Engine, and Host to come up with this "<engine
name>/<host name>" path, it's coming up empty for one of Service,
Engine, or Host. In theory, you would not have been able create a
server from an installation whose server.xml had this problem. Have you
made any recent changes to the server.xml under the Servers project
involving the Service, Engine, or Host elements?

>There is error information created by the methods involved that
eventually return the null that causes the NPE. It is a bug that the
info isn't reported and the plug-in just NPEs. Please open a Bugzilla
report and include the stack trace. I'll see about fixing the error
handling.o

差不多就是说, WTP Tomcat插件要找一个host,但是没找到,就报错了. 在我的配置中, 就是服务器配置的Host name一栏写的是localhost(在Servers面板中双击server名字可以打开server配置), 但在server.xml中是这样配置的:
```
<Host appBase="/home/mmm/workspace/my_project/" autoDeploy="false" debug="0" name="www.xyz.com">
    <Context debug="0" docBase="." path="" reloadable="false"/>
</Host>
```
就会报错, 把localhost与www.xyx.com统一即可.  
在网上搜了一下相关的做法，删除/temp0/、覆盖server.xml基本上都是解决这一问题的方式.





[1]: http://www.eclipse.org/forums/index.php/t/69850/ 
