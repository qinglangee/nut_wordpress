# thread 相关 ps top操作

下面这些操作平时可能不大会用到，但是关键时候却能大显身手，大部分跟 thead 有关。

展开 tid
htop -> F2
ps -p PID -L -o pid,tid,psr,pcpu


特定的 pid, tid 跑在哪些 core 上
1. top -H -p {PID} -> f -> j
2. /proc/{PID}/stat -> 第三列: running/stop，倒数第六列: core


通过 -o 指定需要获取的条目:
ps -eLf/ps aux -L
ps -eLo pid,ppid,lwp,nlwp,osz,rss,ruser,pcpu,stime,etime,args | more
ps -eLo pcpu,args | grep java | sort -k1 -r | awk '{print $1}' | head -n 1
ps ax –no-headings -o user,pid,%cpu,%mem,vsz,sgi_rss
ps axo "user=%u, pid=%p, command line args=%a, elapsed time=%t"
ps axo "Application: %c | CommandlineArgs: %a | PercentageCpu: %C | User: %U | VirtualMemory: %z" –sort vsize  | tail

上面的说了这么多，其实是为了解决下面这个问题，找出 java 中最耗 cpu 的 tid，jstack 追踪。要找出这 tid 方式也有很多种，top，ps 都可以实现。

top -H |head -n 10|grep java|awk '{print $1}'|head -n 1 |sed -r 's/[^0-9].*m//g'
主要注意的是 top -H 直接 grep 出来的有乱码，所以需要通过 sed 处理下，为了这个问题还花了点时间，最后把结果 pipe 到文件，vim 打开才发现了问题。

ps -eLo pcpu,args | grep java | sort -k1 -r | awk '{print $1}' | head -n 1
ps p {PID} -L -o time,pid,tid,pcpu,tname,stat,psr | sort -n -k1 –r
ps 做法会好的多处理起来也更漂亮。

source:
[ps(top) cheatsheet](http://www.udpwork.com/item/13622.html)

ref:
http://stackoverflow.com/questions/1519196/finding-usage-of-resources-cpu-and-memory-by-threads-of-a-process-in-unix-sol
http://stackoverflow.com/questions/8032372/how-can-i-see-which-cpu-core-a-thread-is-running-in
http://stackoverflow.com/questions/3342889/how-to-measure-separate-cpu-core-usage-for-a-process

http://stackoverflow.com/questions/8032372/how-can-i-see-which-cpu-core-a-thread-is-running-in