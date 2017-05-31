# 自定义绘图
自定义绘图主要有两种方式
１．　直接在View,Layout结构中插入自定义图形，系统负责绘制．（利用Drawable资源）
２．　用canvas画图　（游戏之类的）

## 用　Canvas画图　　Draw with a Canvas
这个也分两种实现方式，
１．　与UI Activity 在同一线程，　在创建自定义view的位置调用invalidate(), 然后在onDraw()回调方法中处理．
２．　在　SurfaceView　上面作图．　这个先按下不表．　

Canvas就相当于一个接口，你要画的所有内容都通过Canvas, 它会把要绘制的内容画到一个Bitmap上，放到window中．
*Canvas会在　onDraw()方法中给你提供好的！！，　SurfaceView中用　SurfaceHolder.lockCanvas()*

如果要新建一个Canvas的话，就必须要提供一个Bitmap, Canvas总是要画在Bitmap上的嘛．

	Bitmap b = Bitmap.createBitmap(100, 100, Bitmap.Config.ARGB_8888);
	Canvas c = new Canvas(b);
画完后可以通过　`Canvas.drawBitmap(Bitmap,...)`　把Bitmap画到另一个Canvas上面, 但推荐的方法还是在目标Canvas上直接画图形．
[Canvas][1]有一系列的drawXXX()方法，　像是`drawBitmap(...), drawRect(...), drawText(...)`, 还有很多其它的．
可能用到的其它类也有`draw()`方法, 如[Drawable][2]对象有它的`draw()`方法，　会引用Canval作参数

### 在View上　　On a View

刷新率要求不高的ＡＰＰ，　就继承View 组件，　在`View.onDraw()`方法中用Canvas画就可以了．　这个方便之处就是　Canvas 是由系统提供好的．

Android系统只在需要时调用onDraw(), 当你的应用准备好可以绘制时，需要显式调用　`invalidate()`, 系统就会去调用`onDraw()`, 虽然可能不是立即调用．

Note: *在主线程之外请求刷新，要调用`postInvalidate()`方法*

For information about extending the View class, read [Building Custom Components][3].
For a sample application, see the Snake game, in the SDK samples folder: `<your-sdk-directory>/samples/Snake/`

### On a SurfaceView
TODO ZHCH


## Drawables

TODO ZHCH


refs:  
[Canvas and Drawables](http://developer.android.com/guide/topics/graphics/2d-graphics.html)  
[Custom Components(要好好理解一下)](http://developer.android.com/guide/topics/ui/custom-components.html)  




[1]:http://developer.android.com/reference/android/graphics/Canvas.html
[2]: http://developer.android.com/reference/android/graphics/drawable/Drawable.html
[3]: http://developer.android.com/guide/topics/ui/custom-components.html