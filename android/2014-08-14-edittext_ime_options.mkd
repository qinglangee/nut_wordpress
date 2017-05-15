# EditText监听回车事件

## 内置输入法
之前遇到的问题没来得及记录下来，趁今晚有空就重新回忆并写下了。

我们在用到EditText这个空间时经常需要重写软键盘中的回车事件以配合我们接下来的响应，比如点击回车变成搜索、发送、完成等。

EditText为我们提供了一个属性imeOptions用来替换软键盘中enter键的外观，如actionDone会使外观变成“完成”。

下面列出比较经常用到的几个属性以及替换的文本外观：

	　　actionUnspecified        未指定         EditorInfo.IME_ACTION_UNSPECIFIED.  
	　　actionNone                 动作            EditorInfo.IME_ACTION_NONE 
	　　actionGo                    去往            EditorInfo.IME_ACTION_GO
	　　actionSearch               搜索            EditorInfo.IME_ACTION_SEARCH    
	　　actionSend                 发送            EditorInfo.IME_ACTION_SEND   
	　　actionNext                下一项           EditorInfo.IME_ACTION_NEXT   
	　　actionDone               完成              EditorInfo.IME_ACTION_DONE 

设置的方法可以在布局文件中设置 `android:imeOptions="actionNext"` 或者在代码中 `mUserEdit.setImeOptions(EditorInfo.IME_ACTION_NEXT);`

接下来就需要重写回车事件了，通过setOnEditorActionListener

	private void initListener() {
		mUserEdit .setOnEditorActionListener(new TextView.OnEditorActionListener() {
			public boolean onEditorAction(TextView v, int actionId, KeyEvent event) {
				if (actionId == EditorInfo.IME_ACTION_SEND || (event != null && event.getKeyCode() == KeyEvent.KEYCODE_ENTER)) {
					//让mPasswordEdit获取输入焦点
					mPasswordEdit.requestFocus();
					return true;
				}
				return false;
			}
		});
	}

到此重写回车事件就完成了。

## 非内置输入法

	password = (EditText) findViewById(R.id.login_password_edit);
	password.setOnKeyListener(new OnKeyListener() {

		@Override
		public boolean onKey(View v, int keyCode, KeyEvent event) {
			if (KeyEvent.KEYCODE_ENTER == keyCode && event.getAction() == KeyEvent.ACTION_DOWN) {
				login();
				return true;
			}
			return false;

		}
	});



 

## edittext属性
下面顺便列出几个edittext常用的属性：

	android:password="true"  这条可以让EditText显示的内容自动为星号，输入时内容会在1秒内变成*字样。

	android:numeric="true" 这条可以让输入法自动变为数字输入键盘，同时仅允许0-9的数字输入

	android:capitalize="abcde" 这样仅允许接受输入abcde，一般用于密码验证

	android:hint="密码"  设置显示的提示信息

	android:singleLine="true"  设置单行输入，这样就不会自动换行



[Android 重写EditText回车事件][1]  
[android EditText 回车事件][2]  
[EditorInfo][3]  



[1]: http://www.cnblogs.com/kkrimen/p/3414849.html
[2]: http://dingbuoyi.iteye.com/blog/1460807
[3]: https://developer.android.com/reference/android/view/inputmethod/EditorInfo.html 