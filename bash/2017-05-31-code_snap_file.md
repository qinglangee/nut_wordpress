# 文件相关的bash代码

## 判断文件目录是否存在, 不存在就创建
```
	destDir=/home/lifeix/temp/d3/move
	if [ -e "$destDir" ] ;then
	    ls $destDir
	else
	    mkdir  $destDir
	fi
```
## 批量重命名文件
把所有 .mkd 重命名为　.md
```
for file in $(find .) ; do
    newname=`echo $file|sed -n 's/\.mkd$/.md/p'`
    if [[ -n $newname ]] ; then
        mv $file $newname
    fi
done
```
塞到一行里，就是　`for f in $(find .); do n=$(echo $f|sed -n 's/\.mkd$/.md/p'); mv $f $n;done`, *一些不需要改名的， mv命令会报错，不影响结果*