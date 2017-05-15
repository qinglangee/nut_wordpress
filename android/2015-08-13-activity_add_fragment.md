# activity 中 replace() 添加 fragment
在 activity 中添加 fragment时候遇到了一个问题，如果act被系统回收的，再回到这个应用时，fragment调用getActivity返回null，该fragement无法显示. 

因为 fragment是在 activity 的 onCreate() 方法中被添加的, 所以被系统回收的 activity 在恢复时会重新执行 onCreate() 方法, 重新建一个 fragment.  
通过日志调试发现 fragment 的 onCreateView() 方法会调用两遍. 因为系统恢复时也会重建原来的 fragment , 原来的 fragment 被 replace 后, getActivity() 就会返回 null. 
与 getActivity() 相关的调用都会报空指针异常.


所以 FragmentManager 中 用 replace() 添加 fragment 时, 要先查找以前有没有, 没有再添加新的.

add() 与 replace() 方法类似, 下面是 replace() 方法的示例代码.

	public void changeFragment(Fragment fragArg, boolean addToBackStack, String tag) {
        FragmentManager manager = getSupportFragmentManager();
        Fragment frag = null;
        if(tag != null){
            frag = manager.findFragmentByTag(tag);
        }
        if (frag == null) {
            frag = fragArg;
		}
        if (frag == null) {
			return;
		}
		FragmentTransaction transaction = manager.beginTransaction();

		transaction.replace(R.id.viewer, frag, tag);
		if (addToBackStack) {
			transaction.addToBackStack(null);
		}

		transaction.commit();
	}





refs:  
[android fragment getActivity() null ](http://blog.csdn.net/u013942461/article/details/20645847)  