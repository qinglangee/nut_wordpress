# cmake 指令

## configure_file
```
configure_file(<input> <output>
               [COPYONLY] [ESCAPE_QUOTES] [@ONLY]
               [NEWLINE_STYLE [UNIX|DOS|WIN32|LF|CRLF] ])
```
configure_file 主要实现如下两个功能:

1. 将 `<input>` 文件里面的内容全部复制到 `<output>` 文件中；
2. 根据参数规则，替换 @VAR@ 或 ${VAR} 变量；
[详细介绍- cmake学习之-configure_file][1]  

## file  [Doc file][3]  [CMakeFile命令之file][2]

`file(READ <filename> <out-var> [...])`
`file({WRITE | APPEND} <filename> <content>...)`

文件读/写/重命名/路径处理/上传下载等











refs:  
[CMakeFile命令之file][2]









[1]: https://www.cnblogs.com/gaox97329498/p/10952732.html
[2]: https://blog.csdn.net/tantion/article/details/84378266
[3]: https://cmake.org/cmake/help/v3.12/command/file.html






