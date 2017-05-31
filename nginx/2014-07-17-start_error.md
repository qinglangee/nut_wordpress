# nginx 启动运行错误

## 不能绑定端口

	nginx: [emerg] bind() to 0.0.0.0:80 failed (13: Permission denied)
socket API bind() 绑定小于 1024 的端口, 如 80 需要 root 权限.
here is "[Bind to ports less than 1024 without root access][1]"
简单的方法就是用 root 运行 nginx.

refs:  
[(ubuntu) nginx: [emerg] bind() to 0.0.0.0:80 failed (13: permission denied)][2]


[1]: http://serverfault.com/questions/268099/bind-to-ports-less-than-1024-without-root-access
[2]: http://stackoverflow.com/questions/18480201/ubuntu-nginx-emerg-bind-to-0-0-0-080-failed-13-permission-denied