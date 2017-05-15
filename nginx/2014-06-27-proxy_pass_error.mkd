# nginx的listen指令

## 所有域名都被拦截

	listen 80;
	vs
	listen 192.168.1.122:80;
有时候写IP会报502, 有时候不写IP会报502, 这个是什么情况呢

## bad  getway

	server {
	        listen 80;
	        access_log logs/access.nexus.l99.com.log main;
	        error_log logs/error.nexus.l99.com.log;
	        server_name nexus.l99.com;
	        
			# 文件下载一半的问题
			proxy_max_temp_file_size 0;

	        location / {
	                proxy_pass http://192.168.50.124:8080/;
	        }

	}
	# 文件下载一半的问题
	proxy_max_temp_file_size 0;


