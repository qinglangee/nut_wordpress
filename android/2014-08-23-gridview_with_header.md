# 带header的GridView

[add-a-header-to-a-gridview-android][1]是一个带header的GridView的实现, 需要 API Level 11以 上, 在Level 11以下的, 参照 [getnumcolumns-for-api-8][3] 可以实现兼容的 getNumColumnsCompat() 方法.

	private int getNumColumnsCompat() {
        if (Build.VERSION.SDK_INT >= 11) {
            return getNumColumnsCompat11();

        } else {
            int columns = 0;
            int children = getChildCount();
            if (children > 0) {
                int width = getChildAt(0).getMeasuredWidth();
                if (width > 0) {
                    columns = getWidth() / width;
                }
            }
            return columns > 0 ? columns : AUTO_FIT;
        }
    }

    @TargetApi(Build.VERSION_CODES.HONEYCOMB)
    private int getNumColumnsCompat11() {
        return getNumColumns();
    }

the render of B will after the animation, so the animation will looks more smooth.


refs:  
[add-a-header-to-a-gridview-android][1]  
[HeaderGridView.java][2]  
[getnumcolumns-for-api-8][3]  



[1]: http://stackoverflow.com/questions/13217386/add-a-header-to-a-gridview-android
[2]: https://android.googlesource.com/platform/packages/apps/Gallery2/+/idea133/src/com/android/photos/views/HeaderGridView.java
[3]: http://stackoverflow.com/questions/14879394/getnumcolumns-for-api-8