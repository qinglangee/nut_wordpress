# blender 渲染相关内容

## 设置HDRI
在材质编辑窗口中，选择世界的材质，输入改为HDRI图片就可以了。  
但是有个问题只显示单一颜色，因为选用了错的节点，不能用普通的 image texture, 要用 environment texture。

## 渲染太慢时设置跳帧渲染
这样跳着渲染就卡得轻一点，timeline->playback->sync mode->frame dropping