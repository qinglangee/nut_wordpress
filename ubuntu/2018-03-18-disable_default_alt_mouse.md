# 禁用默认的Alt+鼠标

## 禁用默认的Alt+鼠标左(拖动窗口)Alt+鼠标右(窗口菜单)功能

1、打开终端，菜单-编辑-配置文件首选项-命令，勾上“以登录Shell方式运行命令”，重启终端。
    英文版本是 Run command as a login shell

2、在终端输入 `gsettings get org.gnome.desktop.wm.preferences mouse-button-modifier`
查看`mouse-button-modifier`当前的值，应该是返回`<Alt>`。

3，接着输入 `gsettings set org.gnome.desktop.wm.preferences mouse-button-modifier '<Super><Alt>'`
'<Super><Alt>'为要更改的按键，意为Win+Alt，也可以改为想要的键。测试此值不能为空或禁用，否则出现默认按下Alt键的效果。

4、完事记得取消“以登录Shell方式运行命令”。

参考：

http://blog.csdn.net/huhu0769/article/details/53234257（以上内容转自此篇文章）


## 那么 Run command as a login shell 是什么意思呢
简单来说就是读的配置文件不一样, 勾选这种方式读的是~/.bash_profile 或 ~/.profile, 不勾选读的是~/.bashrc

看别人的解释

Assuming that your shell is Bash (the default in Ubuntu), these are the differences:

    When running as a login shell, Bash will read ~/.bash_profile (or, if that doesn't exist, ~/.profile) on startup. In some cases, this file reads ~/.bashrc as well.

    When running as a non-login shell, Bash will read ~/.bashrc.

So, why do you see different behaviors when running as a login/non-login shell? Because your .bash_profile/.profile is doing different things than your .bashrc.

The solution I would recommend in your case is to copy the customizations made to .bash_profile/.profile, paste them into .bashrc and disable "Run command as a login shell".

refs:
[What does “Run command as a login shell” do?](https://askubuntu.com/questions/333446/what-does-run-command-as-a-login-shell-do)  