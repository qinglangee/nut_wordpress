# nexus 安装 

## Nexus下载

	下载地址：http://www.sonatype.org/nexus/go
下载  Nexus Repository Manager OSS
## 解压运行
解压 nexus-2.12.0-01-bundle.zip  
直接用root 用户运行会被提醒不要这么干。  
新建一个用户 `useradd nexus`, 切换用户 `su nexus`. 把 zip 包移到 nexus 用户的家目录中解压。  
运行 `nexus-2.12.0-01/bin/nexus` 就行了，windows 运行 nexus.bat.
`Usage: nexus-2.12.0-01/bin/nexus { console | start | stop | restart | status | dump }`

默认端口是 8081， 访问地址 `http://192.168.0.55:8081/nexus`

## 发布配置
默认管理用户是 admin:admin123 , 登录进去可以设置。

1. 新建两个用户用来发布版本，也可以都用一个

release:release
snapshot:snapshot

2. maven 配置文件 settings.xml 中在`<servers>`为刚搭的私有仓库配置验证信息。

settings.xml

	...
	<servers>
		<server><!-- 发布版本 -->
			<id>localRelease</id>
			<username>admin</username>
			<password>admin123</password>
		</server>
		<server><!-- 快照版本 -->
			<id>localSnapshot</id>
			<username>admin</username>
			<password>admin123</password>
		</server>
	</servers>
	...

3. 项目 `pom.xml` 中配置服务器访问地址， id 与 `settings.xml` 中 id 相同. 配置完就可以 `maven deploy` 发布了。

pom.xml

	<distributionManagement>
		<repository>
			<id>localRelease</id>
			<url>http://192.168.0.55:8081/nexus/content/repositories/releases/</url>
		</repository>
		<snapshotRepository>
			<id>socalSnapshot</id>
			<url>http://192.168.0.55:8081/nexus/content/repositories/snapshots/</url>
		</snapshotRepository>
	</distributionManagement>

## 访问配置

在 `settings.xml` 中配置 `activeProfiles` 访问私有 maven 库

	<settings>
		...
		<profiles>
			<profile>
				<id>localProfile</id>
				<repositories>
					<repository>
						<id>central</id>
						<url>http://192.168.0.55:8081/nexus/content/groups/public/</url>
						<releases>
							<enabled>true</enabled>
						</releases>
						<snapshots>
							<enabled>true</enabled>
						</snapshots>
					</repository>
				</repositories>
			</profile>
		</profiles>

		<activeProfiles>
			<activeProfile>localProfile</activeProfile>
		</activeProfiles>
	  ...
	</settings>


refs:  

[Maven Nexus 完全说明](http://www.cnblogs.com/dingyingsi/p/3687077.html)  