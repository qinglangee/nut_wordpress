# android 动画资源
Anroid 动画资源分为两种，属性动画（Property Animation）和视图动画（View Animation）．  
视图动画又分为两种：  

1. 过渡动画：　一张图片进行一系列的转换
2. 帧动画：　一系列图片的动画，　用　AnimationDrawable　显示.

## 属性动画  Property Animation
属性动画一般放在 `res/animator/filename.xml` 目录，　会被编译成　 [ValueAnimator][1], [ObjectAnimator][2],  [AnimatorSet][3] 这几种类型.  
语法：

	<set
	  android:ordering=["together" | "sequentially"]>

	    <objectAnimator
	        android:propertyName="string"
	        android:duration="int"
	        android:valueFrom="float | int | color"
	        android:valueTo="float | int | color"
	        android:startOffset="int"
	        android:repeatCount="int"
	        android:repeatMode=["repeat" | "reverse"]
	        android:valueType=["intType" | "floatType"]/>

	    <animator
	        android:duration="int"
	        android:valueFrom="float | int | color"
	        android:valueTo="float | int | color"
	        android:startOffset="int"
	        android:repeatCount="int"
	        android:repeatMode=["repeat" | "reverse"]
	        android:valueType=["intType" | "floatType"]/>

	    <set>
	        ...
	    </set>
	</set>
文件的根元素必须是　`<set>, <objectAnimator>,  <valueAnimator>` 三个中的一个，　`<set>`可以用来组合其它的元素．

*`<objectAnimator>`*　在一个对象上执行动画．
*`<animator>`* 再看看吧．

示例

	<?xml version="1.0" encoding="utf-8"?>
	<set xmlns:android="http://schemas.android.com/apk/res/android"
	    android:ordering="sequentially">
	    <set>
	        <objectAnimator
	            android:propertyName="x"
	            android:duration="500"
	            android:valueTo="400"
	            android:valueType="intType" />
	        <objectAnimator
	            android:propertyName="y"
	            android:duration="500"
	            android:valueTo="300"
	            android:valueType="intType" />
	    </set>
	    <objectAnimator
	        android:propertyName="alpha"
	        android:duration="500"
	        android:valueTo="1f" />
	</set>

把动画应用到Object上

	AnimatorSet set = (AnimatorSet) AnimatorInflater.loadAnimator(myContext,
	    R.anim.property_animator);
	set.setTarget(myObject);
	set.start();

## 视图动画　　View Animation
### Tween animation
文件位置　`res/anim/filename.xml`, 资源文件指向 [Animation][4].
语法：　  
pivotX/pivotY : ("50" for 50% relative to the parent, or "50%" for 50% relative to itself).

	<?xml version="1.0" encoding="utf-8"?>
	<set xmlns:android="http://schemas.android.com/apk/res/android"
	    android:interpolator="@[package:]anim/interpolator_resource"
	    android:shareInterpolator=["true" | "false"] >
	    <alpha
	        android:fromAlpha="float"
	        android:toAlpha="float" />
	    <scale
	        android:fromXScale="float"
	        android:toXScale="float"
	        android:fromYScale="float"
	        android:toYScale="float"
	        android:pivotX="float"
	        android:pivotY="float" />
	    <translate
	        android:fromXDelta="float"
	        android:toXDelta="float"
	        android:fromYDelta="float"
	        android:toYDelta="float" />
	    <rotate
	        android:fromDegrees="float"
	        android:toDegrees="float"
	        android:pivotX="float"
	        android:pivotY="float" />
	    <set>
	        ...
	    </set>
	</set>
示例：

	<?xml version="1.0" encoding="utf-8"?>
	<set xmlns:android="http://schemas.android.com/apk/res/android"
	    android:shareInterpolator="false">
	    <scale
	        android:interpolator="@android:anim/accelerate_decelerate_interpolator"
	        android:fromXScale="1.0"
	        android:toXScale="1.4"
	        android:fromYScale="1.0"
	        android:toYScale="0.6"
	        android:pivotX="200%"
	        android:pivotY="200%"
	        android:duration="700" />
	    <set
	        android:interpolator="@android:anim/accelerate_interpolator"
	        android:startOffset="700">
	        <scale
	            android:fromXScale="1.4"
	            android:toXScale="0.0"
	            android:fromYScale="0.6"
	            android:toYScale="0.0"
	            android:pivotX="50%"
	            android:pivotY="50%"
	            android:duration="1400" />
	        <rotate
	            android:fromDegrees="0"
	            android:toDegrees="-45"
	            android:toYScale="0.0"
	            android:pivotX="50%"
	            android:pivotY="50%"
	            android:duration="400" />
	    </set>
	</set>
