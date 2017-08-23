# ubuntu 网络信息配置
笔记本ubuntu /boot目录下删除了一堆东西之后，无线网络不能用了,只好手动重新配置一下．

## 查看网卡硬件信息
如果系统安装过网卡驱动，应该能识别硬件，使用命令 `sudo lshw -C network`
lshw 命令用来显示系统硬件信息，　network 说明显示网卡信息，　-C 说明显示详细信息
输出：
```
*-network               
     description: Ethernet interface
     product: RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller
     vendor: Realtek Semiconductor Co., Ltd.
     physical id: 0
     bus info: pci@0000:04:00.0
     logical name: enp4s0
     version: 10
     serial: c8:5b:76:c0:82:27
     size: 10Mbit/s
     capacity: 1Gbit/s
     width: 64 bits
     clock: 33MHz
     capabilities: pm msi pciexpress msix vpd bus_master cap_list ethernet physical tp mii 10bt 10bt-fd 100bt 100bt-fd 1000bt 1000bt-fd autonegotiation
     configuration: autonegotiation=on broadcast=yes driver=r8169 driverversion=2.3LK-NAPI duplex=half firmware=rtl8168g-3_0.0.1 04/23/13 latency=0 link=no multicast=yes port=MII speed=10Mbit/s
     resources: irq:124 ioport:c000(size=256) memory:f4204000-f4204fff memory:f4200000-f4203fff
*-network
     description: Wireless interface
     product: Qualcomm Atheros
     vendor: Qualcomm Atheros
     physical id: 0
     bus info: pci@0000:05:00.0
     logical name: wlp5s0
     version: 31
     serial: 28:56:5a:9f:1d:f5
     width: 64 bits
     clock: 33MHz
     capabilities: pm msi pciexpress bus_master cap_list ethernet physical wireless
     configuration: broadcast=yes driver=ath10k_pci driverversion=4.8.0-58-generic firmware=WLAN.TF.1.0-00267-1 latency=0 link=no multicast=yes wireless=IEEE 802.11
     resources: irq:128 memory:f4000000-f41fffff
```
description: Ethernet interface 是有线网卡，logical name: enp4s0
description: Wireless interface 是无线网卡，logical name: wlp5s0
如果没有安装驱动，系统未识别硬件，那么无线可能显示不出来．　（有线网卡驱动安装了，却没有加载模块，结果无线网卡没有logic　name的情况，[原文][1]有讲）

可我系统都显示正常，不需要下面的安装驱动的什么步骤，就是连不了wifi....
后来什么也没改，重启系统就好了．．．．．．．重启大法显神勇！！


refs:  
[ubuntu下无线网卡解决经历](http://www.blog.chinaunix.net/uid-25885064-id-3154645.html)  


[1]: http://m.blog.chinaunix.net/uid-25885064-id-3154645.html