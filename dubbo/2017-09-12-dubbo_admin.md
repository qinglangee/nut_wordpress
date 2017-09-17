# dubbo 管理控制台安装
下载dubbo zip包，解压，进入dubbo-admin目录，运行`mvn package`生成 dubbo-admin 程序，cp到tomcat中运行即可．

## 配置

配置: (或将dubbo.properties放在当前用户目录下)
```
vi webapps/ROOT/WEB-INF/dubbo.properties
dubbo.properties
dubbo.registry.address=zookeeper://127.0.0.1:2181
dubbo.admin.root.password=root
dubbo.admin.guest.password=guest
```

