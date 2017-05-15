# 苹果上的 HOME 和 END 键

Mac osx 上的 home 和 end 键是不能用的，可以用 keybinding 的方法来转换一下。

	cd ~/Library/
	# 如果没有 ~/Library/KeyBindings 目录就新建一个
	mkdir KeyBindings
	cd KeyBindings
	vim DefaultKeyBinding.dict    
编辑dict文件，输入下面内容

	{
	    /* home */
	    "\\UF729"  = "moveToBeginningOfLine:";
	    "$\\UF729" = "moveToBeginningOfLineAndModifySelection:";


	    /* end */
	    "\\UF72B"  = "moveToEndOfLine:";
	    "$\\UF72B" = "moveToEndOfLineAndModifySelection:";


	    /* page up/down */
	    "\\UF72C"  = "pageUp:";
	    "\\UF72D"  = "pageDown:";
	}

按道理说就是这样的，重启你的应用就可以用了。但我试了下，没他娘的鸟用。

## osx 键的表示符号

	Character	Represents
	$	⇧ (shift)
	^	⌃ (control)
	~	⌥ (option)
	@	⌘ (command)
	#	number pad

refs:  
[Mac OS X Home and End Keys](https://www.starryhope.com/mac-os-x-home-and-end-keys/)  
[Key bindings for switchers](http://blog.macromates.com/2005/key-bindings-for-switchers/)  