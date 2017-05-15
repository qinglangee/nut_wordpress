# java 文档解析相关的库

## apache poi 项目概况

apache POI 项目是用来读微软格式文件的库。

POIFS  是基础类库，读 xls  doc 的库基本都用到它。  

HSSF   Excel 97-2007   
XSSF   Excel  2007+    OOXML (.xlsx)  格式的  
SXSSF (Since POI 3.8 beta3)    

HWPF   Word  97-2003
XWPF   Word  2007+      OOXML 格式

HSLF   PowerPoint  97-2003
XSLF   PowerPoint  2007+      OOXML 格式

HPSF   读属性的子类库

## itext  itext-rtf
itext 现在专注于解析 pdf,  itex-rtf 最高版本 2.1.7 

### rtf
itext-rtf 2.1.7 需要配合 itext-2.1.7 使用，因为需要 `com.lowagie.text.Document` .

[api 文档][1],  [一些例子][2] , 可是例子打不开了





refs:  
[Apache POI - the Java API for Microsoft Documents](http://poi.apache.org/)  
[Java API to Handle Microsoft Word Files](http://poi.apache.org/document/index.html)  


[the POIFS project page ](http://poi.apache.org/poifs/index.html)  
[POI-HSSF and POI-XSSF - Java API To Access Microsoft Excel Format Files](http://poi.apache.org/spreadsheet/index.html)  
[rtf文档格式解释](http://blog.csdn.net/a3729291988/article/details/8144883)  





[1]: http://www.docjar.com/docs/api/com/lowagie/text/rtf/
[2]: http://www.ujihara.jp/iTextdotNET/ja/tutorial/rtf/index.html