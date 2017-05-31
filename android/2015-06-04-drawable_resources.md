# 可绘制资源　Drawable Resources

## 　分类
* Bitmap File
	位图的图形文件 (.png, .jpg, or .gif). 创建一个 BitmapDrawable.

* Nine-Patch File
	带可拉伸区域的　PNG，　允许图像根据设置的区域拉伸．(.9.png). 创建一个 NinePatchDrawable.
* Layer List
	一个包含其它 Drawable 组的 Drawable.　它们按数组顺序绘制，索引大的在上层． 创建一个 LayerDrawable.
* State List
	引用其它位图的 XML文件，　每个位图对应不同的状态． (for example, to use a different image when a button is pressed). 创建一个 StateListDrawable.
* Level List
	管理着一组 Drawables,　根据 level　的不同显示不同的　Drawables. 创建一个 LevelListDrawable.
* Transition Drawable
	两个　Drawable 之间过渡转换. 创建一个 TransitionDrawable.
* Inset Drawable
	An XML file that defines a drawable that insets another drawable by a specified distance. This is useful when a View needs a background drawble that is smaller than the View's actual bounds.
* Clip Drawable
	An XML file that defines a drawable that clips another Drawable based on this Drawable's current level value. 创建一个 ClipDrawable.
	切出图片的一部分显示，　通常用来实现进度条．
* Scale Drawable
	An XML file that defines a drawable that changes the size of another Drawable based on its current level value. 创建一个 ScaleDrawable
* Shape Drawable
	An XML file that defines a geometric shape, including colors and gradients. 创建一个 ShapeDrawable.

Also see the [Animation Resource][1] document for how to create an AnimationDrawable.


### Layer List
语法：

	<?xml version="1.0" encoding="utf-8"?>
	<layer-list
	    xmlns:android="http://schemas.android.com/apk/res/android" >
	    <item
	        android:drawable="@[package:]drawable/drawable_resource"
	        android:id="@[+][package:]id/resource_name"
	        android:top="dimension"
	        android:right="dimension"
	        android:bottom="dimension"
	        android:left="dimension" />
	</layer-list>
EXAMPLE:
XML file saved at res/drawable/layers.xml:

	<?xml version="1.0" encoding="utf-8"?>
	<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
	    <item>
	      <bitmap android:src="@drawable/android_red"
	        android:gravity="center" />
	    </item>
	    <item android:top="10dp" android:left="10dp">
	      <bitmap android:src="@drawable/android_green"
	        android:gravity="center" />
	    </item>
	    <item android:top="20dp" android:left="20dp">
	      <bitmap android:src="@drawable/android_blue"
	        android:gravity="center" />
	    </item>
	</layer-list>

### State List
语法：

	<?xml version="1.0" encoding="utf-8"?>
	<selector xmlns:android="http://schemas.android.com/apk/res/android"
	    android:constantSize=["true" | "false"]
	    android:dither=["true" | "false"]
	    android:variablePadding=["true" | "false"] >
	    <item
	        android:drawable="@[package:]drawable/drawable_resource"
	        android:state_pressed=["true" | "false"]
	        android:state_focused=["true" | "false"]
	        android:state_hovered=["true" | "false"]
	        android:state_selected=["true" | "false"]
	        android:state_checkable=["true" | "false"]
	        android:state_checked=["true" | "false"]
	        android:state_enabled=["true" | "false"]
	        android:state_activated=["true" | "false"]
	        android:state_window_focused=["true" | "false"] />
	</selector>
EXAMPLE:
XML file saved at res/drawable/button.xml:

	<?xml version="1.0" encoding="utf-8"?>
	<selector xmlns:android="http://schemas.android.com/apk/res/android">
	    <item android:state_pressed="true"　android:drawable="@drawable/button_pressed" /> <!-- pressed -->
	    <item android:state_focused="true"　android:drawable="@drawable/button_focused" /> <!-- focused -->
	    <item android:state_hovered="true"　android:drawable="@drawable/button_focused" /> <!-- hovered -->
	    <item android:drawable="@drawable/button_normal" /> <!-- default -->
	</selector>
### Level List
语法：

	<?xml version="1.0" encoding="utf-8"?>
	<level-list
	    xmlns:android="http://schemas.android.com/apk/res/android" >
	    <item
	        android:drawable="@drawable/drawable_resource"
	        android:maxLevel="integer"
	        android:minLevel="integer" />
	</level-list>


	<?xml version="1.0" encoding="utf-8"?>
	<level-list xmlns:android="http://schemas.android.com/apk/res/android" >
	    <item　android:drawable="@drawable/status_off"　android:maxLevel="0" />
	    <item　android:drawable="@drawable/status_on"　android:maxLevel="1" />
	</level-list>

Once this is applied to a View, the level can be changed with `setLevel()` or `setImageLevel()`.


### Shape Drawable
语法：

	<?xml version="1.0" encoding="utf-8"?>
	<shape
	    xmlns:android="http://schemas.android.com/apk/res/android"
	    android:shape=["rectangle" | "oval" | "line" | "ring"] >
	    <corners
	        android:radius="integer"
	        android:topLeftRadius="integer"
	        android:topRightRadius="integer"
	        android:bottomLeftRadius="integer"
	        android:bottomRightRadius="integer" />
	    <gradient
	        android:angle="integer"
	        android:centerX="integer"
	        android:centerY="integer"
	        android:centerColor="integer"
	        android:endColor="color"
	        android:gradientRadius="integer"
	        android:startColor="color"
	        android:type=["linear" | "radial" | "sweep"]
	        android:useLevel=["true" | "false"] />
	    <padding
	        android:left="integer"
	        android:top="integer"
	        android:right="integer"
	        android:bottom="integer" />
	    <size
	        android:width="integer"
	        android:height="integer" />
	    <solid
	        android:color="color" />
	    <stroke
	        android:width="integer"
	        android:color="color"
	        android:dashWidth="integer"
	        android:dashGap="integer" />
	</shape>
EXAMPLE:
XML file saved at res/drawable/gradient_box.xml:

	<?xml version="1.0" encoding="utf-8"?>
	<shape xmlns:android="http://schemas.android.com/apk/res/android"
	    android:shape="rectangle">
	    <gradient
	        android:startColor="#FFFF0000"
	        android:endColor="#80FF00FF"
	        android:angle="45"/>
	    <padding android:left="7dp"
	        android:top="7dp"
	        android:right="7dp"
	        android:bottom="7dp" />
	    <corners android:radius="8dp" />
	</shape>
This layout XML applies the shape drawable to a View:

	<TextView
	    android:background="@drawable/gradient_box"
	    android:layout_height="wrap_content"
	    android:layout_width="wrap_content" />
This application code gets the shape drawable and applies it to a View:

	Resources res = getResources();
	Drawable shape = res. getDrawable(R.drawable.gradient_box);

	TextView tv = (TextView)findViewByID(R.id.textview);
	tv.setBackground(shape);

refs:  
[Drawable Resources](http://developer.android.com/guide/topics/resources/drawable-resource.html#Shape)  





[1]: http://developer.android.com/guide/topics/resources/animation-resource.html