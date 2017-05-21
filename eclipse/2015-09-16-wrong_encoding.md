# 乱码

## eclipse 运行输出正常， 命令行 java 运行乱码
这个是在一个英文系统中运行java,输出中文时遇到的
javac 编译时可以指定一个编码， 是源文件的编码。 java 运行时还可以指定另一个编码， 这个暂时不知道怎么指定， 只会在 eclipse 中指定。
方法如下： 
菜单Run -> Debug Configration -> 在 Common 标签中， 有一个 Encoding, 这个指定错了就会乱码。