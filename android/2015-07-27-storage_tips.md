# android 存储

## 应用数据缓存位置
其实DiskLruCache并没有限制数据的缓存位置，可以自由地进行设定，但是通常情况下多数应用程序都会将缓存的位置选择为 /sdcard/Android/data/<application package>/cache 这个路径。选择在这个位置有两点好处：第一，这是存储在SD卡上的，因此即使缓存再多的数据也不会对手机的内置存储空间有任何影响，只要SD卡空间足够就行。第二，这个路径被Android系统认定为应用程序的缓存路径，当程序被卸载的时候，这里的数据也会一起被清除掉，这样就不会出现删除程序之后手机上还有很多残留数据的问题。[Android DiskLruCache完全解析，硬盘缓存的最佳方案 ][1]
## 查看应用可用内存
我们可以通过下面的代码看出每个应用程序最高可用内存是多少。[高效加载大图片][2]
[java] view plaincopy

    int maxMemory = (int) (Runtime.getRuntime().maxMemory() / 1024);  
    Log.d("TAG", "Max memory is " + maxMemory + "KB");





[1]: http://blog.csdn.net/sinyu890807/article/details/28863651
[2]: http://blog.csdn.net/guolin_blog/article/details/9316683