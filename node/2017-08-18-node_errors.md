# node 常见与不常见错误

## 升级node之后，运行项目时MongoDB驱动报错：

    [Error: Module did not self-register.]
    js-bson: Failed to load c++ bson extension, using pure JS version

造成这个问题的原因是node升级后C/C++模块没有重新编译。