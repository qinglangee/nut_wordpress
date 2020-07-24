# blender 视频合成

## 把视频拆成图片序列。 
这一步不是必需的，但是图片序列可以自由控制帧率。

1. 打开movie clip editor,导入视频。在n面板可以查看视频的帧率。
2. 在output属性面板中，修改帧率为视频的帧率。
如果帧率是24.98这种选项里没有的，就把帧率设置为Custom (自定义), FPS设为2498，然后下面的base设置为100。  
3. 然后修改分辨率为视频分辨率，如x 1920, y 1080等，按视频的修改。  
4. 然后进入Compositing工作面板，默认会打开Composito。 勾选 Use node和auto render,  然后把输入节点改为movie clip.  
5. 在输出标签页面，修改输出格式为jpeg,质量设置为最高，然后选择好输出目录，点击 ctrl-f12 等待完成。

## 摄像机路径解析
1. 如果拆成了图片就导入全部图片，设置为想要的帧率。 没拆就直接导入视频 。 
1. 设置好总的帧数。 Set Scene Frames
1. 设置motion model. 一般摄像机自由移动就选perspective, 其它只有位置或大小变化的就选相对应的。
1. 勾选 normalize, 减少光照变化的影响。
1. 在tracking settings Extra中设置Correlation为0.9, 这表示在追踪标记时正确率为90%以上时才继续。 设为0表示忽略错误，设为1表示完全正确才行，不容错。
1. 添加标记。可以ctrl-左键直接添加，也可以先在track t面板点击add按钮再添加。 添加后在track n面板中可以查看，也可以调整框选区域大小。 按alt-s显示搜索区域大小，也可以调节。
1. 记录标记的路径。按alt-右方向 可以逐帧添加标记的轨迹。 按L可以把标记锁定在屏幕中央，方便观察。按ctrl-t可以自动完成剩余的轨迹自动添加。 有错的可以手动修改。 轨迹完成后按ctrl-L可以锁定轨迹，防止不小心移动破坏等。
	按shift-左方向  回到第一帧。  
	如果标记比较清晰容易识别，可以在第一帧标记多个，全选ctrl-t.
1. 解析摄像机路径。 打开Solve t面板，用三角架时勾选tripod, 没用的就不勾。keyframe勾上，这个表示设置起作用的帧的范围，一般让它自动选或全部就可以了。
	优化参数： Refine参数， 知道焦距的话可以直接设置焦距，最准确。这个参数就选 K1K2就行了。不知道焦距的话就选 Focal length, K1K2, 这样自动计算焦距。  


1. 开始解析相机路径。 点击Solve Camera Motion. 解析完成后，错误的数值要越小越好。注意调整上面的优化参数。  
计算完成后，在右上角clip Display中勾选info. 这样在画面上会显示每个标记点的信息，把错误数值比较大的直接删除掉可以降低错误的平均值 。 

1. 把相机轨迹用到3D场景中。 2.8中很简单，点击Scene Setup中的Setup Tracking Scene按钮就可以了，顺便点上Set as Background,可以在摄像机窗口看到视频的内容。
1. 匹配视频与3D模型的世界。选同一个平面的三个标记，点击Solve t面板->Orientation中的Floor按钮。 然后设置origin 和 x y轴。   
设置比例没看明白，以后再复习吧。 

## 设置合成节点

Movie Clip节点和Render Layer 节点用 Alpha Over节点合成，合成后输出到Viewer和Composite节点。


合成viewer显示大小控制，快捷键 v alt-v

## 设置渲染背景透明
1. 在 Render(渲染属性)->Film 下，勾选 Transparent.
1. 在 View Layer(视图层属性)->Filter 下 ，去掉Environment的勾选。 (这个是可能有影响)  

## eevee 设置阴影捕捉
添加一个平面，材质->Settings->Blend Mode 选择 alpha blend.
材质节点设置：  
Diffuse BSDF->shader to RGB->RGB to BW->math(greater than)::@01   math调整阈值，接到output上查看
Emission::@02    Transparent BSDF::@03

@01->fac    --  
@02->Shader -- Mix Shader::@04  -> Output  这是正面阴影捕捉，@02设置阴影的颜色  
@03->Shader --   

Texture Coordinate -> Mapping(选Normal,Scale全取-1)::@05

Geometry->fac
@04->Shader -- Mix Shader  -> Output  这是正反两面的阴影捕捉
@05->@04->Shader

根据 https://www.bilibili.com/video/av42075600/
设置第一层时教程透明部分是显示底色，自己是黑色，那为啥是黑色呢？
材质->Settings->Blend Mode 选择 alpha blend.

[另一种方式设置阴影捕捉](https://haokan.baidu.com/v?pd=wisenatural&vid=11574613347367503110)   