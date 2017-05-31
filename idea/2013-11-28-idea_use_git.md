# 在IDEA中使用git
## git

### 配置
1. 打开 File->Settings->Version Control->Git
在 Path to Git executable: 中填写git的执行程序路径
2. 打开 File->Settings->Version Control->Github
host填github.com, 填好用户名,密码后点Test测试.

### 检出项目

#### 从github中检出项目
选择菜单”VCS — Checkout from Version Control — Github”：
或者在欢迎界面上也有 Checkout from Version Control,
填好信息后, 点击”Clone”按钮，即完成获取过程。

## 项目管理

### 删除项目
1. 关闭项目 File->Close Project
2. IntelliJ IDEA 删除项目，先关闭项目，然后界面上不会是有项目例表，鼠标移到你想要删除的项目上（不要点击，一点就打开了），然后按DELETE键

## 快捷键
http://blog.csdn.net/palmerma/article/details/9163749

* Ctrl + B
跳转到定义处这个就不用多说了，好象是个IDE就会提供的功能
* Ctrl + W
按一个word来进行选择操作在IDEA里的这个快捷键功能是先选择光标所在字符处的单词，然后是选择源
代码的扩展区域
* Ctrl + Q
在editor window中显示java docs这个功能很方便
* F2/Shift + F2
跳转到下/上一个错误语句处IDEA提供了一个在错误语句之间方便的跳转的功能
* Shift + F6
提供对方法、变量的重命名
* Ctrl + Alt + L
根据模板格式化选择的代码,根据模板中设定的格式来format你的java代码
* Ctrl + ]/[
跳转到代码块结束/开始处
* Ctrl+F12
可以显示当前文件的结构
* Ctrl+Shift+N
可以快速打开文件
* Alt+Insert
可以生成构造器/Getter/Setter等
* Ctrl+Alt+V
可以引入变量。例如把括号内的SQL赋成一个变量
* Ctrl+Shift+Space
在很多时候都能够给出Smart提示
* Ctrl+J
Live Templates!
* Ctrl+Shift+E shortcut.
最近编辑过的文件列表

## IDEA配置

### 配置JDK
打开 File->Project Structure, 在Project SDK下选择安装的JDK位置.


## eclipse转向IntelliJ IDEA的问答
http://arhipov.blogspot.com/2011/06/whats-cool-in-intellijidea-part-i.html
http://arhipov.blogspot.com/2011/07/whats-cool-in-intellijidea-part-ii-live.html
http://arhipov.blogspot.com/2011/08/whats-cool-in-intellijidea-part-iii.html
http://www.open-open.com/bbs/view/1380256028555

http://www.jetbrains.com/idea/documentation/migration_faq.html

* 在IntelliJ IDEA中有动态模板---通过输入相关缩写调用预定义的代码片段。它们可能包括上下文参数,用于在它们插入时自动调整。点击这里查看更多有关在代码中如 何使用模板的信息。要管理动态模板,按Ctrl+ALT+S键打开设置对话框,然后单击Live Templates来增加。
