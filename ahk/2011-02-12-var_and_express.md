太他娘的变态了
0. 用函数的时候要看清接不接受表达式,   (重要)

1. 没有明确的变量类型
    所有变量都以字符串形式存储
    当字面是数值的变量进行数学运算或比较时,会自动转换为数值.
2. 除了函数中的局部变量 其他所有变量都是全局的
    而且变量无需声明,使用时就产生了(初始值为空/空白)
3. 变量名不分大小写
4. 赋值方式有两种==========
    4.1 传统方法  用 = 来指定未引用的原义字符串或围在百分号里的变量.
        number = 123
        var = This is a string.
        var2 = %var%   ;和 = 运算符一起用时，需要使用百分号来获得变量的内容。
    4.2 表达式方法 用 := 来存储数字,引用的字符串和其它类型的表达式
        number := 123
        var := "This is a string."
        var2 := var
    4.3 获取变量的内容
        var2 = %var%
        msgbox 变量 var 的值为 %var%。
        或
        var2 := var
        msgbox % "变量 var 的值为 " . var . "。"  ;(一个百分号一个空格表示后面是一个表达式)
        这里 . 的两边一定要有空格--^  (起连接作用的两个点两边要有空格)
5. 其他
    引号中有引号,用两个引号. "She said, ""An apple a day."""  (注意引号的使用)
6. 关于 if
    重要的：一个包含有表达式的 if-语句与传统的 if-语句例如 If FoundColor <> Blue 可以通过 "if" 后面是否有左括号来区分。虽然一般将整个表达式放在括号里，但也可以像这样写 if (x > 0) and (y > 0) 。此外，如果 "if" 后面的第一项是一个函数调用或者一个像 "not" 或 "!" 这样的运算符，括号也可以完全地省略。

    单词 true 和 false 是包含 1 和 0 的内置变量。
7. 命令行传入的参数
    用%1%  %2% %3% 取得,%0%得到参数的个数