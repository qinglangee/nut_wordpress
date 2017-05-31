# view 属性

## 自定义命名空间

	xmlns:fresco="http://schemas.android.com/apk/res-auto"
	xmlns:app="http://schemas.android.com/apk/res-auto"
## 屏幕参数
获得屏幕宽高

	// 已过时
	int screenWidth = getWindowManager().getDefaultDisplay().getWidth(); // 屏幕宽（像素，如：480px）  
	int screenHeight = getWindowManager().getDefaultDisplay().getHeight(); // 屏幕高（像素，如：800p）

	// 新方法
	DisplayMetrics dm = new DisplayMetrics();
    getActivity().getWindowManager().getDefaultDisplay().getMetrics(dm);
    params.width = dm.widthPixels;
## view

*id冲突的范围*
只在context范围内冲突, 不同的xml可以有相同的id
有一个莫名其妙的错误, 一个layout中的TextView没有设置id, 导致遥远的另一个layout中LinearLayout的 findViewById 返回了这个没加ID的TextView, cast报错.........
*默认不显示*
`android:visibility="gone"`    恢复  setVisibility():
有三个参数：Parameters:visibility One of VISIBLE 可见的, INVISIBLE 不可见的，但还占着原来的空间, or GONE 不可见的，不占用原来的布局空间 ，想对应的三个常量值：0、4、8

透明度30%的白色, 可以当背景用

	<color name="bg_user_header_desc">#30FFFFFF</color>

## TextView
textview中有个内容过长加省略号的属性，即ellipsize，可以较偷懒地解决这个问题，哈哈~  
用法如下：  
在xml中

	android:ellipsize = "end"　　      省略号在结尾
	android:ellipsize = "start" 　   　省略号在开头
	android:ellipsize = "middle"     省略号在中间
	android:ellipsize = "marquee"    跑马灯


    android:text="@string/empty_msg_charm"
    android:textColor="@color/gray"
    android:textSize="15sp"
    android:textCursorDrawable="@null"，        "@null"作用是让光标颜色和text color一样

    android:drawableLeft="@drawable/chat_count_hint"      设置文本带的图片

最好加一个约束`android:singleLine = "true"`

## layout
要想写出好的Android程序，学好Android的layout布局是十分重要的。对于新手来说，一开始对布局可能比较模糊，以下列举出Android布局中经常用到的一些对齐属性介绍，希望对大家有帮助。
*不带"layout" 的属性是指控件中文本的格式，如gravity是指文本的对齐方式等等*  
[最外层 layout_param 相关的设置][4]

	android:layout_above    将该控件的底部至于给定ID的控件之上
	android:layout_below="@id/title"    将该控件的顶部至于给定ID的控件之下
	android:layout_toLeftOf    将该控件的右边缘和给定ID的控件的左边缘对齐
	android:layout_toStartOf
	android:layout_toRightOf    将该控件的左边缘和给定ID的控件的右边缘对齐
	android:layout_alignBaseline    该控件的baseline和给定ID的控件的baseline对齐
	android:layout_alignBottom    将该控件的底部边缘与给定ID控件的底部边缘
	android:layout_alignLeft     将该控件的左边缘与给定ID控件的左边缘对齐
	android:layout_alignStart
	android:layout_alignRight     将该控件的右边缘与给定ID控件的右边缘对齐
	android:layout_alignTop     将给定控件的顶部边缘与给定ID控件的顶部对齐
	android:layout_alignParentBottom     如果该值为true，则将该控件的底部和父控件的底部对齐
	android:layout_alignParentLeft="true"    如果该值为true，则将该控件的左边与父控件的左边对齐
	android:layout_alignParentStart="true"
	android:layout_alignParentRight="true"    如果该值为true，则将该控件的右边与父控件的右边对齐
	android:layout_alignParentTop="true"    如果该值为true，则将空间的顶部与父控件的顶部对齐
	android:layout_centerHorizontal="true"    如果值为真，该控件将被至于水平方向的中央
	android:layout_centerInParent="true"    如果值为真，该控件将被至于父控件水平方向和垂直方向的中央
	android:layout_centerVertical="true"    如果值为真，该控件将被至于垂直方向的中央
	android:layout_gravity="bottom" 

    android:background="@drawable/main_background"  设置背景色 
    android:background="#FF0000"
    android:alpha="0.5"                         设置透明度

    android:clickable="true"　　设置Layout为可点击状态，　这样才可以在　background　上设置　StateListDrawable
在 code 设置 layout


	LayoutParams params = (RelativeLayout.LayoutParams) mImage.getLayoutParams();
	params.removeRule(RelativeLayout.ALIGN_PARENT_START);
	params.addRule(RelativeLayout.ALIGN_PARENT_END, RelativeLayout.TRUE);

	.bringToFront();   // 设置zindex到最前

	// 宽度, 调试
	LayoutParams p = view.getLayoutParams();
	p.width = FrameLayout.LayoutParams.WRAP_CONTENT;
	p.height = FrameLayout.LayoutParams.MATCH_PARENT;

	// margin
	

	// match_parent

	// 文字对齐方式
	mContent.setGravity(Gravity.LEFT);


	// Relation 相关
	RelativeLayout.LayoutParams params = new RelativeLayout.LayoutParams(
            android.view.ViewGroup.LayoutParams.WRAP_CONTENT, android.view.ViewGroup.LayoutParams.WRAP_CONTENT);
    params.addRule(RelativeLayout.ALIGN_PARENT_LEFT);
    params.setMargins(20, 10, 10, 10);

	//  设置透明度
    RelativeLayout rl; ...
	rl.setAlpha(0.5F);
	Drawable background = backgroundimage.getBackground();
	background.setAlpha(80);

