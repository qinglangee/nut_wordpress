# python date处理

## 模块
```
# -*- coding: utf-8 -*-
import datetime
```
*下面 date 是指 datetime.date ,datetime 也是 datetime.datetime*

`today = date.today()`：返回一个表示当前本地日期的date对象；  
`mydate = date(2012,9,17)` 获得一个指定日期  

`mydate.isoformat()`：返回格式如'YYYY-MM-DD’的字符串；
`mydate.strftime(fmt)`：自定义格式化字符串。在下面详细讲解。


`datetime.utcnow()`：返回一个当前utc时间的datetime对象；
`now = datetime.now([tz])`：返回一个表示当前本地时间的datetime对象，如果提供了参数tz，则获取tz参数所指时区的本地时间；
`datetime.strptime(date_string, format)`：将格式字符串转换为datetime对象；
`time.mktime(now.timetuple())`: 把时间转换为unix时间戳
`datetime.strftime(format)` 


datetime、date、time都提供了strftime()方法， 该方法接收一个格式字符串， 输出日期时间的字符串表示。 下表是从python手册中拉过来的， 我对些进行了简单的翻译（翻译的有点噢口~~）。

格式字符  意义
```
	%a 星期的简写。如 星期三为Web
	%A 星期的全写。如 星期三为Wednesday
	%b 月份的简写。如4月份为Apr
	%B月份的全写。如4月份为April 
	%c:  日期时间的字符串表示。（如： 04/07/10 10:43:39）
	%d:  日在这个月中的天数（是这个月的第几天）
	%f:  微秒（范围[0,999999]）
	%H:  小时（24小时制，[0, 23]）
	%I:  小时（12小时制，[0, 11]）
	%j:  日在年中的天数 [001,366]（是当年的第几天）
	%m:  月份（[01,12]）
	%M:  分钟（[00,59]）
	%p:  AM或者PM
	%S:  秒（范围为[00,61]，为什么不是[00, 59]，参考python手册~_~）
	%U:  周在当年的周数当年的第几周），星期天作为周的第一天
	%w:  今天在这周的天数，范围为[0, 6]，6表示星期天
	%W:  周在当年的周数（是当年的第几周），星期一作为周的第一天
	%x:  日期字符串（如：04/07/10）
	%X:  时间字符串（如：10:43:39）
	%y:  2个数字表示的年份
	%Y:  4个数字表示的年份
	%z:  与utc时间的间隔 （如果是本地时间，返回空字符串）
	%Z:  时区名称（如果是本地时间，返回空字符串）
	%%:  %% => %

    dt = datetime.now()  
    print   '(%Y-%m-%d %H:%M:%S %f): ' , dt.strftime( '%Y-%m-%d %H:%M:%S %f' )  
    print   '(%Y-%m-%d %H:%M:%S %p): ' , dt.strftime( '%y-%m-%d %I:%M:%S %p' )  
    print   '%%a: %s '  % dt.strftime( '%a' )  
    print   '%%A: %s '  % dt.strftime( '%A' )  
    print   '%%b: %s '  % dt.strftime( '%b' )  
    print   '%%B: %s '  % dt.strftime( '%B' )  
    print   '日期时间%%c: %s '  % dt.strftime( '%c' )  
    print   '日期%%x：%s '  % dt.strftime( '%x' )  
    print   '时间%%X：%s '  % dt.strftime( '%X' )  
    print   '今天是这周的第%s天 '  % dt.strftime( '%w' )  
    print   '今天是今年的第%s天 '  % dt.strftime( '%j' )  
    print   '今周是今年的第%s周 '  % dt.strftime( '%U' )  
      
    # # ---- 结果 ----   
    # (%Y-%m-%d %H:%M:%S %f):  2010-04-07 10:52:18 937000   
    # (%Y-%m-%d %H:%M:%S %p):  10-04-07 10:52:18 AM   
    # %a: Wed    
    # %A: Wednesday    
    # %b: Apr    
    # %B: April    
    # 日期时间%c: 04/07/10 10:52:18    
    # 日期%x：04/07/10    
    # 时间%X：10:52:18    
    # 今天是这周的第3天    
    # 今天是今年的第097天    
    # 今周是今年的第14周   
```



refs:  
[python datetime处理时间](http://www.cnblogs.com/lhj588/archive/2012/04/23/2466653.html)  
[python时间处理之date ](http://blog.csdn.net/wirelessqa/article/details/7973113)  