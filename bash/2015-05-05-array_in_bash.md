# bash 数组

## 一、定义数组
1.使用[]操作符

	names[0]=\'zrong\'
	names[1]=\'jacky\'

2.使用()直接赋值

	names=(\'zrong\' \'jacky\')
	# 或
	names=([0]=\'zrong\' [1]=\'jacky\')
3.使用declare -a定义数组。这种方法可以将一个空的变量定义成数组类型。

	declare -a names
4.从文件中读取数组


	cat>names.txt
	zrong
	jacky
	sweet
	Ctrl+C
	# 将每一行读取为数组的一个元素
	names=(`cat \'names.txt\'`)
## 二、读取数组
1. 数组取值

和ActionScript一样，Bash也使用[]操作符和基于0的下标来取值：

	adobe=(\'Flash\' \'Flex\' \'Photoshop\')
	echo ${adobe[0]}
	# 打印
	# Flash

2. 数组长度（元素个数）

使用“@”这个特殊的下标，可以将数组扩展成列表，然后就可以使用bash中的获取变量长度的操作符“#”来获取数组中元素的个数了：

	adobe=(\'Flash\' \'Flex\' \'Photoshop\')
	echo ${#adobe[@]}
	# 打印
	# 3

有趣的是，没有定义的数组下标，并不会占用数组中元素的个数：

	adobe=([0]=\'Flash\' [2]=\'Flex\' [4]=\'Photoshop\')
	echo ${#adobe[@]}
	# 打印
	# 3

3. 获取数组的一部分

命令替换对数组也是有效的，可以使用偏移操作符来取得数组的一部分：

	adobe=(\'Flash\' \'Flex\' \'Photoshop\' \'Dreamweaver\' \'Premiere\')
	echo ${adobe[@]:1:3}
	# 打印
	# Flex Photoshop Dreamweaver
	echo ${adobe[@]:3}
	# 打印
	# Dreamweaver Premiere

4. 连接两个数组

code

	adobe=(\'Flash\' \'Flex\' \'Photoshop\' \'Dreamweaver\' \'Premiere\')
	adobe2=(\'Fireworks\' \'Illustrator\')
	adobe3=(${adobe[@]} ${adobe2[@]})
	echo ${#adobe3[@]}
	# 打印
	# 7


## 三、修改数组
1. 替换数组元素

模式操作符对数组也是有效的，可以使用它来替换数组中的元素

	adobe=(\'Flash\' \'Flex\' \'Photoshop\' \'Dreamweaver\' \'Premiere\')
	echo ${adobe[@]/Flash/FlashCS5}
	# 打印
	# 注意，打印的结果是一个字符串列表，不是数组
	# FlashCS5 Flex Photoshop Dreamweaver Premiere
	#
	# 将替换后的值重新保存成数组
	adobe=(${adobe[@]/Flash/FlashCS5})

2. 删除数组元素

使用命令替换并重新赋值的方式删除数组元素

	# 删除Photoshop元素
	adobe=(\'Flash\' \'Flex\' \'Photoshop\' \'Dreamweaver\' \'Premiere\')
	adobe=(${adobe[@]:0:2} ${adobe[@]:3})
	echo ${adobe[@]}
	# 打印
	# Flash Flex Dreamweaver Premiere

使用模式操作符删除数组元素

	adobe=(\'Flash\' \'Flex\' \'Photoshop\' \'Dreamweaver\' \'Premiere\')
	adobe=(${adobe[@]/Photoshop/})
	echo ${adobe[@]}
	# 打印
	# Flash Flex Dreamweaver Premiere

## 四、循环

使用for in循环读取数组：

	adobe=(\'Flash\' \'Flex\' \'Photoshop\' \'Dreamweaver\' \'Premiere\')
	for item in ${adobe[@]};do
	    echo $item
	done
	# 打印
	# Flash 
	# Flex 
	# Photoshop 
	# Dreamweaver 
	# Premiere

使用for循环读取数组：

	adobe=(\'Flash\' \'Flex\' \'Photoshop\' \'Dreamweaver\' \'Premiere\')
	len=${#adobe[@]}
	for ((i=0;i<$len;i++));do
	    echo ${adobe[$i]}
	done
	# 打印
	# Flash 
	# Flex 
	# Photoshop 
	# Dreamweaver 
	# Premiere


refs:  
[Bash数组操作教程](http://zengrong.net/post/1518.htm)  