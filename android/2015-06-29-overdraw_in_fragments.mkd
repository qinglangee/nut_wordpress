# Overdraw in fragments

添加　fragment时如果用的是add, 不是 replace, 后添加的 fragment会　覆盖到先前的 fragment 的上面．
http://stackoverflow.com/q/16771293/3410697

一个快速的解决方式是给后添加的 fragment　添加 background ,　但这就会造成 overdraw.

避免这个问题的一个方法是，在添加　fragment 的 transaction 中把先前的 fragment 隐藏．

	Fragment currentFragment;
	FragmentTransaction transaction = getFragmentManager().beginTransaction();
	transaction.add(R.id.container, new Fragment2());
	if ((currentFragment = getFragmentManager().findFragmentById(R.id.container)) != null) {
	    transaction.hide(currentFragment);
	}
	transaction.commit();

有时 fragment 的背景与原来的 windowBackground 不同，　需要有新的背景，可以把　windowBackground 去掉．

	getActivity().getWindow().setBackgroundDrawable(null);
但是这样当　fragment detach　时，　windowBackground　不会自动回来．　可以用下面的方法获取　windowBackground．

	public static Drawable getWindowBackground(Context context) {
	    TypedValue typedValue = new TypedValue();
	    Drawable drawable;
	    context.getTheme().resolveAttribute(android.R.attr.windowBackground, typedValue, true);
	    if (typedValue.type >= TypedValue.TYPE_FIRST_COLOR_INT && typedValue.type <= TypedValue.TYPE_LAST_COLOR_INT) {
	        drawable = new ColorDrawable(typedValue.data);
	    } else {
	        drawable = context.getResources().getDrawable(typedValue.resourceId);
	    }
	    return drawable;
	}
然后在　fragment　的 onDetach() 方法中调用它．

	getActivity().getWindow().setBackgroundDrawable(Utils.getWindowBackground(getActivity()));

refs:  
[Overdraw in fragments](http://androidshenanigans.blogspot.jp/2015/03/overdraw-in-fragments.html)  