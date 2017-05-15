# Unhandled event loop exception

## 原因一
pom.xml 编辑器报错

>Unhandled event loop exception
>org.eclipse.swt.SWTError: Item not added
>	at org.eclipse.swt.SWT.error(SWT.java:4517)
>	at org.eclipse.swt.SWT.error(SWT.java:4406)
>	at org.eclipse.swt.SWT.error(SWT.java:4377)


给pom.xml换个默认编辑器就好了，
## 原因二
看看是不是其它特定文件编辑时报错， 换个默认编辑器试试