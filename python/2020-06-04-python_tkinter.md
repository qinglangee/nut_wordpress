# tinkter 常用内容
[Python GUI之tkinter窗口视窗教程大集合](https://blog.csdn.net/ahilll/article/details/81531587)  

[python ttk Treeview的插入、清空、各种点击事件、获取条目值、标题单击排序](https://blog.csdn.net/sinat_27382047/article/details/80161637)  
[现代tk教程](https://tkdocs.com/tutorial/intro.html#audience)  
[Python interface to Tcl/Tk](https://docs.python.org/3.4/library/tkinter.html)  
## 相关导入包
```
import tkinter
import tkinter.simpledialog as dialog
from tkinter.simpledialog import askinteger, askfloat, askstring
import tkinter.messagebox as msgbox
from tkinter.messagebox import showinfo, showwarning, showerror
```

```
import tkinter as tk  # 使用Tkinter前需要先导入
 
# 第1步，实例化object，建立窗口window
window = tk.Tk()
 
# 第2步，给窗口的可视化起名字
window.title('My Window')
 
# 第3步，设定窗口的大小(长 * 宽)
window.geometry('500x300')
window.resizable(0,0) #防止用户调整尺寸
window.mainloop()
```
## window控制
```
#防止用户调整尺寸
window.resizable(0,0) 

# 自定义窗口关闭事件
self.win.protocol('WM_DELETE_WINDOW', self.onClosing)

def onClosing(self):
    self.client.close()
    self.timer.cancel()
    self.win.destroy()

# 设置窗口一直在最前
win.wm_attributes('-topmost',True)

# 设置窗口最小化 恢复 最大化
root.state('icon')   # icon/iconic：最小化；normal：正常显示； zoomed：最大化  不带参数可以返回窗口的状态
```
## 常用控件和布局方式
pack
```
frameTop = Frame(window)  # 添加容器
frameTop = Frame(window, padx=10, pady=20)  # 设置内边距
frampTop.pack(padx=10, pady=10)   # 在pack()中设置pad则是外边距

# pack() 默认是从上向下放置，都设置成left就是从左往右放置
Label(fCenter,text='结果：',padx=5).pack(side='left')  # 文本框，设置放置的方向

Label(fCenter,text='结果：',padx=5).pack(fill=X)  # x方向占满，选项有X/Y/BOTH

# expand 允许控制扩张占满父组件，按 expand 的数值为每个组件分配比例
Label(root,text = 'pack1',bg = 'red').pack(fill = Y,expand = 1)
Label(root,text = 'pack2',bg = 'blue').pack(fill = BOTH,expand = 1)
Label(root,text = 'pack3',bg = 'green').pack(fill = X,expand = 0)
```
grid
```
Label(fBottom, text='懂你').grid(row=0, column=0) # 网格布局
Label(fBottom, text='懂你').grid(row=0, column=0, sticky="ew") # 网格布局, 组件扩张到格子的东西两边
Label(fBottom, text='懂你').grid(row=0, column=0, rowspan=2, columnspan=3) # 组件占两行，3列
```
Label
```
Label(fBottom, text='懂你', anchor='w').pack() # 内部对齐方向
Label(win, wraplength=250, justify="left") # 设置文件自动换行，不满的行靠哪边
label["text"] = "new text"   # 修改文字
label.config(text="new text")
```
Entry
```
text = Entry(fCenter, width=22)  # 输入框, 宽度好像也是指符数
text.get()   # 取值用 get() 方法
text.delete(10)  # 删除索引为10的值
text.delete(0, END)  #删除所有值
text.select_clear()  #取消选中
```
Text
```
entry = Text(parent)
entry = Text(parent, width=20, height=5)  # 宽和高是指字符行和列数
entry.insert('1.0', text)  # 插入时要设置行列， 行从1开始，列从0开始
entry.get(1.0, END)   # 取数据要设置起始结束位置
```
Button
```
Button(fCenter,text='录入', padx=5, command=record).pack()  # 按钮和函数
```
Checkbutton
```
var1 = IntVar()
C1 = Checkbutton(top, text = "RUNOOB", variable = var1, \
                 onvalue = 1, offvalue = 0, height=5, \
                 width = 20)
var1.get()  # 取控件的值
```
Frame
```
# 清空子组件
for widget in myFrame.winfo_children():
    widget.destroy()
```
Treeview
```

# 清空所有条目
x = main.tree.get_children()
for item in x:
    main.tree.delete(item)
```
Menu
```
MenuBar = tk.Menu(window)                     #创建一个菜单栏
fileBar = tk.Menu(MenuBar, tearoff=0)         #创建一个菜单项，不分窗。
MenuBar.add_cascade(label="File", menu=fileBar)  #   在菜单栏添加File菜单
fileBar.add_command(label="open")             #在菜单项中加入子菜单
fileBar.add_separator()                       #在菜单项中加入一条分割线
window.config(menu =MenuBar)                  #放置菜单栏到主窗口
fileBar.delete(0)                             #删除第一个位置菜单项
MenuBar.add_checkbutton                       #添加确认按钮
```

## 显示图片
默认只支持 gif 图片
```
img_gif=tkinter.PhotoImage(file='photo.gif')
label_img = Label(self.win, image = img_gif, )
label_img.abcdefg = img_gif  # 这里一定要设置到一个属性上,要不然图片不显示
label_img.pack()

# 图片缩放
image = PhotoImage(file='imgs/' + p['photo'])
scale_w = round(image.width()/100)
scale_h = round(image.height()/200)
if scale_w > 1 or scale_h > 1:
    image = image.zoom(scale_w, scale_h)

image = image.zoom(2)  # 扩大为两倍
image = image.subsample(2)   # 缩小为二分之一
```
用Pillow
```
img_open = PIL.Image.open('photo.jpg')
img_png = PIL.ImageTk.PhotoImage(img_open)
label_img = Label(self.win, image = img_png )
label_img.img = img_png  # 这里也是一定要设置到一个属性上

img = img.resize((width,height), Image.ANTIALIAS)  # 可以调整图片大小
```
## 设置字体
*字体设置必须在调用了Tk() 方法之后才能用*
```
import tkinter as tk
import tkinter.font as tf

enter_w = tk.Tk()
enter_w.title('Test') #设置标题
enter_w.geometry('750x500')#设置窗体大小
 
ft = tf.Font(family='华文隶书', size=40,weight=tf.BOLD,slant=tf.ITALIC,\
             underline=1,overstrike=1)  #设置字体
Lab = tk.Label(enter_w ,text='测试字体文字',fg ="white",bg = '#0000cd',\
                   font = ft,compound='center')   
Lab.pack()  #设置label显示
 
enter_w.mainloop()
```

## 事件
为 Tk() 指定关闭按钮函数
`self.win.protocol('WM_DELETE_WINDOW', self.onClosing)`  
绑定左键点击事件
`tree.bind('<ButtonRelease-1>', self.showItemInfo)`


## 弹出消息框  
```
# 显示出错信息
def showErr(msg):
    showerror("错误", msg)
# 显示提示信息
def showInfo(msg):
    showinfo("提示", msg)
```

## windows 通知
pip install win10toast
```
from win10toast import ToastNotifier

toaster = ToastNotifier()
toaster.show_toast(u'标题', u'收到一个通知')
```



