# linux iptables 配置

## 起源
Linux 内核 2.4开始引入了全新的包处理引擎-Netfilter, 还提供了一个命令行工具iptables来管理它.
## 概念
iptables把一些规则的"链"应用到网络包上面.  
一些链的集合组成tables被用来处理各种流量.
## 目标

## 配置
Linux 防火墙通常就是 *rc* 启动脚本里的一系列 *iptables* 命令, 每条命令格式通常是下面几种:

	iptables -F chain-name
	iptables -P chain-name target
	iptables -A chain-name -i interface -j target
## 一个复杂的示例

refs:

*Unix And Linux System Administration Handbook* P935  22.12 LINUX FIREWALL FEATURES  
[linux下IPTABLES配置详解][1]  
[9个常用iptables配置实例][2]  


[1]: http://www.cnblogs.com/JemBai/archive/2009/03/19/1416364.html
[2]: http://www.cnblogs.com/bangerlee/archive/2013/02/27/2935422.html
