# 二哥配音的一个光头材质教程

https://www.bilibili.com/video/av85971494


## 001 课程介绍

## 002 chapter3-01 材质大挑战 本章内容介绍

## 003 chapter3-02 真实世界里的材质
木头 砖 叶子 水

## 004 chapter3-03 3D世界里的材质

## 005 chapter3-04 场景简单设置

## 006 chapter3-05 颜色混合和ColorRamp的混合使用
噪波纹理通过ColorRamp后变成了黑白，黑白可以用来控制两种颜色的比例。

## 007 chapter3-06 贴图混合
1. 在用灰度贴图(置换/光泽等)/法线贴图时，color shape 设置为 non-Color
1. 法线贴图需要通过 normal map 节点转换后再接入 Principled BSDF 的法线接口

## 008 chapter3-07 把石灰整上去
## 009 chapter3-08 把腰线整上去
可以建两套UV唉， 用UV map 节点指定后续节点用哪个UV,这样调整这个指定的UV就只影响特定的节点

## 010 chapter3-09 把置换整上去
用的转换修改器实现的，把有石灰的地方去掉置换，用顶点绘制来控制。
当然置换需要细分的。 用置换的布线需要很规整，小方块那样的。要不然置换的效果不好。

## 011 chapter3-10 多个节点打组

## 012 chapter3-11 添加参考图

## 013 chapter3-12 建模一个破墙

## 014 chapter3-13 模型细化以及布尔绞门

## 015 chapter3-14 通过 remesh 来重构拓扑关系
置换要用好的布线。

## 016 chapter3-15 把材质给上去
把腰线加成了顶线和底线

## 017 chapter3-16 把置换给上去

## 018 chapter3-17 权重绘制控制置换

## 019 chapter3-18 最终渲染 本章完结

## 020 chapter4-01 本章内容介绍

## 021 chapter4（室外第一战）-02 场景集合先备好
做了几个集合，做了个平面加了6级细分，再加2次

## 022 chapter4-03 地形的大概塑形
做了个挺好玩的地形，有水有坡有水渠

## 023 chapter4-04 导入做好的砖墙

## 024 chapter4-05 给地形材质
贴个了地形的贴图

## 025 chapter4-06 添加置换

## 026 chapter4-07 添加HDRI光照图

## 027 chapter4-08 导入草的参考图
自己拍了些草的照片，总是第一遍拖入失败怎么回事。

## 028 chapter4-09 做第一株草

## 029 chapter4-10 第一株草细化一下
做了点叶子的折痕

## 030 chapter4-11 上贴图
UV一块一块地调整贴图位置

## 031 chapter4-12 做草的变种
弯一弯叶子， 删几根叶子， 旋转， 缩放， 做出许多根

## 032 chapter4-13 快乐散布一丛草
散布物设置为集合，把多个做的草放到一个集合中。 设置粒子旋转和缩放的随机性，看出自然的感觉。
散布的小草丛也做几个参数不一样的。

## 033 chapter4-14 多丛大小不一的变种草
又做了一些小一点的草丛，又做了些大点的， 哥们一共做了 16 丛

## 034 chapter4-15 把草丛转为 mesh 
转为 mesh 放入一个集合中作为粒子种子

## 035 chapter4-16 把草的半透明材质属性加上
用的是 translucent 不是 transparent 节点， 来与原来材质混合

## 036 chapter4-17 绘制用于草散布的地形权重
只在摄像机能看到的范围内加权重，越远权重越小就行了，看不见就不管了。

## 037 chapter4-18 把草丛散布上去
散布好了，先渲一个看看

## 038 chapter4-19 优化调整
根本就没搞什么优化，就是布景调了下，应该是摆景的优化了。
平面的水就是把粗糙度和透明粗糙度都调0行了

## 039 chapter4-20 优化草的散布密度
粒子修改器参数很多了，不手动操作看不明白的，以后有机会再看。

## 040 chapter4-21 草颜色多样性的优化
太多看不懂，手操时再说吧

下一个要添加氛围感了，下一个在哪里呢， 在 哪里