## linearLayout

	android:baselineAligned="false"   When set to false, prevents the layout from aligning its children's baselines. 
	android:orientation="vertical"     // 纵向
	android:orientation="horizontal"   // 横向
## View attribute

	android:background="@android:color/transparent"    　  背景景透明
	android:background="#e0000000"　　　　　　　　　　　 　　　　　　　　　　　　半透明
	android:background="#00000000"　　　　　　　　　　　　　　　　　　　　　　　　透明
## Button

	android:onClick="sendMessage"



	public void sendMessage(View view) {
	}

请注意，为了让系统能够将这个方法与在android:onClick属性中提供的方法名字匹配，它们的名字必须一致，特别是，这个方法必须满足以下条件：

* 公共的
* 没有返回值
* 有唯一的视图（View）参数（这个视图就是将被点击的视图）

## ListView

	
    android:divider="@color/sub_global_separator"   // 分隔线
    android:dividerHeight="1dp"  
	android:fadingEdge="none"                       // 去掉listview的上边和下边黑色的阴影。
	android:scrollingCache="false"           //解决listview在拖动的时候背景图片消失变成黑色背景。等到拖动完毕我们自己的背景图片才显示出来。
	或者 android:cacheColorHint="#00000000"
	listSelector="@android:color/transparent
去掉分隔线

	1, 设置android:divider="@null"
	2, android:divider="#00000000"     #00000000后面两个零表示透明
	3, .setDividerHeight(0)
## GridView

	android:listSelector="@android:color/transparent"  // 去掉gridView默认带的padding
    android:horizontalSpacing="2dp"          // 水平间距
    android:verticalSpacing="2dp"            // 垂直间距
    android:numColumns="3"                   // 列数

	GridView的item的分界线需要用背景色与item的颜色区别来实现
## ImageView
ScaleType可以设置的值有:
android.widget.ImageView.ScaleType, 各种[显示方式][3]  

	ScaleType[] SCALE_TYPES = {
	      ScaleType.MATRIX,
	      ScaleType.FIT_XY,             // 不按比例缩放图片，目标是把图片塞满整个View。
	      ScaleType.FIT_CENTER,         // 把图片按比例扩大/缩小到View的宽度，居中显示
	      ScaleType.FIT_START,          // 在图片缩放效果上与FIT_CENTER一样，只是显示的位置不同，FIT_START是置于顶部，FIT_CENTER居中，FIT_END置于底部。
	      ScaleType.FIT_END,
	      ScaleType.CENTER,             // 按图片的原来size居中显示，当图片长/宽超过View的长/宽，则截取图片的居中部分显示
	      ScaleType.CENTER_CROP,        // 按比例扩大图片的size居中显示，使得图片长(宽)等于或大于View的长(宽) 
	      ScaleType.CENTER_INSIDE       // 将图片的内容完整居中显示，通过按比例缩小或原来的size使得图片长/宽等于或小于View的长/宽
	}

	android:scaleType="CENTER"   // 拉伸方式 , 代码中设置 imageView.setScaleType(ImageView.ScaleType.CENTER);

圆角图片 lib

	<com.makeramen.roundedimageview.RoundedImageView
	        android:id="@+id/image"
	        android:layout_width="200dp"
	        android:layout_height="100dp"
	        android:layout_below="@id/title"
	        android:layout_alignParentStart="true"
	        android:layout_marginStart="10dp"
	        android:layout_marginTop="6dp"
	        android:contentDescription="@string/default_img_desc"
	        android:padding="1dp"
	        android:src="@drawable/ic_launcher"
	        app:riv_border_color="@color/green"
	        app:riv_border_width="3dip"
	        app:riv_corner_radius="30dip"
	        app:riv_oval="false" />

## ScrollView

Android SDK有两个滚动组件， HorizontalScrollView 和 ScrollView 。一个是水平滚动，另一个是垂直滚动。两个嵌套使用，可实现水平和垂直滚动

	android:scrollbars="none"        // 隐藏滚动条
## Shape 

	android:shape="rectangle"  // 画方框
	android:shape="oval"       // 画圆
## ViewStub

	<ViewStub
	    android:id="@+id/stub_import"
	    android:inflatedId="@+id/panel_import"
	    android:layout="@layout/progress_overlay"
	    android:layout_width="fill_parent"
	    android:layout_height="wrap_content"
	    android:layout_gravity="bottom" />
[about ViewStub][2]



## EditText

	android:inputType="textPassword"    // 密码
	android:hint="@string/login_input_password"     // 提示内容


## Dialog
Dialog 设置　背景透明／没有标题／contentView

	mProgress = new Dialog(getContext());
    mProgress.getWindow().setBackgroundDrawable(new ColorDrawable(android.R.color.transparent));
    mProgress.requestWindowFeature(Window.FEATURE_NO_TITLE);
    mProgress.setContentView(new ProgressBar(getContext()));
refs:  
[Android Layout中的一些对齐属性介绍][1]  


[1]: http://www.eoeandroid.com/thread-162482-1-1.html
[2]: http://developer.android.com/training/improving-layouts/loading-ondemand.html
[3]: http://blog.csdn.net/larryl2003/article/details/6919513
[4]: http://blog.csdn.net/cauchyweierstrass/article/details/41317247