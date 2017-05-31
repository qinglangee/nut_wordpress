# 兼容旧版本API的代码

	import android.os.Build.VERSION;
	import android.os.Build.VERSION_CODES;

	if (VERSION.SDK_INT >= VERSION_CODES.GINGERBREAD) {
		editor.apply();
	}else{
		editor.commit();
	}