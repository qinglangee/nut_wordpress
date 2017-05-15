# rust 相关的　git 项目

最值得关注的应该是编译器本身 XD 另外 Rust 官方有很多项目，很多以前都是在 std 里面的，现在被拆出来了：

[regex][1] 正则库
[num][2] 数学计算和泛型库
[time][3]
[log][4] 日志


就像 @杨昆 提到的一样，awesome 比较全，我来说说我 star 过的几个。

Glium
一个非常赞的 OpenGL 绑定，用这个东西，用 OpenGL 比 C++ 上直接用舒服到不知道哪里去了，bindless，不需要手动管理 VAO 什么的。只是现在功能不是非常全。作者很热心也很活跃。
tomaka/glium · GitHub

nalgebra
一个低维的线性代数计算库，基本是为图形而生。
配合类型推导和Trait系统，使用很丝滑。
nalgebra by sebcrozet

Piston
Rust 游戏引擎，在 Rust 现有的库中算大项目了，只不过拆分成许多小库来协作。是一系列项目，质量都很不错。
有 2D 3D 能力，有自己的 UI 库，最近也有骨骼动画了。
不知前途如何。
一个例子是简单的 minecraft clone PistonDevelopers/hematite · GitHub
[PistonDevelopers/piston · GitHub][6]  

Rust-Doom
Doom 的克隆。
cristicbz/rust-doom · GitHub

Nom
Parser 组合子，貌似是很高端的东西。
Geal/nom · GitHub

Rust-PEG
PEG Parser 生成器。可以生成 Parser 代码，也可以内嵌。也可以编译时编译 PEG。
kevinmehall/rust-peg · GitHub

frustals
分形，点进去看图片就知道了。
FakeKane/frustals · GitHub

Mio
异步 IO（图文无关）

carllerche/mio · GitHub

reenix
用 Rust 操作系统！不过看了一下开发不是特别活跃的样子
scialex/reenix · GitHub


另外 [This Week in Rust][5] 这个网站每周更新，也经常提到各种 Rust 项目。

另外有什么 Rust 问题欢迎私信XD 



refs:  
[GitHub 上有哪些值得关注的 Rust 项目](http://www.zhihu.com/question/30511494)  


[1]: https://github.com/rust-lang/regex
[2]: https://github.com/rust-lang/num
[3]: https://github.com/rust-lang/time
[4]: https://github.com/rust-lang/log
[5]: http://this-week-in-rust.org/
[6]: https://github.com/PistonDevelopers/piston