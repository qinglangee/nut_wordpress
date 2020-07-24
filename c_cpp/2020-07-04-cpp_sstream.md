# sstream 使用
stringstream：同时支持c风格字符串的输入输出操作
istringstream：用于执行c风格字符串的输入操作
ostringstream：用于执行c风格字符串的输出操作

通常ostringstream类用来格式化字符串，避免申请大量的缓冲区，替代sprintf.
该类能够根据内容自动分配内存，其对内存的管理也是相当到位  

## 设置精度
```
stringstream ss;
ss.precision(4);  // 这里的精度是设置浮点数的最多位数的
ss<<d1<<","<<d2<<","<<d3;

// 这样用两步就是设置小数固定为2位
ss.precision(2);
ss.setf(std::ios::fixed);

ss.width(8);  // 从第8列开始输出，前面是空格  
```


