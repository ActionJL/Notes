##### 基础安装 (Ubuntu为例)

```shell
$ sudo apt-get update
$ sudo apt-get install nginx
```

- *端口冲突： 关闭占用80端口的服务*
- *权限问题：sudo权限*

##### 防火墙相关设置

```shell
$ sudo ufw app list
```

- 可用应用程序配置文件的列表
  - CUPS
  - Ningx Full
  - Nginx HTTP
  - Nginx HTTPS
  - OpenSSH
- 浏览器端口：
  - 80：HTTP
  - 443： HTTPS
- Nginx Full: 此配置文件打开端口80 (正常，未加密的网络流量) 和端口443 （TLS/SSL加密流量）
- Nginx HTTP: 此配置文件仅打开端口80 （正常，未加密的网络流量）
- Ningx HTTPS: 此配置文件仅打开443（TLS/SSL加密流量）
- sudo ufw allow 'Nginx HTTP'        允许防火墙通过HTTP请求
- sudo ufw allow 'Nginx HTTPS'      允许防火墙通过HTTPS请求



- 开启防火墙
  - sudo ufw enable
  - sudo ufw status

##### web服务器

- sudo systemctl status nginx
- http://本机IP地址

##### 管理nginx进程

- sudo systemctl stop nginx	    停止nginx服务器
- sudo systemctl start nginx        开启nginx服务器
- sudo systemctl restart nginx    重启ningx服务器
- sudo systemctl reload nginx     重载nginx配置
- sudo systemctl disable nginx   
- sudo systemctl enable nginx

##### 设置服务器模块

- 默认服务器模块
  - /var/www/html/
- sudo mkdir -p /var/www/example.com/html
- sudo chown -R $USER:$USER /var/www/example.com/html/
- sudo chmod -R 755 /var/www/example.com/

```html
<!--/var/www/example.com/html/index.html-->
<html>
    <head>
        <title>Welcome to Example.com!</title>
    </head>
    <body>
        <h1>Success!  The example.com server block is working!</h1>
    </body>
</html>
```

```nginx
server {
        listen 80;	# 监听端口
        listen [::]:80;
 
        root /var/www/example.com/html;	# 监听模块
        index index.html index.htm index.nginx-debian.html;	# 监听的文件名
 
        server_name example.com www.example.com;	# 监听的域名
 
        location / {
                try_files $uri $uri/ =404;
        }
}
```

- sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
- 现在启用两个服务器模块并将其配置为基于listen和server_name指令响应请求
  - example.com: 将响应example.com和www.example.com请求
  - default: 将响应端口80与其他两个块不匹配的任何请求
- sudo nginx -t
- sudo systemctl restart nginx

##### Nginx重要的文件和目录

- /etc/nginx: Nginx配置目录，所有的Nginx配置文件都驻留在这里
- /etc/nginx/nginx.conf: 主要的Nginx配置文件。这可以修改，以更改Nginx全局配置
- /etc/nginx/sites-available/: 可存储每个站点服务器块的目录。除非将Nginx连接到sites-enabled目录，否则Nginx不会使用此目录中的配置文件。通常，所有服务器配置都在此目录中完成，然后通过链接到其他目录启用
- /etc/nginx/sites-enabled/: 存储启用的每个站点服务器块的目录，通常，这些是通过链接到sites-available目录中的配置文件创建的
- /etc/nginx/snippets: 这个目录包含可以包含在Nginx配置其他地方的配置片段，可重复配置的片段可以重构为片段
- /var/log/nginx/access.log: 除非Nginx配置为其他方式，否则每个对您的Web服务器的请求都会记录在此日志文件中
- /var/log/nginx/error.log: 任何Nginx错误都会记录在这个日志中

##### nginx.conf完整配置

```nginx
#user nobody
worker_processes 1;

events {
	worker_connections 1024;
}

http {
	include		mime.types;
	default_type application/octet-atream;
	sendfile 	on;

	keepalive_timeout	65;

	grip on;
	
	server {
		listen		80;
		server_name manage.leyou.com;

		proxy_set_header X-Forwarded-Host $host;
		proxy_set_header X-Forwarded-Server $host;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

		location / {		# 拦截域名下的所有路径
			proxy_pass http://10.141.7.121:9001;	# 主机地址下的9001端口
			proxy_connect_timeout 600;
			proxy_read_timeout 600;
		}
	}

	server {
		listen 		80;
		server_name api.leyou.com;

		proxy_set_header X-Forwarded-Host $host;
		proxy_set_header X-Forwarded-Host $host;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

		location / {
			proxy_pass http://10.141.7.121:10010;
			proxy_connect_timeout 600;
			proxy_read_timeout 600;
		}
	}
}
```

