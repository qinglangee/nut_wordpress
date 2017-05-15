# java 资源的编码

测试平台 windows7 中文版 ， 两个测试文件 
gbk.java, 保存为 ANSI 编码，在windows 中文系统中应该就是 GBK

	public class gbk{
		public static void main(String[] args) {
			System.out.println("gbk 这里是中文  " + System.getProperty("file.encoding"));
		}
	}
utf.java, 保存为 utf-8 编码

	public class utf{
		public static void main(String[] args) {
			System.out.println("utf  这里是中文  " + System.getProperty("file.encoding"));
		}
	}

## 编译

在windows 中文系统中，系统默认编码是 GBK, 所以 `javac gbk.java` 正常， `javac utf.java` 就会报错  
>utf.java:5: 错误: 编码GBK的不可映射字符
  System.out.println("utf  杩欓噷鏄腑鏂?  " + System.getProperty("file.encoding"));

在 javac 中加入编码 utf-8,  `javac -encoding utf8 utf.java` 正常，`javac -encoding utf8 gbk.java` 报错
>gbk.java:3: 错误: 编码utf8的不可映射字符
 System.out.println("gbk ??????????  " + System.getProperty("file.encoding")); 

## 执行
上面编译成功的 class, java 不带参数执行都正常输出中文， 但 file.encoding 都是GBK. 如果指定了 file.encoding=gbk 也是正常输出。不管 file.encoding 指定为什么值，都正常输出。
*file.encoding这不就没什么用了么？？？？？？？？*
`java gbk` 
>gbk 这里是中文  GBK

`java -Dfile.encoding=gbk utf` ->
>utf  这里是中文  gbk

`java -Dfile.encoding=utf8 utf` ->
>utf  这里是中文  utf8

## file.encoding 的作用
在windows 下使用 git bash 时， 因为中文 windows java 默认 file.encoding 是 gbk, git bash 默认编码是 utf8, `java` 命令输出的 帮助是乱码， 这时 使用 `java -Dfile.encoding=utf8` 可以输出正常不乱码的帮助.
执行程序时读入文件的编码也由 -Dfile.encoding 来控制

*javac 的参数指定编译时输入输出的编码， java 的参数控制执行时输入输出*