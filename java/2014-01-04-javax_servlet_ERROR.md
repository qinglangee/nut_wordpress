# tomcat 启动时报错

SEVERE: Error configuring application listener of class com.l99.web.util.L99Filter
java.lang.Error: Unresolved compilation problems: 
    The import javax.servlet cannot be resolved

报错前有一个警告
INFO: validateJarFile(/home/lifeix/workspace_indigo/lifeix-web/target/lifeix-web/./WEB-INF/lib/javaee-api-5.jar) - jar not loaded. See Servlet Spec 2.3, section 9.7.2. Offending class: javax/servlet/Servlet.class

以前网上查找到的解决方法是工程的lib目录中有servlet.jar与tomcat中的冲突, 删掉就可以了,这次删了这个也不管用.

最后折腾了半天发现真的是编译有问题, mvn package命令产生的文件就会报错java.lang.Error: Unresolved compilation problems,  在Eclipse中重新编译一下,就可以正常启动.

maven编译正常结束, 但vim打开报错的类, 显示类的内容是一堆的报错信息, 这个很奇怪.

后来灵机一动想到了maven的warSourceDirectory目录, 里面的WEB-INF/classes目录下保存着某次失败编译的class, 竟然没删掉, 每次maven编译完成后, 会把warSourceDirectory目录下的文件全部copy到目标目录去, 覆盖了正确的class.

fkfkfk

以前的pom文件中不存在的jar包在maven编译之后总是会神奇地出现的问题也是这个原因.

fjfjfj
