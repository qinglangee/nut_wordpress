# maya 建模技巧 
https://www.bilibili.com/video/av93952351?from=search&seid=275676505457885667
是个广告， oh shit!

Teacher : Paul Conner


另一个真货，没字幕 Modeling Complex Shapes Study in Maya (with Paul Conner)
Digital Tutors - Professional Tips for Modeling Complex Shapes part 1
https://www.bilibili.com/video/av89435137
链接：https://pan.baidu.com/s/1u5jECVE6C3T8UVI9IvQC-Q    提取码：hvir 
part 2 
https://www.bilibili.com/video/av89406895
链接：https://pan.baidu.com/s/1od25oVdFIoaufzCwsvuDTw    提取码：jl3j
part 3
https://www.bilibili.com/video/av89438430
链接：https://pan.baidu.com/s/1dUOdibawpA3zXATu2GwG-g    提取码：qyu7
Part 4
https://www.bilibili.com/video/av89436319
链接：https://pan.baidu.com/s/1-v1IQ3z7si9SbHKM_j1Bsw    提取码：0r7u
复制这段内容后打开百度网盘手机App，操作更方便哦

锦程XJC https://space.bilibili.com/483748249

# part 1
## 01 Introduce

## 02 Discussing tips and techniques
对于布线，每一个开状改变的地方应该有线与之配合。 
然后就是细分对于形状的影响，所以有了卡边。

## 03 Utilizing methods to trouble shoot 
镜像物体不平滑： 有可能是镜像中心有重合点。 也有可能是两边法线方向不同。 
本该平滑的地方没平滑： 可能是有了重合点，起了卡边的作用。 
    一种方法是选择一个点移动看一下。多的点就显出来了
    另一种方法是显示面的中心，这样在线上显示的中心就是有面被夹在里面了。 
该平滑的地方没平滑：竟然不是以上的原因。  当原因很难查找的时候，把有问题的地方删掉重建有时是最快的方法。

## 04 Discussing texture and surface stretching
贴图被拉伸，主要是细分时格子不均匀。 把格子均匀一下就好了。

## 05 Fixing spherical poles
对于经纬球的顶点，细分平滑就会产生极点的不平滑。 解决方式就是变成四边形。

## 06 Beveling round corners
对圆角的一边进行倒角，倒角里面就形成一个多边形，细分就会拉扯变形。 解决方式就是多卡一条边。（还是卡边）

## 07 Continuing beveling
向内拐角边的倒角。。。。。 我也不知道在写些什么
对于一分三的倒角，两边的两条与原来角的两条对齐，中间一条内则与卡边交汇

## 08 Beveling options
这个对于 blender 就没什么用了

## 09 Converging bevels
两条边倒角汇聚
1. 两条边外侧及中间正常连接，然后相邻的边连起来，到交汇处形成一个多极点和一个三角形。三角形后面要处理掉的。
1. 另一种方法，因为交汇之后就是平面了，可以让外侧两边合到一点，内侧逐渐形成内插面的形式。

## 10 Discussing beveling vs. fencing
使用倒角和手动卡线的区别
倒角时会自动圆滑被倒角的位置，卡线时不会圆滑，所以再细分后倒角的会比手动卡的更圆。

## 11 Continuing beveling vs. fencing
不管用哪种方法，都是要处理边角线

## 12 Modeling basic forms
一个简单的例子

## 13 Applying proper Booleans
圆形的边数很多情况下都选8个，8在多数情况下比较好处理。  
一个简单的8边圆接方形。

## 14 Referencing objects
用一个物体做参考，吸取到参考物体上（比如说圆）
有挤出边界的形状的边做倒角时，外圈最好做成一个循环的形式，这样横竖相交的倒角交汇布线会比较好。  

## 15 Discussing primitives
不太有意思的小方法

## 16 Using primitives objects 
使用基本物体？

## 17 Working with Transform Component tool
一个嘛工具，不知道 blender 有没有

## 18 Booleaning a curved object
跟平面差不太许多吧，找好点位，处理好后事

## 19 Cutting close to bevels
在离倒角很近的地方切割挖洞
挖洞不要影响到边，各边在细分的时候最好不要变形。

## 20 Using reference objects for measuring
用参考物体做测量
挤出时各边可能挤出的距离不一样，用同样宽度的物体做参考，挤出完事后再吸附到对齐的点位上。

## 21 Adding part lines
用圆形做个圆角再做条细缝。 感觉自动细分圆滑不就好了么。

## 22 Transitioning bebels
从锐利整洁的倒角过渡到平滑的曲面
这没有什么好的方法，只能让你的布线很少，保持低模，让细分自动平滑。
把倒角线从紧致手动过渡到均匀分布。

## 23 Using repetition
重复

## 24 Discussing primary and secondary shapes
主要和次要形状
先做出大形状，再在大形上加细节。 

## 25 Utilizing primitives
半个管道在平面上先是高再过渡到低，手动做非常复杂。 
在直线上利用圆柱做出高度线，再把每一段的点移到应对应的位置上。 

## 26 Continuing to utilize primitives
上一节没做完，这一节接着做
最后用的是两根管道，手动调节的高度过渡。 

## 27 Using primitive objects
把目标物体分解成各个基本物体的组成，再组合起来。

## 28 Continuing to use primitive objects
上一集没弄完，接着弄
最后处理线的方法还挺高级的，弄前想不到，弄完挺好的。

## 29 Finishing our study
这就 over 了

# part 2
## 01 Introduction and project overview
跟 part 1 类似

## 02 customizing the Maya interface
没什么用

