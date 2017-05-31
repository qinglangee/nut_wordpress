# 屏幕密度 dip

有些时候，我们需要获取Android手机或Pad的屏幕的物理尺寸，以便于界面的设计或是其他功能的实现。下面就介绍讲一讲如何获取屏幕的物理尺寸：
从网上找过不少资料，发现获取屏幕尺寸并不是很复杂的编程操作，下面的代码即可获取屏幕的尺寸。
在一个Activity的onCreate方法中，写入如下代码：

        DisplayMetrics metric = new DisplayMetrics();
        getWindowManager().getDefaultDisplay().getMetrics(metric);
        int width = metric.widthPixels;  // 屏幕宽度（像素）
        int height = metric.heightPixels;  // 屏幕高度（像素）
        float density = metric.density;  // 屏幕密度（0.75 / 1.0 / 1.5）
        int densityDpi = metric.densityDpi;  // 屏幕密度DPI（120 / 160 / 240）

但是，需要注意的是，在一个低密度的小屏手机上，仅靠上面的代码是不能获取正确的尺寸的。比如说，一部240x320像素的低密度手机，如果运行上述代码，获取到的屏幕尺寸是320x427。因此，研究之后发现，若没有设定多分辨率支持的话，Android系统会将240x320的低密度（120）尺寸转换为中等密度（160）对应的尺寸，这样的话就大大影响了程序的编码。所以，需要在工程的AndroidManifest.xml文件中，加入supports-screens节点，具体的内容如下：

    <supports-screens
        android:smallScreens="true"
        android:normalScreens="true"
        android:largeScreens="true"
        android:resizeable="true"
        android:anyDensity="true" />
这样的话，当前的Android程序就支持了多种分辨率，那么就可以得到正确的物理尺寸了。




为简单起见，Android把所有的屏幕分辨率也分为四种尺寸：小，普通，大，超大(分别对应：small, normal, large, and extra large).

应用程序可以为这四种尺寸分别提供不同的资源-平台将透明的对资源进行缩放以适配指定的屏幕分辨率。

要调整不同的设备屏幕密度，我们需要在四个密度大小之间按照3:4:6:8缩放比例。使用这些比率，通过简单的计算，android创造四个不同的版本的位图，以供开发生产：

    75*75对应低密度屏幕（如0.75）; ---ldpi
    100*100对应中等密度的屏幕（基准）; ---mdpi
    150*150对应高密度屏幕（ 1.5）; ---hdpi
    200*200对应超高密度显示屏（ 2.0）。 ---xdpi



重中之重：
>density值表示每英寸有多少个显示点，与分辨率是两个不同的概念：

Android主要有以下几种屏：

QVGA和WQVGA屏density=120；

HVGA屏density=160；

WVGA屏density=240；

下面以480dip*800dip的WVGA(density=240)为例，详细列出不同density下屏幕分辨率信息：

当density=120时 屏幕实际分辨率为240px*400px （两个点对应一个分辨率）
状态栏和标题栏高各19px或者25dip
横屏是屏幕宽度400px 或者800dip,工作区域高度211px或者480dip
竖屏时屏幕宽度240px或者480dip,工作区域高度381px或者775dip

density=160时 屏幕实际分辨率为320px*533px （3个点对应两个分辨率）
状态栏和标题栏高个25px或者25dip
横屏是屏幕宽度533px 或者800dip,工作区域高度295px或者480dip
竖屏时屏幕宽度320px或者480dip,工作区域高度508px或者775dip

density=240时 屏幕实际分辨率为480px*800px （一个点对于一个分辨率）
状态栏和标题栏高个38px或者25dip
横屏是屏幕宽度800px 或者800dip,工作区域高度442px或者480dip
竖屏时屏幕宽度480px或者480dip,工作区域高度762px或者775dip

apk的资源包中，当屏幕density=240时使用hdpi标签的资源
当屏幕density=160时，使用mdpi标签的资源
当屏幕density=120时，使用ldpi标签的资源。
不加任何标签的资源是各种分辨率情况下共用的。
建议：布局时尽量使用单位dip，少使用px。

device independent pixels(设备独立像素). 不同设备有不同的显示效果,这个和设备硬件有关，一般我们为了支持WVGA、HVGA和QVGA 推荐使用这个，不依赖像素。

refs: 
[android获取屏幕尺寸、密度](http://www.cnblogs.com/wangtianxj/archive/2011/03/18/1988358.html)   
[Android-dip-dp-sp-pt-px](http://greatverve.cnblogs.com/archive/2011/12/27/Android-dip-dp-sp-pt-px.html)  