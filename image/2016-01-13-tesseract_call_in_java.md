# java 调用 tesseract

java使用[tess4j][1]调用 tesseract api.


	public static void example() {
		File imageFile = new File("test.gif");
		ITesseract instance = new Tesseract();

		try {
			String result = instance.doOCR(imageFile);
			System.out.println(result);
		} catch (TesseractException e) {
			e.printStackTrace();
		}
	}

主要是报错

1. jna  cannot open shared object file: No such file or directory

*解决方法，设置一下链接库路径*

    vim /etc/profile
在export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE INPUTRC下面加入  

    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:${你的so目录}
    # 有个命令叫 ldconfig， 不知是不是干这个事的。（ ldconfig 需要把 *.so 所在目录添加到 /etc/ld.so.conf 配置文件中）

2. Error opening data file ./tessdata/eng.traineddata

>Error opening data file ./tessdata/eng.traineddata
Please make sure the TESSDATA_PREFIX environment variable is set to the parent directory of your "tessdata" directory.
Failed loading language 'eng'
Tesseract couldn't load any languages!


找不到 tessdata目录,程序中打印 TESSDATA_PREFIX 设置是对的， 还是报这个错。

	// 可以在代码中设置数据目录位置  
	instance.setDatapath("datapath");




[1]:   https://github.com/nguyenq/tess4j