应用：

    Animation anim = AnimationUtils.loadAnimation(this, R.anim.basic_tween_01);
    mTargetImage.startAnimation(anim);
#### android:interpolator
Interpolator 被用来修饰动画效果，定义动画的变化率，可以使存在的动画效果accelerated(加速)，decelerated(减速),repeated(重复),bounced(弹跳)等。

AccelerateDecelerateInterpolator 在动画开始与结束的地方速率改变比较慢，在中间的时候加速

* AccelerateInterpolator  在动画开始的地方速率改变比较慢，然后开始加速
* AnticipateInterpolator 开始的时候向后然后向前甩
* AnticipateOvershootInterpolator 开始的时候向后然后向前甩一定值后返回最后的值
* BounceInterpolator   动画结束的时候弹起
* CycleInterpolator 动画循环播放特定的次数，速率改变沿着正弦曲线
* DecelerateInterpolator 在动画开始的地方快然后慢
* LinearInterpolator   以常量速率改变
* OvershootInterpolator    向前甩一定值后再回到原来位置

如果android定义的interpolators不符合你的效果也可以自定义interpolators

#### 自定义　interpolator
自定义　interpolator 文件放在 `res/anim/filename.xml`, 会被编译成上面对应的各种 Interpolator　类　　
语法：　

	<?xml version="1.0" encoding="utf-8"?>
	<InterpolatorName xmlns:android="http://schemas.android.com/apk/res/android"
	    android:attribute_name="value"
	    />
各个属性(attribute_name)的具体定义见[文档][5]  
示例:

	<?xml version="1.0" encoding="utf-8"?>
	<overshootInterpolator xmlns:android="http://schemas.android.com/apk/res/android"
	    android:tension="7.0"
	    />
Note: *各个 interpolator 在自定义文件中是以小写字母开头的*  
在　Animation　中使用：

	<scale xmlns:android="http://schemas.android.com/apk/res/android"
	    android:interpolator="@anim/my_overshoot_interpolator"
	    ...
	    android:duration="700" />
### 帧动画 Frame animation
就类似放电影了，　文件定义位置　`res/drawable/filename.xml`, 被编译成[AnimationDrawable][6]  

语法：

	<?xml version="1.0" encoding="utf-8"?>
	<animation-list xmlns:android="http://schemas.android.com/apk/res/android"
	    android:oneshot=["true" | "false"] >
	    <item
	        android:drawable="@[package:]drawable/drawable_resource_name"
	        android:duration="integer" />
	</animation-list>
示例： `res/drawable/rocket_thrust.xml`

	<?xml version="1.0" encoding="utf-8"?>
	<animation-list xmlns:android="http://schemas.android.com/apk/res/android"
	    android:oneshot="false">
	    <item android:drawable="@drawable/rocket_thrust1" android:duration="200" />
	    <item android:drawable="@drawable/rocket_thrust2" android:duration="200" />
	    <item android:drawable="@drawable/rocket_thrust3" android:duration="200" />
	</animation-list>
应用：

	ImageView rocketImage = (ImageView) findViewById(R.id.rocket_image);
	rocketImage.setBackgroundResource(R.drawable.rocket_thrust);

	rocketAnimation = (AnimationDrawable) rocketImage.getBackground();
	rocketAnimation.start();
refs:  
[Animation Resource](http://developer.android.com/guide/topics/resources/animation-resource.html#View)  
[android之interpolator的用法详解 ](http://blog.csdn.net/jason0539/article/details/16370405)  


[1]: http://developer.android.com/reference/android/animation/ValueAnimator.html
[2]: http://developer.android.com/reference/android/animation/ObjectAnimator.html
[3]: http://developer.android.com/reference/android/animation/AnimatorSet.html
[4]: http://developer.android.com/reference/android/view/animation/Animation.html
[5]: http://developer.android.com/guide/topics/resources/animation-resource.html#Tween
[6]: http://developer.android.com/reference/android/graphics/drawable/AnimationDrawable.html