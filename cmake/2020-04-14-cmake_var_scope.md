# cmake 变量范围

1、两种变量的定义参考

Normal Variables

通过 `set(<variable> <value>... [PARENT_SCOPE])`这个命令来设置的变量就是 Normal Variables。例如 set(MY_VAL "666") ，此时 MY_VAL 变量的值就是 666。

Cache Variables

通过 `set(<variable> <value>... CACHE <type> <docstring> [FORCE])`这个命令来设置的变量就是 Cache Variables 。 

相当于一个全局变量，我们在同一个 cmake 工程中都可以使用。

CMake 规定，有一个与 Cache 变量同名的 Normal 变量出现时，后面使用这个变量的值都是以 Normal 为准，如果没有同名的 Normal 变量，CMake 才会自动使用 Cache 变量。

## 子目录
Normal 变量的作用域就是以 CMakeLists.txt 文件为基本单元。

子目录 CMake 文件会拷贝一份父目录文件的 Normal 变量。
需要说明的是，我们在子目录中如果想要修改父目录 CMake 文件包含的 Normal 变量。必须通过 `set(... PARENT_SCOPE)` 的方式。 这只会修改父目录的变量，不会修改子目录的变量。 

对于 function() 而言，因为函数定义可以是在其他 .cmake 模块文件中定义的。也可以在其他 CMakeLists.txt 文件中调用，因此准确的说，function的父目录应该是『调用函数的地方所属的 CMakeLists.txt 』

通过 include() 和 macro() 相当于把这两部分包含的代码直接加入根目录 CMakeLists.txt 文件中去执行，相当于他们是一个整体。因此变量直接都是互通的。







refs:  
[CMake 两种变量原理](https://www.cnblogs.com/ncuneugcj/p/9756324.html)  