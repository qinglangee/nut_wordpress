# 定义函数

定义一个可在CMake脚本其他位置调用的函数。
```
function(<name>[arg1 [arg2 [arg3 ...]]])
    COMMAND1(ARGS ...)
    COMMAND2(ARGS ...)
    ...

endfunction(<name>)
```
 

定义一个函数名为`<name>`，参数名为`arg1 arg2 arg3(…)`。 函数体内的命令直到函数被调用的时候才会去执行。其中ARGC变量表示传递给函数的参数个数。 ARGV0, ARGV1, ARGV2代表传递给函数的实际参数。 ARGN代表超出最后一个预期参数的参数列表，例如，函数原型声明时，只接受一个参数，那么调用函数时传递给函数的参数列表中，从第二个参数（如果有的话）开始就会保存到ARGN.

```


function (argument_tester arg)
 
    message(STATUS "ARGN: ${ARGN}")
     
    message(STATUS "ARGC: ${ARGC}")
     
    message(STATUS "ARGV: ${ARGV}")
     
    message(STATUS "ARGV0: ${ARGV0}")
     
     
    list(LENGTH ARGV argv_len)
     
    message(STATUS "length of ARGV: ${argv_len}")
     
    set(i 0)
     
    while( i LESS ${argv_len})
     
    list(GET ARGV ${i} argv_value)
     
    message(STATUS "argv${i}: ${argv_value}")
     
     
    math(EXPR i "${i} + 1")
     
    endwhile()

    if(i LESS 2)
      # then section.
      message(STATUS "i less 2")
    elseif(i LESS 3)
      # elseif section.
      message(STATUS "i less 3")
    else()
      # else section.
      message(STATUS "i not less 3")
    endif()
 
 
 
endfunction ()


# test
# argument_tester(arg0 arg1 arg2 arg3)
```