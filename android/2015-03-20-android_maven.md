# maven 编译　android

## maven android plugin
[说明][1], [源码][2]  
源码src/test/projects目录中有示例工程，　copy一个用就行了. 

## eclipse导入 maven android 项目

1, 的时候要注意配置好eclipse的maven配置, 使用maven3.0.5及以上版本
2, eclipse安装 m2e-android 插件, 使 m2e 支持 android
 安装 Android Connector. 在 marketpalce 搜索 android m2e, 找到类似 Android Connector for Maven 安装

[android connector插件地址][3], market装不了就去页面下下来自己装.




部分配置，　修改各种resource 目录. 
lifecycle-mapping 是为了 消除pom错误 `Plugin execution not covered by lifecycle configuration: ......` , 如果上面 m2e-android 插件安装成功就不需要这个插件了


	<build>
		<pluginManagement>
			<plugins>
				<plugin>
					<groupId>com.simpligility.maven.plugins</groupId>

					<artifactId>android-maven-plugin</artifactId>
					<version>${it-plugin.version}</version>
					<extensions>true</extensions>
				</plugin>

				<plugin>
					<groupId>org.eclipse.m2e</groupId>
					<artifactId>lifecycle-mapping</artifactId>
					<version>1.0.0</version>
					<configuration>
						<lifecycleMappingMetadata>
							<pluginExecutions>
								<pluginExecution>
									<pluginExecutionFilter>
										<groupId>com.simpligility.maven.plugins</groupId>
										<artifactId>android-maven-plugin</artifactId>
										<versionRange>${it-plugin.version}</versionRange>
										<goals>
											<goal>manifest-update</goal>
											<goal>generate-sources</goal>
											<goal>proguard</goal>
											<goal>emma</goal>
											<goal>consume-aar</goal>
										</goals>
									</pluginExecutionFilter>
									<action>
										<ignore />
									</action>
								</pluginExecution>
							</pluginExecutions>
						</lifecycleMappingMetadata>
					</configuration>
				</plugin>

			</plugins>
		</pluginManagement>
		<plugins>
			<plugin>
				<groupId>com.simpligility.maven.plugins</groupId>

				<artifactId>android-maven-plugin</artifactId>
				<extensions>true</extensions>
				<configuration>
					<androidManifestFile>${project.basedir}/AndroidManifest.xml</androidManifestFile>
					<resourceDirectory>${project.basedir}/res</resourceDirectory>
					<assetsDirectory>${project.basedir}/assets</assetsDirectory>
					<sdk>
						<platform>19</platform>
					</sdk>
				</configuration>
			</plugin>
		</plugins>
	</build>


refs:  
[一个问题，有修改目录的提示](http://code.google.com/p/maven-android-plugin/issues/detail?id=61)  





[1]: http://simpligility.github.io/android-maven-plugin/examples.html
[2]: https://github.com/simpligility/android-maven-plugin
[3]: http://marketplace.eclipse.org/content/android-maven-eclipse