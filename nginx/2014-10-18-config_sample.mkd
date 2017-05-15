# nginx 配置示例文件

配置一个web服务， 根目录指向 /tmp/static

	http {
	    include       mime.types;
	    default_type  text/html;
	  
	    include options.conf;

		server {
	        listen 192.168.1.10:80;
	        access_log logs/access.www.example.com.log main;
	        error_log logs/error.www.example.com.log;
	        server_name www.example.com;

	        ## Only allow these request methods ##
	        if ($request_method !~ ^(GET|HEAD|POST)$) {
	                return 444;
	        }

	        ## Proxy - WEB ##
	        location / {

				# 设置忽略的 header
				proxy_ignore_headers   Expires Cache-Control;

				# 设置 header
				proxy_set_header        Host            $host;

				# 转发时带上请求的真实IP
				proxy_set_header        X-Real-IP       $remote_addr;
				proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;

				# 请求转发到另一个server
				proxy_pass http://192.168.1.10:88;

				# 重新设置Cache-Control header
				more_clear_headers  "Cache-Control";
				add_header      Cache-Control "no-cache,max-age=0";

				# index文件, 默认可以不设置
                index index.html;

                # 根目录
                root /tmp/static;
	        }
		}
	}

在同一机器上配置两个域名，直接在http中放两个server就可以了。
*注意：listen 后面直接跟端口号80，不需要域名或IP*
如果80前面一个有IP一个没有的话，有域名的会覆盖没有的（也就是两个域名都会访问到有域名的站点）。
比如 `listen 80  和 listen 192.168.0.55:80`. 一个域名， 一个IP也可以打成平手。

	http{
		server {
			listen 80;
			access_log logs/access.nexus.insqt.com.log ;
			error_log logs/error.nexus.insqt.com.log;
			server_name nexus.insqt.com;

			location / {
				# 请求转发到另一个server
				proxy_pass http://localhost:8081;
			}
		}

		server {
			listen 80;
			access_log logs/access.test.insqt.com.log ;
			error_log logs/error.test.insqt.com.log;
			server_name test.insqt.com;

			location / {
			    # 根目录
				root /tmp/static;
			}
		}
	}


## options.conf
一些默认的 iption 选项

	charset utf-8;

	#Size Limits
	  client_body_buffer_size     512K;
	  client_header_buffer_size   1M;
	#  client_max_body_size          1M;
	  client_max_body_size          20M;
	  large_client_header_buffers 8 8k;
	 
	## Timeouts
	  client_body_timeout   60;
	  client_header_timeout 60;
	  expires               24h;    # 超时时间, 不到这个时间的会返回 304  (not modified)
	  keepalive_timeout     60 60;
	  send_timeout          60;
	 
	## General Options
	  ignore_invalid_headers   on;
	  keepalive_requests      100;
	  limit_zone gulag $binary_remote_addr 5m;
	  recursive_error_pages    on;
	  sendfile                 on;
	  server_name_in_redirect off;
	  server_tokens           off;
	 
	## TCP options
	  tcp_nodelay on;
	  tcp_nopush  on;
	 
	## Compression
	  gzip              on;
	  gzip_buffers      16 8k;
	  gzip_comp_level   6;
	  gzip_http_version 1.1;
	  gzip_min_length   0;
	  gzip_types        text/plain text/css image/x-icon application/x-perl application/x-httpd-cgi application/x-javascript;
	#text/html
	  gzip_vary         on;
	  #gzip_disable "MSIE [1-6].(?!.*SV1)";
	  #gzip_disable "msie6";
	  #gzip_disable "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1)";
	  #gzip_disable ".*MSIE.*";
	  gzip_disable ".*MSIE 6.0.*";
	## Log Format
	  log_format  main  '$remote_addr $host $remote_user [$time_local] "$request" '
	                    '$status $body_bytes_sent "$http_referer" "$http_user_agent" '
	                    '"$gzip_ratio"';




