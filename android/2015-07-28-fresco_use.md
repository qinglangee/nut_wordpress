# Fresco 入门使用
Fresco是Facebook最新推出的一款用于Android应用中展示图片的强大图片库，可以从网络、本地存储和本地资源中加载图片。下面我们来看一下如何在项目中 Fresco 的初级用法.

## 首先是引入 Fresco
在 Android Studio 或者 Gradle 中就很简单,添加 dependency 就可以了

	dependencies {
	  // 其它的依赖
	  // ...
	  compile 'com.facebook.fresco:fresco:0.6.0+'
	}
Eclipse 中添加参照[英文文档][1]中 Eclipse 相关段落.

## 开始使用 Fresco 
常规应用就是网络中下载图片然后显示.  
在 Application 初始化时，在应用调用 `setContentView()` 之前，进行初始化：

	Fresco.initialize(context);
初始化方法只能调用一次, 可以在 Application 类中调用, 在每个Activity中调用初始化方法是*不对的*.

在xml布局文件中, 加入fresco的自定义命名空间：

	xmlns:fresco="http://schemas.android.com/apk/res-auto"

在布局中添加 `SimpleDraweeView`, 

	<com.facebook.drawee.view.SimpleDraweeView
	    android:id="@+id/my_image_view"
	    android:layout_width="130dp"
	    android:layout_height="130dp"
	    fresco:placeholderImage="@drawable/my_drawable"
	  />
然后添加下面的代码来显示图片:

	Uri uri = Uri.parse("https://raw.githubusercontent.com/facebook/fresco/gh-pages/static/fresco-logo.png");
	SimpleDraweeView draweeView = (SimpleDraweeView) findViewById(R.id.my_image_view);
	draweeView.setImageURI(uri);
Fresco 来做剩下的事.


refs:  
[Getting started with Fresco ](http://frescolib.org/docs/getting-started.html#_)  


[1]: http://frescolib.org/docs/index.html#_