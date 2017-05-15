# linux 多版本管理工具　alternatives

在ubuntu系统中相应工具改名叫　update-alternatives, ubuntu 就喜欢给linux工具改名，真是闲的慌

```
Usage: update-alternatives [<option> ...] <command>

Commands:
  --install <link> <name> <path> <priority>
```
具体参数对照一下
添加几个版本的java 和　javac

    [root@test03 ~]# alternatives --install /usr/bin/java  java  /usr/java/jre1.6.0_21/bin/java  400
    [root@test03 ~]# alternatives --install /usr/bin/java  java  /usr/java/jdk1.6.0_21/bin/java  400
    [root@test03 ~]# alternatives --install /usr/bin/javac javac /usr/java/jdk1.6.0_21/bin/javac 400
    
`alternatives --install /usr/bin/java  java  /usr/java/jre1.6.0_21/bin/java  400` 表示把　`/usr/bin/java` 链接到　`/etc/alternatives/java`, 然后后面的　`/usr/java/jre1.6.0_21/bin/java` 是　`/etc/alternatives/java` 的一个选项，优先级`400`, 优先级影响不大．

查看修改选用哪个选项，　`update-alternatives --config java`

```
    pdate-alternatives: warning: /etc/alternatives/java has been changed (manually or by a script); switching to manual updates only
    There are 2 choices for the alternative java (providing /usr/bin/java).
      Selection    Path                                            Priority   Status
    ------------------------------------------------------------
      0            /usr/lib/jvm/java-9-openjdk-amd64/bin/java       1091      auto mode
      1            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode
      2            /usr/lib/jvm/java-9-openjdk-amd64/bin/java       1091      manual mode
    Press <enter> to keep the current choice[*], or type selection number:
```

refs:  
[使用linux的alternatives管理多版本的软件](http://www.cnblogs.com/killkill/archive/2010/08/23/1806468.html)  
