# android 资源文件

## 资源目录的分类
Android的各种[资源类型][2]存储在res/下面的各个目录中

	animator/	XML files that define property animations.
	anim/	    XML files that define tween animations. 两个目录放两种不同的动画 

	color/	    颜色
	drawable/	位图 (.png, .9.png, .jpg, .gif) 或可编译成下列资源的 XML
		Bitmap files
		Nine-Patches (re-sizable bitmaps)
		State lists
		Shapes
		Animation drawables
		Other drawables
	mipmap/	    图标
	layout/	    布局 XML
	menu/	    菜单 XML
	raw/	    To open these resources with a raw InputStream, call Resources.openRawResource()
	            保留原本格式的文件. 需要目录层级的放在 assets/ 目录中, assets 目录中的内容没有生成 ID. 只能用 AssetManager读取
	values/	    放简单值的 XML (such as strings, integers, and colors), 可以混合,随便放.
	xml/        可以用Resources.getXML()读取的任意XML文件.  Various XML configuration files must be saved here, such as a searchable configuration.
				For example, an XML file that defines a PreferenceScreen, AppWidgetProviderInfo, or Searchability Metadata. 
*Caution: 不要在 res/ 目录中直接保存 XML文件 , 会导致编译错误*

## 提供替换资源 Providing Alternative Resources
资源修饰符: 多个资源修饰符的顺序要与[文档][1]中 table2 给出的顺序相同. 

## 创建别名资源  Creating alias resources

### Drawable
1.在res/drawable/目录中创建一个文件 icon_ca.png
2.在不同的目录中用icon.xml引用它

	<?xml version="1.0" encoding="utf-8"?>
	<bitmap xmlns:android="http://schemas.android.com/apk/res/android"
	    android:src="@drawable/icon_ca" />
### Layout
用`<merge>`包含一个`<include>` 

	<?xml version="1.0" encoding="utf-8"?>
	<merge>
	    <include layout="@layout/main_ltr"/>
	</merge>
### String 和其它简单资源  Strings and other simple values

	<?xml version="1.0" encoding="utf-8"?>
	<resources>
	    <string name="hello">Hello</string>
	    <string name="hi">@string/hello</string>
	</resources>

## 访问资源
从代码中访问

	[<package_name>.]R.<resource_type>.<resource_name>
从xml中访问

	@[<package_name>:]<resource_type>/<resource_name>
引用样式属性  Referencing style attributes
*resource_type 是可选的*

	?[<package_name>:][<resource_type>/]<resource_name>

	<EditText id="text"
	    android:layout_width="fill_parent"
	    android:layout_height="wrap_content"
	    android:textColor="?android:textColorSecondary"
	    android:text="@string/hello_world" />


refs:  
[资源类型][2]
[Providing Resources](http://developer.android.com/guide/topics/resources/providing-resources.html)  
[Accessing Resources](http://developer.android.com/guide/topics/resources/accessing-resources.html)



[1]: http://developer.android.com/guide/topics/resources/providing-resources.html#AlternativeResources
[2]: http://developer.android.com/guide/topics/resources/available-resources.html