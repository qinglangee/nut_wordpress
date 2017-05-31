# nginx 常见错误

## 403  forbidden

1.权限配置不正确

这个是nginx出现403 forbidden最常见的原因。
为了保证文件能正确执行，nginx既需要文件的读权限,又需要文件所有父目录的可执行权限。   /home 下的目录权限有的系统默认是 700

*解决办法:设置所有父目录为755权限，设置文件为644权限可以避免权限不正确。*
2.目录索引设置错误（index指令配置）

    index  index.html index.htm index.php;



refs:  
[nginx “403 Forbidden” 错误的原因及解决办法](http://www.icultivator.com/p/4750.html)  