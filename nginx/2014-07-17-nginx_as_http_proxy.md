# nginx做 http代理

配置

	server {
        listen       8888;
        client_body_timeout 60000;
        client_max_body_size 1024m;
        send_timeout       60000;
        client_header_buffer_size 16k;
        large_client_header_buffers 4 64k;

        proxy_headers_hash_bucket_size 1024;
        proxy_headers_hash_max_size 4096;
        proxy_read_timeout 60000;
        proxy_send_timeout 60000;

        location / {
            #  用 cat /etc/resolv.conf 可以查看服务器的默认 DNS
            resolver 8.8.8.8;
            proxy_pass http://$http_host$request_uri;
        }
    }
resolver 8.8.8.8; 代表使用Google DNS来解析域名 `client_body_timeout , large_client_header_buffers` 等设置,确保大的请求不会返回400错误.

但,这个代理服务器只支持Http请求, Https会报400错误.

>上面使用谷歌 DNS 8.8.8.8，你可能在本地也需要使用这个 DNS，否则可能会出现 502 的错误。不然可以配置 resolver 地址为你 ISP 分配的 DNS 地址。
>配置完后，重启一下 nginx 或 reload 一下即可。
>注意：由于 HTTP 代理和 VPN 不一样，后者加密，而前者不加密，所以 HTTP 代理是不能用来 FQ 的。

refs:  
[使用Nginx搭建Http代理服务器][1]  
[nginx HTTP代理配置[正向代理]][2]  

[1]: http://wendal.net/108.html
[2]: http://www.rabbit8.cn/Reprinted/426.html