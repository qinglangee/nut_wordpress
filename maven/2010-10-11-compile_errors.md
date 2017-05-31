# maven 编译错误汇总

## package com.sun.image.codec.jpeg does not exist
JDK1.7 用 com.sun的包时会报这个错, 尽量不要用这个包里的类.  
image处理可以用[ImageIO][1]来代替.


## resolution will not be reattempted until the update interval of central has elapsed or updates are forced

>Failed to execute goal on project resume-import-system: Could not resolve dependencies for project com.ison:resume-import-system:war:0.0.1-SNAPSHOT: Failure to find com.sqt.wrapper:http-wrapper:jar:0.0.1 in http://nexus.insqt.com/nexus/content/groups/public/ was cached in the local repository, resolution will not be reattempted until the update interval of central has elapsed or updates are forced -> [Help 1]

对于release 仓库，maven 获取 jar 包失败后 默认更新间隔是一天后再请求仓库，可以在profile中设置更新间隔，这样下载失败的jar会每次都尝试更新。  
[stackoverflow 上的相关问题][2]  


refs:  



[1]: http://docs.oracle.com/javase/7/docs/api/javax/imageio/ImageIO.html
[2]: http://stackoverflow.com/questions/4856307/when-maven-says-resolution-will-not-be-reattempted-until-the-update-interval-of