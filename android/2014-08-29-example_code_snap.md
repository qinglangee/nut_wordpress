# 一些示例代码


## 零散的

### 根据R.color.abc 取颜色

	context.getResources().getColor(R.color.abc);
### 添加点击事件监听

	titleBox.setOnClickListener(new View.OnClickListener() {
		public void onClick(View v) {
			System.out.println(123);
		}
	});
### Bitmap 与 drawable / byte[] 互相转换
1、Bitmap转Drawable

	Bitmap bm=xxx; //xxx根据你的情况获取
	BitmapDrawable bd=BitmapDrawable(bm);
	BtimapDrawable是Drawable的子类，最终直接使用bd对象即可。
2、 Drawable转Bitmap
转成Bitmap对象后，可以将Drawable对象通过Android的SK库存成一个字节输出流，最终还可以保存成为jpg和png的文件。

	Drawable d=xxx; //xxx根据自己的情况获取drawable
	BitmapDrawable bd = (BitmapDrawable) d;
	Bitmap bm = bd.getBitmap();
3、 bitmap -> byte[]

	ByteArrayOutputStream stream = new ByteArrayOutputStream();
	bmp.compress(Bitmap.CompressFormat.PNG, 100, stream);
	byte[] byteArray = stream.toByteArray();
4、 byte[] -> bitmap

	ByteArrayInputStream isBm = new ByteArrayInputStream(byte[]);
    Bitmap bitmap = BitmapFactory.decodeStream(isBm, null, null);
5_ 加载bitmap, *会占用很大内存*

	Bitmap bitmap = BitmapFactory.decodeResource(getResources(), R.drawable.img);
	Bitmap bitmap = BitmapFactory.decodeStream(getResources().openRawResource(R.drawable.img));  // 这个占内存小一些, 但还是比Drawable大
## Theme

### style 设置theme文字颜色

    <!--
        Base application theme, dependent on API level. This theme is replaced
        by AppBaseTheme from res/values-vXX/styles.xml on newer devices.
    -->
    <style name="AppBaseTheme" parent="android:Theme.Light">        <!--
            Theme customizations available in newer API levels can go in
            res/values-vXX/styles.xml, while customizations related to
            backward-compatibility can go here.
        -->
    </style>
    <!-- Application theme. -->
    <!-- All customizations that are NOT specific to a particular API-level can go here. -->
    <style name="AppTheme" parent="AppBaseTheme">        
        <item name="android:textColor">@color/black</item>
    </style>

## Activity

### Activity 全屏

    getWindow().setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN, WindowManager.LayoutParams.FLAG_FULLSCREEN);
### Activity 只能横/竖屏

在AndroidManifest.xml的activity(需要禁止转向的activity)配置中加入`android:screenOrientation="landscape"`属性
代码设置

    setRequestedOrientation(ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE)


## Volley request
string request


        StringRequest stringRequest = new StringRequest(Request.Method.GET, WordApi.PLAN_LIST.url,
                getListResponseListener(), NetUtil.getErrorListener(this));
        VolleyWrapper.getInstance(this).addToRequestQueue(stringRequest);


## View

### 得到 LayoutInflater

    LayoutInflater layoutInflater = LayoutInflater.from(context);  
    LayoutInflater layoutInflater = (LayoutInflater) context.getSystemService(Context.LAYOUT_INFLATER_SERVICE);  

其实第一种就是第二种的简单写法，只是Android给我们做了一下封装而已