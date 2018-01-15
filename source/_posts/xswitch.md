---
title: xswitch
date: 2018-01-16 01:41:40
tags: 
- xswitch
- Chrome Extension
- Proxy
- Forwading
---

[![Build Status](https://travis-ci.org/yize/xswitch.svg?branch=master)](https://travis-ci.org/yize/xswitch)

## 解决的痛点

* 在开发和调试过程中，经常需要把线上或者日常环境的 CSS、JS 转发到本地，Charles 等本地代理工具，特别是在全网 HTTPS 化后，变得更加复杂和繁琐。
* 现有的 Chrome 插件，交互形式，对程序员不是很友好，无法解决快速定位到某一条规则、快速开关组的需求。
* [anyproxy](https://github.com/alibaba/anyproxy) 是不错的工具，但是在浏览器转发上，配置起来相对麻烦。

## XSwitch 的优势

* 基于 Chrome Extension，即装即用。不需要额外配置其他环境。
* 基于 [Monaco Editor](https://github.com/Microsoft/monaco-editor)，可以使用编辑器带来的快捷操作方式。
* 可以写 JSON 注释。
* 即时保存，即时生效。
* 自动提示页面上加载到的资源文件，作为提醒（目前只抓取了 http(s) 的地址，其他协议的忽略了）
* [Open Source](https://github.com/yize/xswitch)

## 功能

如果设定了如下规则：

![](https://img.alicdn.com/tfs/TB1roVJmRfH8KJjy1XbXXbLdXXa-1672-944.png)

访问：[https://g.alicdn.com/platform/daily-test/isDaily.js](https://g.alicdn.com/platform/daily-test/isDaily.js)

会进行如下转发：

![](https://img.alicdn.com/tfs/TB1HH6emLDH8KJjy1XcXXcpdXXa-3048-1922.png)

### 支持自动提示

![](https://img.alicdn.com/tfs/TB1vLPBmH_I8KJjy1XaXXbsxpXa-1672-944.png)

![](https://img.alicdn.com/tfs/TB1oRfdmLDH8KJjy1XcXXcpdXXa-1672-944.png)

### 支持正则匹配

[https://github.com/yize/xswitch/blob/master/test/index.spec.js](https://github.com/yize/xswitch/blob/master/test/index.spec.js)

```json
{
  // proxyRules
  "proxy": [
    [
      "//g.alicdn.com/platform/daily-test/(.*).js$",
      "//g.alicdn.com/platform/daily-test/$1.json"
    ],
    ["g.alicdn.com", "alinw.alicdn.com"]
  ]
}
```

## Logo

> 像是程序员的发际线

![](https://img.alicdn.com/tfs/TB1JIIzmvDH8KJjy1XcXXcpdXXa-1918-832.png)

希望 XSwitch 能够给大家带来帮助或者想法。

欢迎[试用](https://chrome.google.com/webstore/detail/idkjhjggpffolpidfkikidcokdkdaogg)，欢迎[提意见](https://github.com/yize/xswitch/issues)。

## Links

* [前往 Chrome Web Store 下载](https://chrome.google.com/webstore/detail/idkjhjggpffolpidfkikidcokdkdaogg)
* [XSwitch - Github](https://github.com/yize/xswitch)
