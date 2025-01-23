---
title: 【开源】CF Worker KV 短链接/短网址程序
tags: []
id: '147'
categories:
  - - 服务搭建
date: 2020-12-10 22:42:00
---

很多时候网址过长不利于分享，将长网址转换短网址/短链接，缩短内容长度，会使得分享更加方便。 借助免费的Cloudflare Worker和前不久新添加的kv免费额度可以搭建属于我们自己的长网址转换短网址程序。

## 一.项目开源地址

[https://github.com/xyTom/Url-Shorten-Worker](https://github.com/xyTom/Url-Shorten-Worker)
<!-- more -->
注意：KV有免费额度限制，每天只能写1000次

## 二.搭建教程

### 1.首先去[https://workers.cloudflare.com/](https://workers.cloudflare.com/) 注册一个账号。

### 2.去Workers KV中创建一个命名空间。

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20201205232805.png)

### 3.去Worker的Settings选选项卡中绑定KV Namespace，其中Variable name填写LINKS, KV namespace填写你刚刚创建的命名空间

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20201205232536.png) ![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20201205232704.png)

### 4.复制本项目中的`index.js`的代码到Cloudlare Worker，点击Save and Deploy。