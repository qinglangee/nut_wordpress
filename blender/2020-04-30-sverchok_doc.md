# sverchok 文档学习
有用的东西做下记录

# Introduction to geometry
## Basic
介绍基本术语  List, Index, Vector, Vertex, Edge, Polygon, Normal, Transformation, and Matrix.

List   就是编程语言的 list
Index  编程术语

## 3D Geometry
Vector   相当于是面向对象的对象了。 在3D编程中简化为向量，属性少嘛。 Vertex 就是一个特殊的 Vector.  用好 sverchok 的基础是理解掌握向量运算。 

Vertex   点。 三个属性，空间位置。 也可能多一个 W 属性表示权重。 mesh 用 list 存储 vertex 来表示。 

Edges    边。 用 mesh list 里的顶点序号来表示。 

Polygons 别称 Faces 或 Polys. 面/多边形。 跟边相比就是至少包含3个点。 
    还有个 blender api 新建物体的例子，不错。 因为面包含了边，所以定义了面就不需要定义边了。 

# Curve
Curve    与数学中的曲线基本上一样的。 
    Sverchok 中的曲线特性：
    有两个端点，不能多也不能少
    但可以是个封闭的，就是两个端点重合。 
    曲线中可能没有空间，挤一块好像是有多个端点。 
    也可能缩成一个点。 
    curve domain 曲线域
    natural parametrization 自然参数化，就是曲线变成直线的那个参数
    Evaluate Curve节点或Curve Length Parameter节点用来把曲线转换为网格形式。 


# Surface
Surface   与数学的曲面也基本一致。 
    曲面也可以是封闭的。  比如圆柱 圆环  球
    “good enough” functions -continuous and having at least one derivative at each point。 
    好的函数-连续并且在每个点上至少有一个导数。 
    surface domain. 曲面域 同样的曲面在不同参数下可以有不同的域。
    Evaluate Surface节点用来把曲面转换为网格形式。  曲面的可视化 
    Tessellate & Trim 节点也可以用来可视化曲面。 


# Scalar Fields  标量场
Scalar Fields 是一个数学对象， 用来定义一个把三维数据转为一维的函数。


# Vector Fields  矢量场
Vector Fields 是三维转三维的。  从P到P'  或从原点到Q。 Sverchok 一般用从一点到另一点的表示方法。 
    Apply vector field 节点 返回 P',即 P+Q
    Evaluate vector field 节点 返回 Q


# Introduction to Sverchok

## Unit 00 - Introduction to NodeView and 3DView
基本介绍 blender 和 sverchok 添加节点的使用

## Unit 01 - Introduction to modular components
学这个需要向量和三角函数的基础。 
每节介绍不多于10个的节点


### Lesson01 - A Plane
本节介绍节点 
Math, Vector In, Float, Range Float, Viewer Draw, Stethoschope, Formula, Vector Math

用这些共同组成一个平面。 
Formula 的格式很奇怪， 搞不懂，照着教程都摆不出姿势。。。

### Lesson02 - A Circle
本节介绍节点
List Length, Int Range, List Shift, List Zipt

手动创建圆  可调整的分段数量 

手动创建边  用 list shift 和 list zip

### Lesson03 - A Grid
Math: Modulo    Integer Division

思路很重要，一个mod, 一个除法取整。 得出点的坐标。 然后计算出四边形。 

# Panels of Sverchok
## Node Tree Panel 

## Nodes Toolbar
打不开？？？

## Presets Panel
可以保存复用 

## 3D Panel 

那个 Scan for props 没看懂， 什么意思 

## Import Ecport Panel

## Groups Panel
没找到？ 快捷键就行了  Ctrl-g

## Templates
现在改名叫 Examples 了

# Nodes
这块就太长了，等有需要再看吧。 基本上 ok 了， 可以去看别人的教程了，有不懂的回来查节点。 

学过的节点：

Generator:
    Line 可以产生直线上的点，为 vector in 作为位置的输入
    Box
    Circle
    Sphere
    Random Vector MK2
    Generators Extended:
        Profile Parametric MK3
Transforms:
    MoveA
Analyzers:
    Calculate Normals
Modifiers:
    Modifier Change:
        Polygon Boom
    Modifier Make:
        UV Connection
        Convex Hull
Number:
    A Number
    Scalar Math
    Number Range
    Random Num Gen
    Random
    Float to Int
    Formula

Vector:
    Vector In
    Vector Math
    Vector Interpolation

Matrix:
    Matrix In

List:
    List Main:
        List Join
        List Zip
        List Length
    List Struct:
        List Shift
        List Slice

Viz: 
    Viewer Draw MK3
    Viewer BMesh

Text:
    Viewer text mk3
    Stethoscope MK3A

Scene:
    Frame info


# Jimmy 直播视频 

## 001 随机选图片块




















