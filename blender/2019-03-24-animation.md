# blender 动画操作

## 调节动画速度
`调整物理模拟速度`
方法１　sence标签中，Rigid body world部分，修改speed选项(这种需要重新bake)
方法２　在render标签中，Dimensions部分，修改time remapping的比例参数　
`曲线调节动画速度`
GraphEditor 曲线编辑器可以用来调节两个关键帧之间的变化速度
方法１　物体添加follow path约束后，勾选fixed position,用关键帧的方式来控制物体的运动，就可以在曲线编辑器中进行控制
    在曲线编辑器中，按T可以为曲线切换不同的曲线类型
方法２　物体添加曲线为它的父物体，然后没看懂．．．(https://www.youtube.com/watch?v=HsOSDYTsG7o)