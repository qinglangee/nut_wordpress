# jquery 选择 a 标签 点击

发现直接trigger或者click都不行，后来有印象之前用[0]的时候可以点击，测试了下可以的，记录下来。

	// 直接调用浏览器中 html 元素的click事件
	$('a.next')[0].click();


jquery 直接用 a 的 点击事件会无效


一开始还以为是浏览器做了相应的安全措施，屏蔽了JS对A标签的操作，后来发现，并不是这样的，接下来就说说其中的原委。

在开始解释前，我先抛出一个问题。在我们点击“A标签”的时候，究竟是点击了什么才发生的跳转？

1）点击的是“A标签”本身？

2）点击的是“A标签”中显示的文字？

说到这里，大家应该明白了，我们上边的代码已经证实了点击A标签本身，并不会触发跳转到指定链接的事件，就是说，我们平时都是点击的A标签中的文字了？

	 <html>
	<head>磨途歌-A标签测试2<head>
	<body>
	   <a href="http://www.mo2g.com">磨途歌<a>
	</body>
	</html>
	<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js"><script>
	<script>
	jQuery(function($) {
	  var mo2g = '<span id="mo2g">磨延城<span>';
	  //给A标签中的文字添加一个能被jQuery捕获的元素
	  $('a').append(mo2g);
	  //模拟点击A标签中的文字
	  $('#mo2g').click();
	});
	</script>



这下效果出来了，事实证明了上述的推断是正确的，所以要想用JS模拟点击A标签事件，就得先往A标签中的文字添加能被JS捕获的元素，然后再用JS模拟点击该元素即可。

以上就是本文讲诉的相关jQuery中$("a").click()无效问题的分析了，希望小伙伴们能够喜欢。


refs:  
[jQuery中$.click()无效问题分析](http://www.jb51.net/article/60538.htm)  