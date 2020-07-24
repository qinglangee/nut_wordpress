# c盘空间不足
今天突然遇到C盘的空间条红了，C盘除了系统自己运行，什么软件也不往里面装的，莫名其妙。 原来还有9G多的空间的
C盘全选了文件看了一下，只20多G，整个盘48G,相差也太多了。
上网查了一通也没找到什么真正原因的方法。可能的原因罗列一下有下面这些

1 显示隐藏文件。  这个已经做了
2 显示系统隐藏文件。  这个解决了10G，还差的10多G还是匹配不上。
3 系统更新文件。  控制面板->系统和安全->管理工具->释放磁盘空间 。  显示有3G多的垃圾，清理完就多了不到1G，王德发。
4 系统还原。 System Volume Information 目录中会存储还原文件，很大。 我没开系统还原。
	系统 -> 存储 -> 立即释放空间 也试过，没放出多少。
5 安装系统，以前的旧系统文件。 并没有
6 驱动更新，旧驱动占了很大空间。 我并没有更新。 [驱动查看软件 DriverStoreExplorer][1], 有[github版本 DriverStoreExplorer][3]  
	软件新版本有【选取旧的驱动】按钮，以后要用的话可以下个新的看看。
7 有休眠功能的话会有个休眠文件很大  (hiberfil.sys)。 这个有，不过不想关休眠。 可能还真是休眠搞的，刚装系统还没用休眠时好像就是剩10G多的空间。 这个休眠文件也是9G多。。。。。 不过其实那时用没用休眠记不太清了。 再不过休眠文件也是计算大小的，文件占用跟磁盘整体占用还是对不上数。[这里][2]还有调整休眠文件大小的方法，不过不能调太小，容易导致休眠失败。
`以管理员身份运行C：\windows\system32\cmd.exe--执行命令：powercfg -h off。休眠文件便不再存在。`

8 配置系统
win10在“设置--系统--存储--存储感知”中按钮打开，能够定期自行清除垃圾 

还是他娘的没搞定，就TMD剩下2G多的空间了，再TMD减就要重装系统了。

9 虚拟内存存放位置  我的本来就在D盘
	电脑->属性->高级系统设置->高级->性能->设置->高级->虚拟内存->更改。
10 修改临时文件夹目录  我的user用户名目录就链接到外面了，只改下系统目录就可以了。
	在另外的盘新建 User Windows目录，把TEMP 和 TMP 环境变量改到外面存放。 用户变量和系统变量分别设置。 设置完确定并重启电脑，就可以删除原目录下的缓存了。
	系统原来的目录在 `%SystemRoot%\Temp   C:\Windows\Temp`
	用户目录在 `%USERPROFILE%\AppData\Local\Temp`
11 显卡驱动备份
	NVIDIA 显卡的目录 `c:\Program Files\NVIDIA Corporation\Installer2\` 在这个目录下的除了 InstallerCore 都是单项备份，可以在程序控制那里单独删除，不需要这个功能可以删除 InstallerCore 以外的。
	如果使用 GeForce Experience 进行更新，在 `c:\Program Files\NVIDIA Corporation\Downloader\latest` 目录有下载的安装包，装完后全删除就行。  
12 Windows其它目录  可以按需删除
	Windows 日志目录 `C:\Windows\System32\winevt\Logs`  
	Windows 更新临时文件 `C:\Windows\SoftwareDistribution\Download`  
	系统升级补丁备份 `C:\Windows\WinSxS\Backup`
13 昨天系统自动更新了一下，刚更新完时查看系统容量还是所剩无几。又过一天不知道啥原因，丢的10几G回来了。 可能是下载的更新文件自己删除了吧，反正真不是这个原因也没搞清楚。
refs:  
[1]: http://dl.pconline.com.cn/download/373628.html
[2]: https://jingyan.baidu.com/article/e75aca85229cab142edac6a9.html
[3]: https://github.com/lostindark/DriverStoreExplorer/releases/tag/v0.9.35