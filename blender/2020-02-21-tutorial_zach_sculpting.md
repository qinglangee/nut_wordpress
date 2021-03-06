# 扎克雕刻教程

https://www.bilibili.com/video/av87930881

## 0-01 课程简介
## 0-02 雕刻的基本流程
## 1-01 绘画板的设置与使用

## 1-02 雕刻方法的基本介绍 
1. 在基本风格上雕刻
1. 在多级细分上雕刻
1. 动态拓扑雕刻，基本上就用这种了

## 1-03 雕刻工具-多级精度修改器
1. 多级修改了之后，想在低级添加点改模型就会乱掉。  改之前要确定好模型
1. 一种受限的雕刻方式
1. 一个好的应用方式，做的模型复制一部分，添加多级修改器后雕刻个衣服什么的。

1. 可以在添加修改器前先加一个多级精度修改器，让后面的修改器都加在多级精度上，回到无精度时还能保持模型原来的网格。
1. 给面加个多级再物理模拟，其实说来这两种用法有什么用呢，回去的状态并没有什么卵用。

1. 对雕刻好的模型进行重拓扑，拓扑模型再加多级修改器，缩裹到雕刻模型上得到细节。这个用法还有点意思 。 

## 1-04 雕刻工具-动态拓扑
动态拓扑参数
Detail size/Resolution: 细节的大小，相对的按像素。 所以物体放得越大，细节就越小。 绝对的是分辨率，就是单位分的段数。
Detailing: 细节调整方式，有相对细节和常量大小。 
	Relative Detail 相对的就是边长占像素数。
	Constant Datail 常量的就是一个单位长度被分成多少段。数值越大，格子越小。
Refine Method: 细节调整方式。
	如果笔画的细节更多，可以细分。如果笔画的细节更少，可以合并。
	根据设置的选项，只细分不合并或只合并不细分，或又合并又细分。
Smooth Shading: 光滑显示 

Remesh: 不常用的些选项，看看名字就差不多了。
	Symmetrize: 忘了对称的时候可以手动再对称过来。

## 1-05 雕刻工具-纹理
纹理就是笔刷刷出来的样子，可以创建图片纹理或程序纹理。 笔刷刷过时，黑色部分凹下去，白色部分凸上来。
Brush Mapping: 可以调整纹理在物体上的呈现方式。
	View plane 视窗投射，与屏幕平行
	Area plane 法线投射，与物体表面垂直
	Tiled 平铺，适用于可以无缝循环的纹理。想当于纹理无限扩展向物体上印刷。
	3D 程序纹理就是一种3D纹理，用这种相当于3D的 tiled(个人理解).
	Random 取纹理上的随机一块刷下来
	Stencil 镂版。 跟平铺类似，但是不铺。就一块。 可以调整旋转方向，大小等。 按右键移动，ctrl-右键 旋转， shift-右键 缩放。
Angle: 调整纹理旋转角度
Rake: 让纹理方向根据笔刷移动方向调整，雕刻头发时可以雕也一向的效果。
Random: 随机的旋转角度，与随机纹理结合可以更随机。
	Random下面的角度是限制随机旋转的最大角度的。
Simple Bias: 对于纹理黑白灰度值的处理。 -1 只黑的向下 1 只白的向上  0 黑的向下，白的向上

## 1-06 雕刻工具-笔画 stroke
Stroke Method: 笔画的连续方式。
	Space - 空间连续。
	Dots - 点画。降低取样值， 感觉类似于降低 Input Samples值。 
	Drag Dot - 就取样一次，可以拖着走。
	Airbrush - 喷枪。 点住不动就一直画。
	Anchored - 锚定。 点下位置，越拖越大。
		edge to edge - 确定大小的方式，是直径还是半径。
	Line - 两点确定一条直线。(在球上可能不直了，嘿嘿)。 直线再配合下面的spacing等选项又出新方式。
	Curve - 点击新建按钮添加曲线。 添加点，调整好曲线后，按回车或点击Draw Curve按钮在面上画出曲线。 曲线还可以复用的。 
		ctrl-右键 - 添加点
		左键 - 移动点和控制柄
		shift-右键 - 两柄对称调整。 
Spacing: 每两次画下之间的距离
Jitter: 抖动的幅度，画得线不直了
Input Samples: 单位时间内对鼠标位置取样的数量。 鼠标移动得很快时，取样值低中间有些位置就会丢掉。 雕刻得快和慢时可以调整这个值来适应。
Smooth Stroke: 光滑笔触。 笔触会延迟触发，结果会更圆滑。 
	可以调整半径和影响系数。

