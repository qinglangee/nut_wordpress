# C++ 随机数
代码见 code/cpp/random  
头文件 C++ 重写了C的头文件，以 c 开头， 没有`.h` ， 例如 `<cstdlib>` 就重写实现了 `stdlib.h`

## 使用c标准库
先设置一下随机种子，不设置的话每次产生的序列都是相同的
```
#include <cstdlib>

srand( (unsigned)time( NULL ) ); //srand()函数产生一个以当前时间开始的随机种子 
for (int i=0;i<10;i++) 
    cout<<rand()%MAX<<endl; //MAX为最大值，其随机域为0~MAX-1
```


## C++ 11 random库
默认的种子生成随机数范围在1-2147483646之间  
 default_random_engine 默认种子每次运行都会生成相同的随机数序列  
 bernoulli_distribution 是一个分布类，但它不是模板类。它的构造函数只有一个参数，表示该类返回 true 的概率，该参数默认为 0.5 ，即返回 true 和 false 的概率相等
```
#include <random>
default_random_engine e;
// e();

uniform_int_distribution<unsigned> u(0, 9); // 随机数分布对象设置范围，结果包含0 和9 
u(e); // 生成整数

uniform_real_distribution<double> ud(0, 1); // 设置实数范围

normal_distribution<> n(4, 1.5); //正态分布，大部分生成的随机数落在0-8之间   
```