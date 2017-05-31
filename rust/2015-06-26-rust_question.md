# rust 问题大杂

## rust   the Book
### 2.1
[文档位置](/usr/local/share/doc/rust)
On Windows, it's in a share/doc directory
### 2.2
[编辑器插件](https://github.com/rust-lang/rust/blob/master/src/etc/CONFIGS.md)  
[编辑器配置](https://github.com/rust-lang/rust/tree/master/src/etc/CONFIGS.md)  

### 4.6

??
怎么 Send 和 Sync 看起来都是线程安全的，是这个意思么？

### 5.2
let x: i32 = diverges();
let x: String = diverges();

x 的值是什么？？

### 5.20 
Inheritance 的实现 可不可以 多个的实现都写在一个里面。

### 5.21
while let 是怎么回事，是一次就break还是好多走到false才break, 代码运行一下看看

### 5.23
看不懂


## rust samples

[7.5.1.3 pointers/ref](http://rustbyexample.com/flow_control/match/destructuring/destructure_pointers.html)  
& ref 有没有的都一样，这页说明了个什么问题？

[7.5.1.4 structs](http://rustbyexample.com/flow_control/match/destructuring/destructure_structures.html)  
说好的一个错误呢，怎么没有了．

[8.1 Methods](http://rustbyexample.com/fn/methods.html)  
Pair.destroy() 挺有意思
[8.2.2 As input parameters](http://rustbyexample.com/fn/closures/input_parameters.html)  
水很深，　再看一遍