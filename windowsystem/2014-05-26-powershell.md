# windows powershell
windows下有个加强版的cmd shell, 建立在.NET Framework之上， 可以更方便的使用，控制windows.  
[有关PowerShell脚本你必须知道的十个基本概念][1]  
[通过 Windows PowerShell 编写脚本][2]  

## window7下安装配置powershell
Windows 7, Windows 8, Server 2008 R2,Server 2012默认带有powershell, Vista SP1 和 SP2, Server 2008 SP1 , SP2, Server 2003 SP2, Windows XP SP3则可以单独安装。Powershell 3.0 在win8和2012中是预装的, win7和2012需要升级才能用3.0.

1. 安装.NET Framework 4.0 或更新版本.  

[.NET Framework v4.0][4] 或 [.NET Framework v4.5][5]

2. 安装 Windows Management Framework 3.0

[Windows Remote Management Framework v3.0][6]  装完需要重启.

3. 配置powershell可以运行脚本

以管理员权限运行powershell, 执行下面的命令:

	Set-ExecutionPolicy RemoteSigned

4. 配置 WinRM

以管理员权限打开一个命令行,运行以下命令:

	net start winrm
	winrm set winrm/config/client/auth @{Basic="true"}

打完收工!

## 配置powershell的配置文件
在powershell中输入`$profile`就会显示配置文件的位置
## powershell中配置别名命令
显示系统自带的别名设置

	get-alias
设置一个别名

	Set-Alias d Get-Date
将别名设置保存到文件中并引用文件

	Export-Alias C:\Files\MyAliases.txt   # 导出(包含用户定义和内建的)
	Import-Alias C:\Files\MyAliases.txt   # 导入 (导入内建别名时会报错, 虽然能用, 可以编辑MyAliases.txt把内建的干掉就好)
设置别名不能带参数, 如果带参数要先放在function中, 再对function设置别名(真是2B), 或者直接调用function. 管道命令也不能直接别名,要放到function中

	Set-Alias toOld (Set-Location C:\Scripts\old)  # 报错
	# 正确做法
	function toOld{Set-Location C:\Scripts\Old}
	set-alias to toOld

	Set-Alias as (Get-Alias | Sort-Object) # 错误

 * 把要设置的别名放到profile文件中 *


## powershell 中安装posh-git
安装posh-git可以让git与powershell更好地集成(提供git命令的提示), powershell中git没有颜色区分很不爽  
先安装PsGet, 打开powershell, 执行下面命令  

	(new-object Net.WebClient).DownloadString("http://psget.net/GetPsGet.ps1") | iex
然后安装 posh-git  

	install-module posh-git


顺便介绍一个git 进阶游戏 [githug][7]

参考资料：  
[How to install/configure Powershell 3.0 in Windows 7 SP1][3]  
[Windows PowerShell Aliases][8]  
[The Windows PowerShell Profile][10]  
[Setting up Git in PowerShell][9]

[1]: http://os.51cto.com/art/201101/244228.htm
[2]: http://technet.microsoft.com/zh-cn/scriptcenter/powershell.aspx
[3]: http://www.everonit.com/techtips/techtips/how-to-installconfigure-powershell-3-0-in-windows-7-sp1/
[4]: http://go.microsoft.com/fwlink/?LinkID=212547
[5]: http://go.microsoft.com/fwlink/?LinkID=242919
[6]: http://www.microsoft.com/en-us/download/details.aspx?id=34595
[7]: https://github.com/Gazler/githug/blob/master/README.md
[8]: http://technet.microsoft.com/en-us/library/ee692685.aspx
[9]: http://thepracticalsysadmin.com/setting-up-git-in-windows/
[10]: http://technet.microsoft.com/en-us/library/ee692764.aspx
