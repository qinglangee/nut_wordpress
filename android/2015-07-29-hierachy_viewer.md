# HierachyViewer 相关问题
打开[hierarchy viewer][3]:

1. 在 Android Studio 中, Tools > Android Device Monitor 或点击 Android Device Monitor 图标 ![icon][1] . 点击打开视图 ![视图][2], 选择 Hierarchy View
2. 从 SDK tools/ 目录, 输入:

	monitor

TreeView 界面的右上角有一个捕捉处理时间的按钮, 默认不点不显示时间.

To preserve security, Hierarchy Viewer can only connect to devices running a developer version of the Android system.
使用 Hierarchy Viewer 需要手机上安装的是开发版本系统  

Hierarchy Viewer在连接手机时，手机上必须启动一个叫View Server的客户端与其进行socket通信。而在商业手机上，是无法开启View Server的，故Hierarchy Viewer是无法连接到普通的商业手机。


检验一台手机是否开启了View Server的办法为：
`adb shell service call window 3`
若返回值是：Result: Parcel(00000000 00000000 '........')" 说明View Server处于关闭状态
若返回值是：Result: Parcel(00000000 00000001 '........')" 说明View Server处于开启状态

若是一台可以打开View Server的手机（Android开发版手机 、模拟器or 按照[本帖步骤][4]给系统打补丁的手机），我们可以使用以下命令打开View Server：
`adb shell service call window 1 i32 4939`
使用以下命令关闭View Server：
`adb shell service call window 2 i32 4939`




refs:  
[优化UI](http://developer.android.com/tools/debugging/debugging-ui.html)  
[如何在Root的手机上开启ViewServer，使得HierachyViewer能够连接][4]
[解决View Hierarchy不能启动](http://seo.plar.cn/seo-2032.html)  

[1]: http://developer.android.com/images/tools/hierarchicalviewer-icon.png "Android Device Monitor"
[2]: http://developer.android.com/images/tools/studio-DDMS-open-perspective-icon.png "Open Perspectives icon"
[3]: http://developer.android.com/tools/help/hierarchy-viewer.html
[4]: http://maider.blog.sohu.com/255448342.html