## 1-07 雕刻工具-衰减曲线
控制笔刷力度从中间向周围衰减的变化方式。 用曲线可以创造出不同的笔刷。 有些默认笔刷也就是改了曲线而已。 

## 1-08 雕刻工具-对称锁定
Mirror: 对称 
Lock: 锁定对应轴向，点在相应轴向不能移动。
Tiling: 每个单位长度内有多个笔刷。 笔刷个数由Tile Offset 控制。
Feather: 对称的笔画在相遇时会减少叠加的影响。
Radial: 径向。 在对应的轴向上有几只笔画。
Tile Offset: 多个笔刷时，笔刷之间的距离。

## 1-09 雕刻工具-笔刷介绍 Brush
教程里可以保持笔刷与物体比例不变。2.82里找不到了。
Options:
	Accumulate: 不选的时候笔刷叠加有上限，选了就可以一直叠加。
	Front Faces Only: 勾选了后笔刷只影响能看到的面。不过在新版本里，不勾选也是这样的。。。。
	Sculpt Plane: 雕刻的平面。 雕刻效果添加的方向。 与纹理的 Brush Mapping 有点像。  这上面的锁定按钮也没有了。。。

## 1-10 球体笔刷 blob
就球，跟默认笔刷差不多

## 1-11 黏塑笔刷 clay
有个很奇怪的trim选项，能限制在一片区域内，没看明白。

## 1-12 黏条笔刷 clay strips
这是一个用得很多的笔刷，是真的很多很多。

## 1-13 折痕笔刷 crease
刷屁股沟

## 1-14 填充笔刷 fill
填充或加深沟壑

## 1-15 平化笔刷 flatten
取中间值抹平，反向加大差异

## 1-16 抓起笔刷 grab
调整大形时用的多一些，是为数不多的在动态拓扑时不会产生新的点的工具。
有一个选项，可以限制法线方向，使移动时不能乱跑。

## 1-17 膨胀笔刷 Inflate
使各面沿法线移动，快速鼓起来。

## 1-18 层笔刷 Layer
这个一般不在动态雕刻时用，就是让刷过的地方整个高了一层。
Persistent: 鸡肋的功能，不能叠加，却能减少。

## 1-19 遮罩笔刷 mask

## 1-20 推移笔刷 nudge
在面上平移类似的移动

## 1-21 夹捏笔刷 pinch
向中间聚拢，反向则是向两边分散

## 1-22 旋转笔刷 rotate
旋转笔刷内的内容

## 1-23 刮削笔刷 scrape
可以刮出硬表面的感觉

## 1-24  -27
雕刻笔刷 sculpt
平滑笔刷 smooth
蛇形勾笔刷 snake hook
拇指笔刷 thumb

## 1-28 雕刻模型-显示与选项
Options:
	Gravity: 会影响笔画向下垂。

其它的先忽略吧，想不到zach也干这种挨个讲的没用东西。

## 1-29 雕刻模型-雕刻与隐藏
很多隐藏/显示/mask 相关的快捷键在 sculpt 和 mask 菜单中。
alt-b 选取部分内容显示， 再按一次取消

## 1-30 雕刻模式的用户界面设置
关掉可以不显示的内容，风格之类的

matcap 有利于观察
开AO, 方便观察
这两个需要额外的计算量，可以到用户偏好里设置Lights,这里保存好灯光设置，不需要额外的计算量。

## 1-31 自带插件的安装与学习
sculpt tools
哪里是自带插件，明明是外面下载的，瞎JB翻译

## 1-32 雕刻插件-快速雕刻
speed sculpt 一个收费插件，看了也没用，不看了！

## 1-33 雕刻基础型的创作方法
基础物件组装
skin修改器
metaball 组装
曲线

## 1-34 雕刻常见问题及解决办法
1
没有应用的缩放
在物体量级很小时，布尔会有bug.

2
糟糕的几何图形： 有面的重合  有内部面   错误的法线   物体表面的空洞
插件 3d-print toolbox , make manifold 可以修复上面这些问题

3
薄的区域  小心点雕刻就是了

## 2-01 可爱怪物-基础网格
身体 脑袋 胳膊 腿 耳朵 尾巴

## 2-02 可爱怪物-主体部分创建

## 2-03 细节
没看

## 2-04 结束
加毛发
一个制作笔刷纹理的方法


.
.
.
.


## 3-08 生物 降低网格数量
插件 github.com/wjakob/instant-meshs   重拓扑










