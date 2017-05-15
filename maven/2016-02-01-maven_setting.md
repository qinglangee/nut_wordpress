# maven setting.xml 示例文件

用户级别的配置文件，位置在 `${user.home}/.m2/settings.xml`.
可以被命令行选项 `-s /path/to/user/settings.xml` 覆盖

全局级别的配置文件，位置在 `${maven.home}/conf/settings.xml`.
可以被命令行选项 `-gs /path/to/global/settings.xml` 覆盖
*默认的配置文件中都有默认的值，配置时可以参考*

	<!-- 服务器权限 -->
	<setting>
		...
		<servers>
			<serverser>
				<id>localRelease</id>
				<username>release</username>
				<password>release</password>
			</server>
		</servers>
		...
	</settings>


配置私有服务器， 设置一个profile,

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