---
title: hexo-from-octopress
date: 2016-02-20 19:13:48
categories : 
- Stack
tags:
- Hexo
- Octopress
- Docker
- Nginx
---

# hexo 建站

## 安装：

### node

> hasNode && skipThis;

Linux install node , [nodejs docs](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions):

```bash
$ curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
$ sudo apt-get install -y nodejs
```

### install hexo-cli

```bash
$ npm install -g hexo-cli
```

## 配置

### 初始化 hexo

```bash
$ hexo init blog
$ cd blog
$ npm install
```

### install NexT 主题

[知乎](https://www.zhihu.com/question/24422335/answer/46357100)上看到这个主题，还不错。

```bash
$ cd your-hexo-site
$ git clone https://github.com/iissnan/hexo-theme-next next
```

see [theme-NexT-five-minutes-setup.html](http://theme-next.iissnan.com/five-minutes-setup.html)

<!--more-->

### 从 Octopress 迁移到 Hexo

把 Octopress `source/_posts` 文件夹内的所有文件转移到 Hexo 的 `source/_posts` 文件夹，并修改 _config.yml 中的 new_post_name 参数。

```
new_post_name: :year-:month-:day-:title.md
```

## tips

### 阅读全文语法

```html
<!--more-->
```

### 同步到 github

在 Github 上新建项目，在 blog 文件下配置：

```bash
$ git init
$ git remote add origin git@github.com:yize/blog.git
```

## 部署

启动模式有几种：

1. 只使用 `hexo` 启动

	```bash
	$ docker pull wzpan/hexo:v3
	$ docker run --rm -p 80:4000 -v YOUR_LOCAL_BLOG_DIR:/root/blog wzpan/hexo:v3
	```
	
	这样可以直接占用 `80` 端口。

2. Use nginx-proxy （推荐）

	通过 [nginx-proxy](https://hub.docker.com/r/jwilder/nginx-proxy/) 让我们的反向代理变的更加简单：
	
	```bash
	$ docker run -d -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock:ro jwilder/nginx-proxy
	```
	
	```bash
	$ docker run -e VIRTUAL_HOST=www.ithans.com --rm -v YOUR_LOCAL_BLOG_DIR:/root/blog wzpan/hexo:v3
	```
	
	nginx-proxy 会自动寻找容器的 Port ，然后做好 nginx 的 proxy：大概的实现是：
	
	1. 通过 Docker API 获取 containers 的 `IP`、`Port` 以及其他配置项
	
		手动查询方法：
		
		```bash
		$ docker ps #查询启动的容器
		$ docker inspect YOUR_CONTAINER_ID #查询容器信息（包括 IP）
		```
		
	2. 通过 [docker-gen](https://github.com/jwilder/docker-gen) 生成 Nginx config：
	
		```Nginx
		upstream www.ithans.com {
		    server 172.17.0.1:4000;
		}
		
		server {
		    #ssl_certificate /etc/nginx/certs/demo.pem;
		    #ssl_certificate_key /etc/nginx/certs/demo.key;
		
		    gzip_types text/plain text/css application/json application/x-javascript
		               text/xml application/xml application/xml+rss text/javascript;
		
		    server_name www.ithans.com;
		
		    location / {
		        proxy_pass http://www.ithans.com;
		        include /etc/nginx/proxy_params;
		    }
		}
		
		upstream  {
		    server 172.17.0.1:4000;
		}
		
		server {
		    #ssl_certificate /etc/nginx/certs/demo.pem;
		    #ssl_certificate_key /etc/nginx/certs/demo.key;
		
		    gzip_types text/plain text/css application/json application/x-javascript
		               text/xml application/xml application/xml+rss text/javascript;
		
		    server_name www.ithans.com;
		
		    location / {
		        proxy_pass http://www.ithans.com;
		        include /etc/nginx/proxy_params;
		    }
		}
		```
		
	3. 直接通过 `hexo server` 启动

## links
- [hexo](https://hexo.io)
- [docker nginx-proxy](https://hub.docker.com/r/jwilder/nginx-proxy/)
- [docker wzpan/hexo](https://hub.docker.com/r/wzpan/hexo/)
- [hexo-in-the-docker](https://blog.jamespan.me/2015/04/17/hexo-in-the-docker/)
- [automated-nginx-reverse-proxy-for-docker](http://jasonwilder.com/blog/2014/03/25/automated-nginx-reverse-proxy-for-docker/)
- [hexo-NexT setup](http://theme-next.iissnan.com/five-minutes-setup.html)



