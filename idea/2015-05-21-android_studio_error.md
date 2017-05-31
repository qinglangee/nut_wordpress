# android studio 错误处理

## Error:Cannot locate factory for objects of type DefaultGradleConnector, as ConnectorServiceRegistry has been closed.
命令行gradle编译没有问题, android studio中就是不能编译. 工程删掉重新导入都不能解决
可能是上次导入gradle工程时没有处理完, 到 ~/.AndroidStudio 目录中找到项目相关的文件都删掉, 重新导入工程.

	find . |grep "your project name" |xargs rm -r