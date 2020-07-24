# 计算几何 清华大学 邓俊辉  
Computational Geometry  
[B站](https://www.bilibili.com/video/BV1ZE41177JM/?p=7)  

https://next.xuetangx.com/course/THU08091000327/1391645

# 1
## p1 1.1.1 A. History of this course

## p2 1.2.1 B. What's Computational Geometry 

## p3 1.3.1 C. How to learn CG Better  
先不管啥不会的，先看能学到什么  

看图很重要，看懂再看公式  

提问时暂停，思考  

用眼 动脑 动手  

一定要多练，多思考  

## p4 1.4.1 D. Why English  
扯蛋

# 2.1
## p5 2.1.1 A 01.Why Convex Hull  
凸包问题

## p6 2.1.2 A 02.Nails In The Table
桌上的钉子， 用橡皮筋围起来

## p7 2.1.3 A 03.Paint Blending
混合颜料  

## p8 2.1.4 A 04.Color Space
颜色空间  
在两种颜色的线段上，就可以用这两种颜色混合出来。不在就不能。  
目标颜色在三种颜色点构成的三角形内部，就可以用这三种颜料混合出来。 在外部就不能

## p9 2.1.5 A 05.Convex Hull
用数学表示  
凸相关，第n种是由前n-1种混合出来的，这种是没什么用的    

# 2.2
## p10 2.2.1 B Extremity
凸包的算法  
转化- 转而化之  大事化小 小事化了   
极性 
极点 过极点上必有一条直线把所有的点归于一边

## p11 2.2.2 B Strategy
转换成判断极点的问题  
再转换成点是否在其它点构成的三角形内部

## p12 2.2.3 B In Triangle Test
1 逐一遍历三角形  
O(n^4)

## p13 2.2.4 B To-Left Test
一个点相对于另两点构成的有向直线 

## p14 2.2.5 B Determinant
to-left 测试实现  
突然就出来个行列式，这讲得莫名其妙呢 

# 2.3 
## p15 2.3.1 C Definition
极边 Extreme Edges 最终对凸包有贡献的边(可以把所有的点划分到同一边)  

如何甄别极边

## p16 2.3.2 C Algorithm
算法复杂度从 n^4 到了 n^3  

## p17 2.3.3 C Demonstration

# 2.4
## p18 2.4.1 D Decrease and Conquer
减而治之

## p19 2.4.2 D In Convex Polygon Test
判断点是在凸多边形内部还是外部  

## p20 2.4.3 D Why not binary search
binary search 需要用数组存储，但动态数据插入在数组中是需要n时间的，所以在动态数据中binary search 并不能提速   

但减而治之还是把复杂度降到了 O(n^2)