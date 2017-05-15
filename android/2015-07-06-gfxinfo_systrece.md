# android 性能分析工具之　gfxinfo

gfxinfo　　GPU呈现模式分析

在开发者模式中打开->GPU呈现模式分析，滑动几下界面后，在 adb shell 中执行　`adb shell dumpsys gfxinfo com.example.demo`
在输出内容中标题为`Profile data in ms`的就是图像处理和显示的时间．　三个值加起来是渲染一帧需要的时间．

* Draw 是在Java中创建显示列表所需要的时间。这个值显示了运行绘图函数用了多长时间，比如View.onDraw(Canvas)。
* Process 是Android 2D引擎渲染显示列表所需要的时间。在界面中View数目越多，则有越多的绘制命令需要执行。
* Execute 是把一帧数据送到屏幕上排版显示的时间，这个时间通常比较小。

注意：要流畅的运行60帧/秒， 则需要每帧的处理时间不超过16ms。

# systrace

*adb shell: 如果手机系统中没有/sys/kernel/debug/tracing 目录就不能执行　systrace　功能*



refs:  
[Android 性能分析](http://blog.chengyunfeng.com/?p=458)  
