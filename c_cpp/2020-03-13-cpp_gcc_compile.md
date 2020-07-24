# 使用 gcc 编译 c++ 
编译C++文件时需要用 g++ 命令, 编译 C 文件时用 gcc 
gcc/g++ 常用选项
```
-v              查看版本
-o              产生目标文件
-I+目录         指定头文件目录
-D              编译时定义宏
-00/-01/-03     没有优化/缺省值/优化级别最高
-Wall           提示更多警告信息
-c              只编译子程序
-E              生成预处理文件
-g              包含调试信息
-E                       Preprocess only; do not compile, assemble or link.
-S                       Compile only; do not assemble or link.
-c                       Compile and assemble, but do not link.
```

静态与动态库
目标文件 静态库文件 动态库文件
windows   `*.obj *.lib  *.dll`
linux   `*.o  lib*.a  lib*.so`
静态库(.lib .a)可以看做是一组目标文件(.obj .o)的集合，在链接打包时一起打包到可执行文件中。 

## 最基础
编译出 a.exe 文件
`g++ source.cpp`   
指定输出文件名
`g++ -o test source.cpp`


## 编译静态库与动态库
https://blog.csdn.net/daidaihema/article/details/80902012  
这个主要是 linux 平台下的。

目录结构
```
./main.cpp
./src
./src/add.cpp
./src/div.cpp
./src/mul.cpp
./src/sub.cpp
./include
./include/add.h
./include/head.h
./lib
```

### 无库编译
` g++  src/*.cpp main.cpp  -Iinclude `
1. 一编译时，把需要的源文件在命令行上都指出就可以。 .h 头文件与 cpp 文件不是很密切的关系，只是声明，多个cpp 合到一个h 文件也没问题，直接在main.cpp里自己写也可以。

### 编译静态库
第一步：得到*.o文件。 进入 src 目录  `gcc *.cpp -c -I../include`   得到
第二步：创建静态库  
```
ar rcs libMyTest.a *.o        将所有.o文件打包为静态库，r将文件插入静态库中，c创建静态库，不管库是否存在，s写入一个目标文件索引到库中，或者更新一个存在的目标文件索引。
mv libMyTest.a ../lib         将静态库文件放置lib文件夹下
nm libMyTest.a                查看库中包含的函数等信息
```
第三步：使用静态库
```
第一种方法：
gcc + 源文件 + -L 静态库路径 + -l静态库名 + -I头文件目录 + -o 可执行文件名
gcc main.cpp -L lib -l MyTest -I include -o app
./app

第二种方法：
gcc + 源文件 + -I头文件 + libxxx.a + -o 可执行文件名
gcc main.cpp -I include lib/libMyTest.a -o app
```


### 编译动态库

第一步：生成与位置无关的.o文件
`gcc -fPIC *.c -I ../include -c   参数-fPIC表示生成与位置无关代码`

第二步：创建动态库
```
gcc -shared -o libMyTest.so *.o        参数：-shared 制作动态库 -o：重命名生成的新文件
mv libMyTest.so ../lib
```
第三步：使用动态库
```
第一种方法：
gcc + 源文件 + -L 动态库路径 + -l动态库名 + -I头文件目录 + -o 可执行文件名
gcc main.c -L lib -l MyTest -I include -o app
./app
（执行失败，找不到链接库，没有给动态链接器（ld-linux.so.2）指定好动态库 libmytest.so 的路径）

第二种方法：
gcc + 源文件 + -I头文件 + libxxx.so + -o 可执行文件名
gcc main.c -I include lib/libMyTest.so -o app
（执行成功，已经指明了动态库的路径）
```

如何解决第一种方法中找不到链接库的问题

```
使用命令ldd app可以查看当前的链接库情况

第一种方法：
export LD_LIBRARY_PATH=自定义动态库的路径
（只能起到临时作用，关闭终端后失效）
LD_LIBRARY_PATH ： 指定查找共享库（动态链接库）时除了默认路径之外的其他路径，该路径在默认路径之前查找

第二种方法：
将上述命令写入home目录下的.bashrc文件中，保存后重启终端生效（永久）

第三种方法：
直接将动态库拷贝到user/lib的系统目录下（强烈不推荐！！）

第四种方法：
将libmytest.so所在绝对路径追加入到/etc/ld.so.conf文件，使用sudo ldconfig -v 更新
```