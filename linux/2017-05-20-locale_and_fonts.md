# linux locale 和　font 设置

## locale 命令
`locale` - get locale-specific information

here is local 的输出:
>LANG=en_US.UTF-8
LANGUAGE=en_US:en
LC_CTYPE=en_US.UTF-8
LC_NUMERIC=zh_CN.UTF-8
LC_TIME=zh_CN.UTF-8
LC_COLLATE="en_US.UTF-8"
LC_MONETARY=zh_CN.UTF-8
LC_MESSAGES="en_US.UTF-8"
LC_PAPER=zh_CN.UTF-8
LC_NAME=zh_CN.UTF-8
LC_ADDRESS=zh_CN.UTF-8
LC_TELEPHONE=zh_CN.UTF-8
LC_MEASUREMENT=zh_CN.UTF-8
LC_IDENTIFICATION=zh_CN.UTF-8
LC_ALL=

locale把按照所涉及到的使用习惯的各个方面分成12个大类，这12个大类分别是： 

1、语言符号及其分类(LC_CTYPE) 
2、数字(LC_NUMERIC) 
3、比较和习惯(LC_COLLATE) 
4、时间显示格式(LC_TIME) 
5、货币单位(LC_MONETARY) 
6、信息主要是提示信息,错误信息,状态信息,标题,标签,按钮和菜单等(LC_MESSAGES) 
7、姓名书写方式(LC_NAME) 
8、地址书写方式(LC_ADDRESS) 
9、电话号码书写方式(LC_TELEPHONE) 
10、度量衡表达方式 (LC_MEASUREMENT) 
11、默认纸张尺寸大小(LC_PAPER) 
12、对locale自身包含信息的概述(LC_IDENTIFICATION)。


`locale -a` 显示所有可用的locale值
`man locale` 查看帮助
The locale command can also be provided with one or more arguments, which are the names  of  locale  key‐
words  (for  example,  date_fmt,  ctype-class-names, yesexpr, or decimal_point) or locale categories (for
example, LC_CTYPE or LC_TIME).  For each argument, the following is displayed:

*  For a locale keyword, the value of that keyword to be displayed.
*  For a locale category, the values of all keywords in that category are displayed.
`locale date_fmt`
`locale LC_TIME`

FILES
`/usr/lib/locale/locale-archive`  Usual default locale archive location.
`/usr/share/i18n/locales`  Usual default path for locale definition files.

## LC_ALL、LANG和LC_*的关系
设定locale就是设定12大类的locale分类属性，即 12个LC_*。除了这12个变量可以设定以外，为了简便起见，还有两个变量： LC_ALL和LANG。它们之间有一个优先级的关系： LC_ALL>LC_*>LANG 可以这么说，LC_ALL是最上级设定或者强制设定，而LANG是默认设定值。
LANG是LC_*的默认值，LC_*变量可以单独设置而可以与LANG不同。而LC_ALL比LC_*的优先级别高，设置完LC_ALL之后，会强制重置LC_*各个值，如果不将LC_ALL重新设置为空，则再无法设置LC_*的单个值 。


## 设置　tty 显示中文　
设置字体
`sudo dpkg-reconfigure console-setup`
按照提示选择字体

安装支持中文的term 
`sudo apt-get install fbterm`
安装好后，tty登录　`Ctrl-Alt-F(1~6)`, `sudo fbterm`

refs:  
[Linux的locale、LC_ALL和LANG](http://www.cnblogs.com/LCcnblogs/p/6208110.html)  
[14.04版本让tty1～6显示中文](http://www.ubuntukylin.com/ukylin/forum.php?mod=viewthread&tid=8519)  


