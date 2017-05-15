# webview 相关小内容
在加载完成后执行js, 比如　替换所有　link. ref: [disabling-links-in-android-webview][1], [modify-a-webpages-dom][2]  

	public class WebClient extends WebViewClient {
	    @Override
	    public boolean shouldOverrideUrlLoading(WebView view, String url) {
	        return true;
	    }

	    @Override
	    public void onPageFinished(WebView view, String url) 
	    {       
	        view.loadUrl("javascript:document.body.innerHTML = document.body.innerHTML.replace(/<a.*href=/gi,'<a href=\"#\" _url=');");
	    }
	}

执行函数

	view.loadUrl("javascript:(function() { "
            + "document.getElementsByClassName('signin-card')[0].style.width = 'auto';" + "})()");
            
也[有些人][3]说这个只能在本地html上执行，　加载 google.com　就不执行了．
refs:  
[disabling-links-in-android-webview][1]  
[modify-a-webpages-dom][2]    
[android-load-and-execute-javascript-on-external-webpage][3]  



[1]: http://stackoverflow.com/questions/7416142/disabling-links-in-android-webview
[2]: http://stackoverflow.com/questions/2219074/in-android-webview-am-i-able-to-modify-a-webpages-dom
[3]: http://stackoverflow.com/questions/7309123/android-load-and-execute-javascript-on-external-webpage