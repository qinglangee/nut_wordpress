# java heap size

##  Java Heap Size
程序运行产生的对象占用的内存， 超出会报 java.lang.OutOfMemoryError: Java heap space.

Heap sizes 的默认值
初始值是物理内存的 1/64, 最大 1 G
最大值是物理内存的 1/4, 最大1G

运行时设置 heap 值

	$ java -Xms512m -Xmx1024m JavaApp

##  Perm Gen Size
加载的类定义和元数据占用的内存。 超出会报 Java.Lang.OutOfMemoryError: PermGen  
运行时设置

	$ java -XX:PermSize=64m -XX:MaxPermSize=128m JavaApp

## Java Stack Size

设置值

	$ java -Xss512k JavaApp


## 在系统中查看这些值

linux 

	$ java -XX:+PrintFlagsFinal -version | grep -iE 'HeapSize|PermSize|ThreadStackSize'
mac

	$ java -XX:+PrintFlagsFinal -version | grep -iE 'heapsize|permsize|threadstacksize'
windows

	C:\>java -XX:+PrintFlagsFinal -version | findstr /i "HeapSize PermSize ThreadStackSize"



refs:  

[Find out your Java heap memory size](http://www.mkyong.com/java/find-out-your-java-heap-memory-size/)  
