# 动态设置GridView高度

## GridView放在scrollView中
让GridView与内容长度一样, ScrollView来控制滚动  
继承GridView,重写 onMeasure 方法

	public class MyGridView extends GridView {

		public MyGridView(Context context, AttributeSet attrs) {
		    super(context, attrs);
		}

		public MyGridView(Context context) {
		    super(context);
		}

		public MyGridView(Context context, AttributeSet attrs, int defStyle) {
		    super(context, attrs, defStyle);
		}

		@Override
		public void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
		    int expandSpec = MeasureSpec.makeMeasureSpec(Integer.MAX_VALUE >> 2,
		            MeasureSpec.AT_MOST);
		    super.onMeasure(widthMeasureSpec, expandSpec);
		}
	}

*注意点*
这种用法显示很多图片的话会内存爆掉的


talk about this   
[how-to-make-the-height-of-a-gridview-wrap-its-content][1]  
[grid-of-images-inside-scrollview][2]  
[gridview-height-gets-cut][3]  

another solution:
[GridView with header and footer][4]

[1]: http://www.jayway.com/2012/10/04/how-to-make-the-height-of-a-gridview-wrap-its-content/
[2]: http://stackoverflow.com/questions/4523609/grid-of-images-inside-scrollview/4536955#4536955
[3]: http://stackoverflow.com/questions/8481844/gridview-height-gets-cut/8483078#8483078
[4]: https://github.com/SergeyBurish/HFGridView