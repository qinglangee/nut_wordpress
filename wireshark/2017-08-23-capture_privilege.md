# wireshark 权限设置
linux下wireshark新版本不允许使用root权限运行了．需要分权限设置．　  
wireshark程序本身用普通用户权限运行，底层捕捉网卡数据的程序(WinPcap, dumpcap等)用root权限运行
## ubuntu 
简单来说，wireshark安装后会新建一个wireshark分组，把需要运行wireshark的用户回到wireshark分组中就可以了．

## windows
windows 一般用管理员运行就可以了

## 具体 wireshark 设置步骤
见下面 refs 1:How To Set Up a Capture



refs:  
[1. How To Set Up a Capture](https://wiki.wireshark.org/CaptureSetup/)  
[2. Platform-Specific information about capture privileges](https://wiki.wireshark.org/CaptureSetup/CapturePrivileges)  
[3. Content of /usr/share/doc/wireshark-common/README.Debian](https://anonscm.debian.org/viewvc/collab-maint/ext-maint/wireshark/trunk/debian/README.Debian?view=markup)  