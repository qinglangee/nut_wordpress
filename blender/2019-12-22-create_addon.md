# 创建一个插件
斑斓视界第二期  blender2.8-python 插件编写入门

本地下载手册有入门文章 Quickstart Introduction

[插件类命名规则][3] 

## 简记步骤

## 控制台
切换成控制台窗口，输入第一个令，创建方块 `bpy.ops.mesh.primitive_cube_add(location=(0,0,2))`  

默认包含了bpy模块， 打开控制台会看到有基本模块和常量的介绍。 补全提示是 ctrl-space .  
信息窗口显示大多数操作的命令输出，可以手动做一个动作查看对应的命令。  

```
for d in D.objects:print(d.name)    ## 遍历所有物体
for c in C.selected_objects:print(c.name)   ## 遍历所有选中的物体
```

## 文本编辑器
  在文本编辑面板新建一个文本， 并重命名为hw.py， 注意自己要经常手动保存 ， 以防不测， 首次保存需要另存为 （Shift+Ctrl+Alt+S） ， 之后可以随意保存（Alt+S） ， 用外部编辑器编辑并保存后， 可以用重载 （Alt+R） 更新脚本。 

 在文本编辑器中写脚本可以直接点运行按钮运行了，但是这里不能输入中文。 外部编辑器可以编辑中文，但运行会乱码。

## 插件信息
插件的身份信息就是插件在安装时显示在插件面板的各种信息， 比如插件名称， 作者名称， 插件分类， 兼容的Blender版本， 插件的版本等等。信息用一个在脚本开头所定义的一个名为bl_info的字典所表示， 如下

	 bl_info = {
	    'name':'Hi Addons' ,#插件名称*
	    'category':'3D View' ,#插件类别*
	    'blender':(2,80,0),#插件所兼容的blender版本号*
	    'author':'AuthorName' ,#插件作者名称
	    'version':(1,0,0),#插件版本号
	    'location':'Addons location' ,#用于说明插件功能的所在位置
	    'description':'Addon's power'#插件的功能说明
	   }
有星标的字典项是必须存在的， 不然会出错

## 简单插件代码结构
```
# 官方最简单示例
bl_info = {
    "name": "My Test Add-on",
    "blender": (2, 80, 0),
    "category": "Object",
}
def register():
    print("Hello World")
def unregister():
    print("Goodbye World")
```

```
#hiaddon.py
bl_info = {#插件的身份信息
  'name':'Hi Addons' ,  #*插件名称
  'category':'3D View' , #*插件类别
  'blender':(2,80,0),  #*插件所兼容的blender版本号， 这三个是插件所必须的键值
  'author':'作者名称' ,  #插件作者名称
  'version':(1,0,0),  #插件版本号
  'location':'插件的功能在3D视图的T面板' ,   #用于说明插件功能的所在位置
  'description':'这是一个说你好插件的插件'  #插件的功能说明
}
import bpy  #包含bpy工具
class hiadd(bpy.types.Panel):  #定义一个面板类
  bl_idname = 'hiadd'     #类的ID名称
  bl_space_type = 'VIEW_3D'  #面板所在的空间类型， 3D视图
  bl_region_type = 'TOOLS'   #面板所在的位置类型， T面板
  bl_label = 'Hi Addons'   #面板的标签
 
  def draw(self,context):  #Panel类的绘画函数
    self.layout.label(text='你好插件！ ')

def register():   #插件勾选时运行的操作
  bpy.utils.register_class(hiadd)  #挂载面板
 
def unregister():  #插件取消勾选是运行的操作
  bpy.utils.unregister_class(hiadd)  #删除面板
 
if __name__ == '__main__':  #插件在文本编辑器运行时执行的函数
  register()
```

## 安装插件
文件保存好，在blender的插件管理窗口，点击安装选择自己保存的插件文件就可以了。  


## 编写UI
面板中一般包含四种组件，标签/操作/属性/各种容器。    
在draw() 方法中添加一个带操作的按钮：  `self.layout.operator('mesh.primitive_cube_add')`    
好，最简单插件的流程就是这样。


```
# 遍历物体应用修改器
for c in C.selected_objects:
...     C.view_layer.objects.active = c 
...     bpy.ops.object.modifier_apply(apply_as='DATA',modifier='Array')
```

## 一个简单的操作插件

```
## 把选中物体的所有修改器全应用了
## 这样建立的插件需要按F3搜索名字执行
bl_info = {
    "name": "Apply all modifiers",
    "blender": (2, 80, 0),
    "category": "Object",
}

import bpy


class ObjectMoveX(bpy.types.Operator):
    """My Object Modifiers Apply"""      # Use this as a tooltip for menu items and buttons.
    bl_idname = "object.modifiers_all_apply"        # Unique identifier for buttons and menu items to reference.
    bl_label = "ApplyAllModifiers"         # Display name in the interface.
    bl_options = {'REGISTER', 'UNDO'}  # Enable undo for the operator.

    def execute(self, context):        # execute() is called when running the operator.
    	bpy.ops.object.make_single_user(type='SELECTED_OBJECTS', object=True, obdata=True, material=False, animation=False)

    	C = context
        for c in C.selected_objects:
			C.view_layer.objects.active = c 
			modifiers = c.modifiers
			for m in modifiers:
				print(m.name)
				bpy.ops.object.modifier_apply(apply_as='DATA',modifier=m.name)

        return {'FINISHED'}            # Lets Blender know the operator finished successfully.

def register():
    bpy.utils.register_class(ObjectMoveX)


def unregister():
    bpy.utils.unregister_class(ObjectMoveX)

if __name__ == "__main__":
    register()
```

## 被快捷键折磨得死去活来 
[关于name的解释][1], [另一个讨论keymap的帖子][2], 怎么样加，怎么样关闭之类的  
`bpy.context.window_manager.keyconfigs.addon.keymaps.new(name="Object Mode")`  
name: 它是一个有真实作用的属性，不是起好看作用的名字，下面代码用来显示所有的name

To see all of the potential keymaps, run this script:
```
import bpy

for i, km in enumerate(bpy.context.window_manager.keyconfigs.default.keymaps):
    print(f"{i}\t{km.name}")
```
Also, as a somewhat related side-note, when you should always check to see if a keymap already exists before calling keymaps.new().
```
# There's a more 'pythonic' way to do this with one line of code but it's 
# not as easily readable for people new to python.
if "Mesh" not in kc.keymaps:
    kc.keymaps.new(name="Mesh", etc)
km = kc.keymaps["Mesh"]
```

## 在operator 中调用系统 operator 可能需要传一个 INVOKE_DEFAULT 参数
在 [api_2_65][4] 的一个页面中发现了相关介绍，但没弄明白 
`bpy.ops.view3d.select_circle('INVOKE_DEFAULT')` 


refs:  

[1]: https://devtalk.blender.org/t/official-keymap-example-does-not-work/9032
[2]: https://blenderartists.org/t/keymap-for-addons/685544/16
[3]: https://wiki.blender.org/wiki/Reference/Release_Notes/2.80/Python_API/Addons
[4]: https://docs.blender.org/api/blender_python_api_2_65_release/bpy.ops.html