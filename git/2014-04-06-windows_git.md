# 使用putty的ssh连接github
## putty生成sshkey文件
运行puttygen,点击generate，按提示生成一个并保存就好了。
## git clone 报错

### 没有rsa2 key

>The server's host key is not cached in the registry. You  
have no guarantee that the server is the computer you 
think it is.
The server's rsa2 key fingerprint is:
ssh-rsa 2048 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48
Connection abandoned.
fatal: The remote end hung up unexpectedly

这个原因是主机没有加入信任hosts列表， 先用putty ssh连接一次github.com，它会询问是否将rsa2 key存储在本机，点是就行了

### 添加 ssh key, 不使用 putty   [所有][1]
windows下如何github ssh 公钥

1. 安装git，从程序目录打开 "Git Bash" 
2. 键入命令：ssh-keygen -t rsa -C "email@email.com"
  "email@email.com"是github账号
3. 提醒你输入key的名称，输入如id_rsa
4. 在C:\Documents and Settings\Administrator\下产生两个文件：id_rsa和id_rsa.pub
5. 把4中生成的密钥文件复制到C:\Documents and Settings\Administrator\.ssh\ 目 录下。
6. 用记事本打开id_rsa.pub文件，复制内容，在github.com的网站上到ssh密钥管理页面，添加新公钥，随便取个名字，内容粘贴刚才复制的内容。
7. ^_^ OK了

需要注意步骤2中产生的密钥文件在当前用户的根目录，必须把这两个文件放到当前用户目录的“.ssh”目录下才能生效。
在windows中只能在命令行下输入创建"."开头的文件夹。命令为 mkdir .ssh









### Unable to open connection
>Unable to open connection:
Host does not existfatal: The remote end hung up unexpectedly

先试一下putty连接

    D:\software\putty>plink qinglangee@github.com
报错
>Using username "qinglangee".
FATAL ERROR: Disconnected: No supported authentication methods available

执照下面步骤添加sshkey, 不是直接copy public文件的内容， 先用puttyGen load, 再copy

### 验证方式错误

    FATAL ERROR: Disconnected: No supported authentication methods available
    fatal: The remote end hung up unexpectedly

1. 把windows的ssh key添加到github中的信任ssh key列表中。  
打开puttygen load一个public key, 把public key内容copy到github中添加ssh key.
2. 启动pagent, 并且加载本地的sshkey文件。

    # 使用git自带ssh连接
    ## 配置文件
在`C:\Users\[user]` 目录中新建一个.profile目录，内容如下
GIT_SSH="/usr/bin/ssh.exe"
这样git就使用自带的ssh连接工具，.profile在Git bash中才能起作用，所以要在Git bash中使用git

# Permission denied 

>Cloning into 'javatool'...
Permission denied (publickey).
fatal: Could not read from remote repository.

>Please make sure you have the correct access rights
and the repository exists.












[1]: http://www.cnblogs.com/igrl/archive/2010/09/17/1829358.html