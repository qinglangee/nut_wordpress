# C++ 控制台清屏方法


## 调用系统函数
缺点是比较闪
```
#include <iostream> 
#include <windows.h> 
system("cls");
```

## 屏幕定位局部重写
缺点是逻辑会更复杂，比较不闪烁
```
void move(short x,short y) {
    HANDLE hOut=GetStdHandle(STD_OUTPUT_HANDLE);

    COORD pos={x,y};//x,y为屏幕坐标

    SetConsoleCursorPosition(hOut,pos);
}
void goPos(int i, char c){
    if(i < 0){
        return;
    }
    short x = i % 10;
    short y = i / 10;
    move(x, y);
    printf("%c", c);
}
```
## 一些相关 api 
用于控制台窗口操作的API函数如下：

GetConsoleScreenBufferInfo 获取控制台窗口信息

GetConsoleTitle 获取控制台窗口标题

ScrollConsoleScreenBuffer 在缓冲区中移动数据块

SetConsoleScreenBufferSize 更改指定缓冲区大小

SetConsoleTitle 设置控制台窗口标题

SetConsoleWindowInfo 设置控制台窗口信息

[c/c++ console(控制台)编程详解](https://www.cnblogs.com/flowingwind/p/8159035.html)  
这个帖子里有些控制台修改颜色的方法。 