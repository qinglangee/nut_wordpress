# bash 基本语法

## 大小判断
`if [[ $# -eq 0 ]];then exit 0;fi;    # 数字相等`

## 数学运算
```
a=1
b=$[$a+2]
echo $b    # 3
```
## 多个条件连接
`and:  -a     or: -o`
`if [ $a -gt 5 -a $a -lt 10 ]`
`if [ $a -gt 5 -o $a -lt 2 ]`

*其它比较和字符串等比较参见 wordpress/bash/2015-05-13-if_string_num.mkd*

## if else
```
if [ $num -gt 5 ]
then
    echo "num is great than 5"
elif [ $num -gt 3 ]; then
    echo "num is great than 3"
else
    echo "num is not great than 3"
fi
```

## 循环
```
while [ condition ]
do
   command1
   command2
done
```

## case 语法
```
case $1 in
a) echo alpha;;
b) echo beta;;
c) echo coda;;
*) echo other;;
esac
```