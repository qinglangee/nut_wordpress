# C++ 多线程问题
系列讲座：  
[秒杀多线程第一篇 多线程笔试面试题汇总 ][1]  
[秒杀多线程第二篇 多线程第一次亲密接触 CreateThread与_beginthreadex本质区别][2]  
[秒杀多线程第三篇 原子操作 Interlocked系列函数][3]  
[秒杀多线程第四篇 一个经典的多线程同步问题][4]  
[秒杀多线程第五篇 经典线程同步 关键段CS][5]  
[秒杀多线程第六篇 经典线程同步 事件Event][6]  
[秒杀多线程第七篇 经典线程同步 互斥量Mutex][7]  
[秒杀多线程第八篇 经典线程同步 信号量Semaphore][8]  
[秒杀多线程第九篇 经典线程同步总结 关键段 事件 互斥量 信号量][9]  
[秒杀多线程第十篇 生产者消费者问题][10]  
[秒杀多线程第十一篇 读者写者问题][11]  
[秒杀多线程第十二篇 多线程同步内功心法——PV操作上][12]  
[][13]  
[秒杀多线程第十四篇 读者写者问题继 读写锁SRWLock][14]  
[][15]  

C++11 之后有了标准线程库，有空可以研究一下  
`#include <thread>`  
[C++多线程类Thread（C++11）][16]  
[C++11多线程(简约但不简单)][17]  
[C++11 并发与多线程（一）][18]  

## 讲座1
多线程面试题，啊   不会做

## 讲座2 多线程第一次亲密接触 
CreateThread 与 `_beginthreadex`本质区别  

CreateThread 是 windows 提供的 API, 
`_beginthreadex` 是 C++ 对API的包装，内部做了一些线程数据块与线程绑定的动作。 

## 讲座3 原子操作 
Interlocked系列函数

## 讲座4 一个经典的多线程同步问题
多线程问题的错误实现

## 讲座5 经典线程同步 关键段CS
CRITICAL_SECTION  

最后总结下关键段：
1．关键段共初始化化、销毁、进入和离开关键区域四个函数。
2．关键段可以解决线程的互斥问题，但因为具有“线程所有权”，所以无法解决同步问题。
3．推荐关键段与旋转锁配合使用。

## 讲座6 经典线程同步 事件Event
事件Event实际上是个内核对象，它的使用非常方便。  

最后总结下事件Event：
1．事件是内核对象，事件分为手动置位事件和自动置位事件。事件Event内部它包含一个使用计数（所有内核对象都有），一个布尔值表示是手动置位事件还是自动置位事件，另一个布尔值用来表示事件有无触发。
2．事件可以由SetEvent()来触发，由ResetEvent()来设成未触发。还可以由PulseEvent()来发出一个事件脉冲。
3．事件可以解决线程间同步问题，因此也能解决互斥问题。

## 讲座７ 经典线程同步 互斥量Mutex
互斥量常用于多进程之间的线程互斥

互斥量也是一个内核对象，它用来确保一个线程独占一个资源的访问。互斥量与关键段的行为非常相似，并且互斥量可以用于不同进程中的线程互斥访问资源。
与关键段类似，互斥量也是不能解决线程间的同步问题。
由于互斥量常用于多进程之间的线程互斥，所以它比关键段还多一个很有用的特性——“遗弃”情况的处理。比如有一个占用互斥量的线程在调用ReleaseMutex()触发互斥量前就意外终止了（相当于该互斥量被“遗弃”了），那么所有等待这个互斥量的线程是否会由于该互斥量无法被触发而陷入一个无穷的等待过程中了？这显然不合理。因为占用某个互斥量的线程既然终止了那足以证明它不再使用被该互斥量保护的资源，所以这些资源完全并且应当被其它线程来使用。因此在这种“遗弃”情况下，系统自动把该互斥量内部的线程ID设置为0，并将它的递归计数器复置为0.


最后总结下互斥量Mutex：

1．互斥量是内核对象，它与关键段都有“线程所有权”所以不能用于线程的同步。

2．互斥量能够用于多个进程之间线程互斥问题，并且能完美的解决某进程意外终止所造成的“遗弃”问题。

## 讲座8 经典线程同步 信号量Semaphore

## 讲座9 经典线程同步总结 
关键段 事件 互斥量 信号量

## 讲座10 生产者消费者问题

## 讲座11 读者写者问题

## 讲座12 多线程同步内功心法——PV操作上

## 讲座13 

## 讲座14 讲座14 读者写者问题继 读写锁SRWLock
最后总结一下读写锁SRWLock

1．读写锁声明后要初始化，但不用销毁，系统会自动清理读写锁。

2．读取者和写入者分别调用不同的申请函数和释放函数。

## 讲座15 


refs:  



[1]: https://blog.csdn.net/MoreWindows/article/details/7392749
[2]: https://blog.csdn.net/morewindows/article/details/7421759
[3]: https://blog.csdn.net/morewindows/article/details/7429155
[4]: http://blog.csdn.net/morewindows/article/details/7442333
[5]: https://blog.csdn.net/morewindows/article/details/7442639
[6]: https://blog.csdn.net/morewindows/article/details/7445233
[7]: https://blog.csdn.net/morewindows/article/details/7470936
[8]: https://blog.csdn.net/morewindows/article/details/7481609
[9]: https://blog.csdn.net/morewindows/article/details/7538247
[10]: https://blog.csdn.net/morewindows/article/details/7577591
[11]: https://blog.csdn.net/morewindows/article/details/7596034
[12]: https://blog.csdn.net/morewindows/article/details/7650470
[13]: https://
[14]: https://blog.csdn.net/morewindows/article/details/7650574
[15]: 
[16]: https://blog.csdn.net/ouyangfushu/article/details/80199140
[17]: https://www.jianshu.com/p/dcce068ee32b
[18]: https://blog.csdn.net/qiuyoujie/article/details/79175985