---
title: hexo-from-octopress
date: 2016-02-20 19:13:48
categories : 
- Stack
tags:
- Hexo
---

# hexo 建站

## 安装：

### node

Linux install node , [nodejs docs](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions):

```bash
curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### install hexo-cli

```bash
$ npm install -g hexo-cli
```

## 配置

### 初始化 hexo

```bash
hexo init blog
cd blog
npm install
```

### install NexT 主题

[知乎](https://www.zhihu.com/question/24422335/answer/46357100)上看到这篇主题，很不错。


## tips

### 首页的出现阅读全文切割

```md
<!--more-->
```

### 同步到 github

在 Github 上新建项目，在 blog 文件下配置：

```bash
git init
git remote add origin git@github.com:yize/blog.git
```

add -> commit -> push


## links

- [https://blog.jamespan.me/2015/04/17/hexo-in-the-docker/](https://blog.jamespan.me/2015/04/17/hexo-in-the-docker/)


