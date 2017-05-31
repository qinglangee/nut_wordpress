# 报错  Failed while installing JAX-RS (REST Web Services) 1.1.

## 解决方式  
1. 不理它
2. web.xml中 web-app节点的内容全删掉, 导入后再恢复

## 具体查看原因
在Error log面板中双击错误打开详细信息, Failed while installing JAX-RS 错误的具体信息可能有很多种

###  web.xml格式, 之前格式是下面这样的
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE web-app PUBLIC "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN" "http://java.sun.com/xml/ns/javaee 
    http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">
<web-app version="2.5" 
    xmlns="http://java.sun.com/xml/ns/javaee" 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
    http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd">

    <listener>  
        <listener-class>com.l99.web.WwereStartListener</listener-class>  
    </listener> 
</web-app>
```
可能报的错误有:
* Caused by: org.xml.sax.SAXParseException: The markup declarations contained or pointed to by the document type declaration must be well-formed.
* Caused by: java.net.MalformedURLException: Illegal character in URL

把`<!DOCTYPE .....>` 这个元素删掉就可以了

###  org.eclipse.emf.ecore.xmi.FeatureNotFoundException 

    Caused by: org.eclipse.emf.ecore.xmi.FeatureNotFoundException: Feature 'listener' not found. (platform:/resource/abc/src/main/webapp/WEB-INF/web.xml, 8, 12)
    Caused by: org.eclipse.emf.ecore.xmi.FeatureNotFoundException: Feature 'welcome-file-list' not found. (platform:/resource/abc/src/main/webapp/WEB-INF/web.xml, 8, 22)

等等各种,没找到好的解决办法  
避免的方法: 

    Window->Preferences->Maven->Java EE Integration->Select active Java EE configurators , 把勾全去掉就行了
