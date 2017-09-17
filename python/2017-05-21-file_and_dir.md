# python 文件目录相关操作
`import os`

## 判断文件是否存在
`os.path.isfile('test.txt')` #如果不存在就返回False
`os.path.exists(directory)` #如果目录不存在就返回False 

##　递归遍历目录
```
#!/usr/bin/python
# -*- coding: utf-8 -*-
import os
def gci(filepath):
#遍历filepath下所有文件，包括子目录
  files = os.listdir(filepath)
  for fi in files:
    fi_d = os.path.join(filepath,fi)            
    if os.path.isdir(fi_d):
      gci(fi_d)                  
    else:
      print os.path.join(filepath,fi_d)

#递归遍历/root目录下所有文件
gci('/root')
```