# ahk 代码的字符编码

脚本文件编码

首先请阅读帮助中相关内容：脚本文件代码页。这里说明了解释器（AutoHotkey.exe）加载脚本时选择编码的优先级顺序：

    若脚本文件开头为字节顺序标记（BOM），则据其选择相应的编码（UTF-8 BOM 或 UTF-16 BOM）；
    若解释器命令行中包含了 /CPn 选项，则使用 n 指定的编码；
    其他情况下，则使用系统默认代码页（一般简单称为 ANSI 编码）。


一般情况下建议脚本文件使用 ANSI 或 UTF-8 BOM（注意必须加上 BOM）编码，这样一般情况下脚本文件都能正常加载，但下列两种情况中必须使用 UTF-8 BOM 编码，否则脚本加载或执行时会出问题：

    脚本文件中包含多种非 ANSI 编码字符集的字符，如同时包含简体中文和俄文；
    脚本可能在不同默认代码页的系统中执行，例如在简体中文系统和日文系统；


对于简体中文 Windows 系统，默认代码页为 CP936（也可以认为是 GB2312、GBK 或 GB18030），这是种双字节字符集（缩写 DBCS，是多字节字符集即 MBCS 的一种，与单字节字符集 SBCS 相对；典型的多字节字符集如汉字，而单字节字符集常见于欧洲语言）。对于上面的第二种情况，如果脚本只包含 ANSI 字符，那么应该也能正常执行，不过中文用户脚本中不包含汉字的可能性有多大呢？

注：AutoHotkey Basic 默认脚本编码为 ANSI；对于 AutoHotkey_L，在 1.1.08.00 版本之前，ANSI 构建（build）默认脚本编码为 ANSI，但 Unicode 构建默认编码为 UTF-8，为了减少混乱，该版本之后脚本默认编码都使用 ANSI（所以 UTF-8 编码的脚本必须包含 BOM 头部才能被正确识别）。

SciTE4AutoHotkey 中在工具中设置默认代码页为 UTF-8 时创建的 UTF-8 脚本不含 BOM：



refs:  
[AHK常见的编码问题](http://ahkscript.org/boards/viewtopic.php?f=29&t=4292)  