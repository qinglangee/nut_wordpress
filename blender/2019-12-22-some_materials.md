# 一些材质设置方法的记录

## 节点编辑插件
连接两个节点：alt-右键从一个节点滑向另一个
混合两个着色器： ctrl-shift-右键从一个滑向另一个， ctrl-0
当前节点输出：ctrl-shift-左键点击节点
添加一个纹理节点输入：ctrl-t  


## 皮革材质 [视频][1]

## 生锈材质 [视频][2]
Texture Coordinate(Object)->Mapping->Noise Texture::@01  产生噪音输入，但前面为什么要加 Object的Mapping转换没太搞明白
Noise Texture(color)->Noise Texture(color)->Height-Bump::@02  为最终bump产生normal值，为平面部分产生不平的感觉。  

@01->ColorRamp->Height --  
-----------@02->Normal -- Bump::@03  最终bump, 为shader产生normal值。用colorRamp来调整bump的平面与凹陷比例。  

@01->ColorRamp::@04   用来控制表面颜色，colorRamp中添加两三个颜色，调整各个颜色的分布。  

@04->BaseColor --  
@03->Normal    --  Principled BSDF -> output   最终输出，Principled 金属属性调为1。 

## 矩阵显示材质  [论坛帖子][4]

## 一张图片出凹凸材质 [视频][5]  
ImageTexture->RGB分离::@01  从图片中分离出单色色阶图，取一个对比明显的作为色阶图
@01->反转->颜色渐变::@01  反转和颜色渐变是可选的，粗糙度的位置反了可以加个反转，颜色渐变可以加强色阶对比度
@01->Roughness      --  
@01->Bump->Normal   --  Principled BSDF -> output

可以再给物体加一个置换修改器(Displace), 添加图片做为贴图，强度设为0.01或大小再细调。 置换是需要面细分多一点儿的，面少了置换效果不好。  






refs:  
[blender 5分钟制作皮革材质][1]  
[Blender 教程 EEVEE 程序化生锈材质制作][2]  
[Blender 教程 EEVEE 破损残缺金属材质制作][3]  
[Animatable Pixel Matrix Display][4]  


[1]: https://www.bilibili.com/video/av77753053   
[2]: https://www.bilibili.com/video/av47634616
[3]: https://www.bilibili.com/video/av46486296
[4]: https://blenderartists.org/t/animatable-pixel-matrix-display/1126033
[5]: https://www.bilibili.com/video/av81508799