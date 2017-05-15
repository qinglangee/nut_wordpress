# Idea 模板设置
在　IntelliJ Idea中也可以像Eclipse 中那样设置代码模板，　打开菜单　Settings->LiveTemplates

需要自己指定应用的上下文, 变量内容也需要自己指定．
$END$ 和 $SELECTION$ 是两个预定义的变量，分别指定光标位置和选中的内容
## Java Templates

	public void test(){
	 $end$
	}
	public static void main(String[] args) {
	    $CLASS_NAME$ t = new $CLASS_NAME$();
	    t.test();
	}

## Android Templates
Button

	<Button
	    android:id="@+id/$id$"
	    android:layout_width="wrap_content"
	    android:layout_height="wrap_content"
	    android:text="$End$" />