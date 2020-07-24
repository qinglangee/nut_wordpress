# eevee 灯光渲染类教程

https://www.bilibili.com/video/av46040621

## 01 关于光01　eevee真实光基本设置
```
红蓝墙的盒子和里面的球和立方体
设置eevee达到与cycles差不多的效果
Ambient Occlusion 可以在物体边产生微小的阴影
镜面小球要有反光，需要添加reflection prob，产生反射烘焙
Screen Space Reflections选项也能让屏幕区域产生反光
DefuseBSDF 材质不反光，只是会接受间接光（看起来有点像反光但不是）
irradiance prob 球可以产生间接光烘焙
在world里面设置　Ambient Lighting, 一般就是一个颜色或HDR, 模拟室外光最好加点蓝色调子
shadows设置里的VSM模式对控制漏光更有用
```
## 02 关于光02  漏光
```
室外有强光时，室内就有可能看到漏光（阳光，ＨＤＲＩ，强烈的ＡＯ(背景光)等)
解决漏光的办法：
1. 加厚墙壁　2. 点光源产生的漏光比太阳光要小一些
3. 详细设置一下点光源的选项(墙壁要有一点厚度)
    shadow：勾选
        Clip Start:0.01
        Softness : 0.000
        Bias     : 0.001
        Exponent : 2.5  默认值
    Contact Shadows:勾选
        Distance  :0.2  默认
        Softness 2.0000　　其他的保持默认
        Bias     : 0.03  默认
    eevee 的全局shadow设置，勾选　SoftShadow(软阴影) 和　HighBitdepth(高深度),ESM改为VSM
4. 用窗口的面光假装太阳光照进来(也会在窗口产生一些溢出)
    解决窗口的溢出
        1. 把面光向外面移得远一点
        2. 烘焙一下
        3. 不要把面光放在墙壁内部
```
## 03 ReflectionProbes-反射采集器
```
反射采集球示例大小没有调出来？？？(莫名其妙地又有了，没搞明白)
反射采集球调整Clipping Start 和　End 的大小可以调整反射效果的范围（镜子球的黑部就是由于包裹了整个Clipping Start的范围）
start太小被包围了，就会出现黑块．end太小没伸出盒子，就会反射到盒子外面的物体和光线．
反射采集的边框部分是混合部分，在一个场景中有多个反射采集时会用在交叉部分
reflection plain 的distance 属性可以控制影响的范围　
```




