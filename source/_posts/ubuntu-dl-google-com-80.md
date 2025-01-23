---
title: 'Ubuntu中出现无法连接dl.google.com:80'
tags: []
id: '192'
categories:
  - - LInux
date: 2021-04-27 00:09:52
---

# 系统环境

Ubuntu 20.04

# 问题描述

执行

```
sudo apt-get update
```

命令时，发现出现以下错误：

```
Could not connect to dl.google.com:80 (6.6.6.6), connection timed out
```

# 解决方法

这里通过修改/etc/hosts文件来解决这个问题，先输入

```
vim /etc/hosts
```

在hosts文件下面添加一下内容：

```
#Download 下载 
203.208.41.32 dl.google.com 
203.208.41.32 dl-ssl.google.com

#Groups 
203.208.41.32 groups.google.com

#Google URL Shortener 
203.208.41.32 goo.gl

#Google App Engine 
203.208.41.32 appengine.google.com
```

修改完成后，使ping命令来测试，结果如下图：

![](https://blogjkfff-1302429038.cos.ap-beijing.myqcloud.com/img/pinggoogle.png)

表示问题成功解决，再次sudo apt-get update时成功。