## 03 Preplanning for correct geometry
没看懂计划了什么
好像是分散的倒角线固定了间隔太大的边。

## 04 Continue to preplan for correct geometry
继续

## 05 Discussing promary vs. secondary shapes
一个布尔的例子，没看出什么来。

## 06 Continue discussing promary vs. secondary shapes
继续

## 07 Breaking down forms into smaller shapes
在一个圆弧上切下一块平面，难点是圆弧的弧度不好控制。   
他的做法是先做出切面来，旋转阵列放好，再连起来当做圆柱，真是闻所未闻，惊得一P.  原来那中间根本就不是个圆柱。
最后一条一条边地把所有要倒角的边选起来，真得受不了。。。可能是道行还是不够吧。  

## 08 Using deformers to help in modeling
用变形器辅助建模，要不然扭曲的东西不好做。  
回去研究自己的变形工具。  

## 09 Converging edges and repetition
斜面的突起平滑到平面
汇聚的边的重复网格
突出的块，细分之前要卡边，自己做也是很不好做。 要是不做的话就会觉得很简单，以后的不能一天好几十地看了，要动手。

这个主要矛盾还是倒角边的交汇处。 不能平滑出去。看他怎么处理吧。  
重复的物体就把需要重复的部分独立出来处理，这样两边的没有其它影响，向外扩展时更少顾虑。

## 10 Continue converging edges and repetition
这个其实并不好做，有空可以复习一下

## 11 keeping points oriented and spaced correctly
## 12 Continue keeping points oriented and spaced correctly
他只用倒角就解决了要圆滑的问题，选择哪些要倒角的边很重要，会产生不同的结果。  

又领会到的一个点啊：倒角的时候多条边交叉的情况，不要倒很多条，原线两边各卡一条就可以了，太多了容易乱。 最好的情况是四线交到一起，出四边面和四边点。 三条线和五条线就会出三边面和五边面，还有三边点和五边点。 


## 13 Cleaning up booleans and average vertices (清除布尔后遗症 and 平均顶点)
最大的困难竟然是 blender 中布尔的两个物体不能重合面，也不能重合点，点在别人的面上也不行？？？
## 14 Continue cleaning up booleans and average vertices
原来他布尔的也是不能重合点（不知道能不能重全，反正他做的时候没重合），然后又手工合并的。（用合并距离限制合并的） 不过他的平面重合布尔时没问题。 
然后他有个 average 的工具，跟 blender 的功能好像不太一样，没怎么看明白。  没找到功能类似的工具。 

## 15 Applying boolean order and correct geometry amount (应用布尔的顺序 和 改正图形数量)
在应用布尔时，多个物体布尔可能会出现不同的结果。 如果结果不对的话可以调整布尔的顺序重新试试看。  
在 blender 里表现不太一样，顺序不影响结果。 
## 16 Continue applying boolean order and correct geometry amount
布尔产生的线很乱，大佬一根一根地进行了清理，出来一个好看的布线。  一会又布尔了一个圆柱上去，又一根一根地调整布尔的乱线， 大佬是真的有耐心啊。 
后面布尔上去的圆柱下边没有被圆滑，有点问题，具体是啥问题没太看懂，反正大佬一通操作后就变好了。好像就是删掉了重新加了一遍。 不得不说真是有耐心啊，这样才能成为大佬呢。 


## 17 Blending cylinders together(竟然blending 。。。  圆柱混合)
三个圆柱相接的例子，同样粗细的，细一点的，细很多的。
同样粗细的最简单，对齐布尔就可以了，稍微整理一下点。 
细点的管子装到粗管子上，最好可以减少粗管的分段数，少了好控制嘛。 共8个，相接处两个就很好，但这样一细分体积就圆滑掉很多。 再多一点，16段可能就有4个相接面，处理起来还行。 小的给了8段，后面再细分一下就变圆了。
## 18 Continue blending cylinders together
很细的接到粗管上，原来粗管是20段，大佬给改了了16段， 以便让小管可以在两段中挤下来。 这样就更好处理一些。 细管就用8段，上下各卡一道边就可以了。 
那再来一个，如果稍细点的那根管子段数比较多呢，怎么办？ 那就调整被加的粗管，竖直方向上与细管多对应，再加几条水平线的方式来与对应不上的边进行连接。 

很遗憾的一点是，maya 在圆柱创建之后可随时调整它的圆的段数，blender 只能在创建之时调整。 后面就不好调整了。 （可以熟悉一下参数建模插件）


## 19 Opposing Booleans and Bevels (抵制布尔和倒角？反抗布尔和倒角？)
他会分析产生目标图形需要几条边，这很重要，应该学会分析。 
## 20 Continue opposing Booleans and Bevels
就是一个示例。。。

## 21 Project overview
一分钟总结一下


# part3

## 01 Introduction and project overview
简单介绍

## 02 Optimizing the Maya Interface
这就跟 blender 无关了。 

## 03 Setting up custom Maya presets and tools 
也是设置 maya 的， 与 blender 无关了。。  
他竟然直接用几行脚本创建了一个按钮，blender 好像没有这个创建按钮的功能，只能创建一个插件了。 

## 04 Applying custom options for beveling
新建了两个添加倒角的按钮

## 05 Discussing geometry amount and modeling options (讨论几何数量和建模选项 )
讲了点体积保持的事情， 细分之的互常会损失体积。 细分之前分段多损失的就会少一些。  
## 06 Continue discussing geometry amount and modeling options 
卡边的线与内部距离太远会出现拉扯变长的（在细分后），虽然没什么大的影响，但是可以通过中间加分隔线来加强固定。 







