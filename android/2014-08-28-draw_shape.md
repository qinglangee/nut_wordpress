# 画各种图形

## 方框

    <?xml version="1.0" encoding="utf-8"?>
    <!-- border_main颜色的边框，四个角是直角 -->
    <shape xmlns:android="http://schemas.android.com/apk/res/android" >
        <stroke
            android:width="1dp"
            android:color="@color/border_main" />
         <solid android:color="@color/bg_main"/>
        <padding
            android:bottom="1dp"
            android:left="1dp"
            android:right="1dp"
            android:top="1dp" />
    </shape>

## 线条

    <View
            android:layout_width="fill_parent"
            android:layout_height="1dp"
            android:background="@color/border_separator"
             />
## 画两个图形  [stackoverflow][1] 

    <?xml version="1.0" encoding="utf-8"?>
    <!-- 用户时间轴背景 -->
    <layer-list xmlns:android="http://schemas.android.com/apk/res/android">

        <item>
            <shape android:shape="rectangle" >
                <solid android:color="@color/white" />
            </shape>
        </item>

        <item android:top="-2dp" android:right="-2dp" android:left="67dp" android:bottom="-2dp">
            <shape>
                <solid android:color="@android:color/border_separator_in_light" />
                <stroke
                    android:dashGap="10px"
                    android:dashWidth="10px"
                    android:width="1dp"
                    android:color="@color/red" />
            </shape>
        </item>

    </layer-list>

refs:  
[官方文档](http://developer.android.com/guide/topics/resources/drawable-resource.html#Shape)  
[民间文档](http://idunnolol.com/android/drawables.html)  
[中文例子](http://blog.csdn.net/ygc87/article/details/7673587)  





[1]: http://stackoverflow.com/questions/19238738/android-shape-with-bottom-stroke
