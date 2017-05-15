# 写一个简单的 插件

因为sublime 的一个快捷键只能绑定一个命令， 想要一次执行多个命令时，可以写一个插件合并两个命令

## sublime3 版本

## sublime2 版本
1) Tools → New Plugin

	import sublime, sublime_plugin

	class RevealInSideBarAndFocusCommand(sublime_plugin.WindowCommand):
	    def run(self):
	        self.window.run_command("reveal_in_side_bar")
	        self.window.run_command("focus_side_bar")

Save as RevealInSideBarAndFocus.py


2) Sublime Text 2 → Preferences → Key Bindings — User

Bind it to shortcut:

	{ "keys": ["alt+shift+l"], "command": "reveal_in_side_bar_and_focus" }



refs:  
[API  reference](http://www.sublimetext.com/docs/3/api_reference.html#sublime.View)  
[Is it possible to chain key binding commands in sublime text 2?](http://stackoverflow.com/questions/9646552/is-it-possible-to-chain-key-binding-commands-in-sublime-text-2)  