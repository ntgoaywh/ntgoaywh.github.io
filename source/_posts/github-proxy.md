---
title: 如何提高国内访问GitHub的速度达到3MB/S以上（轻松解决）
tags: []
id: '223'
categories:
  - - 服务搭建
date: 2021-05-07 00:03:33
---

**为什么GitHub下载速度这么慢？**

GitHub，我们都知道是世界上最大的开源及私有软件项目的托管平台，全世界每天有海量优秀的开源软件在这里产生，而 GitHub 在国内很多时候获取到的下载链接是亚马逊的服务器。

中国因为不可言说的原因，经常抽疯或龟速。想要加快 GitHub 下载速度就需要用到 GitHub 国内加速服务，对于有条件的可以使用代理加快访问速度，而没有条件的就可以用到以下解决方案，实现加速：

*   1.GitHub 镜像访问
*   2\. GitHub文件加速
*   3\. Github 加速下载
*   4\. 加速你的 Github
*   **5\. 谷歌浏览器GitHub加速插件(推荐)**
*   6\. GitHub raw 加速
*   7\. GitHub + Jsdelivr
*   8\. 通过Gitee中转fork仓库下载
*   9\. 通过修改HOSTS文件进行加速

详细说明：

## 1\. GitHub 镜像访问

这里提供两个最常用的镜像地址：

*   [github.com.cnpmjs.org](https://github.com.cnpmjs.org)
*   [hub.fastgit.org](https://hub.fastgit.org)

也就是说上面的镜像就是一个克隆版的 GitHub，你可以访问上面的镜像网站，网站的内容跟 GitHub 是完整同步的镜像，然后在这个网站里面进行下载克隆等操作。

## 2\. GitHub 文件加速

利用 Cloudflare Workers 对 github release 、archive 以及项目文件进行加速，部署无需服务器且自带CDN.

*   [gh.api.99988866.xyz](https://gh.api.99988866.xyz)
*   [g.ioiox.com](https://g.ioiox.com)

以上网站为演示站点，如无法打开可以查看开源项目：gh-proxy-GitHub([hunsh.net/archives/23…](https://hunsh.net/archives/23/)) 文件加速自行部署。

## 3\. Github 加速下载

打开以下网站，只需要复制当前 GitHub 地址粘贴到输入框中就可以代理加速下载！

地址：[toolwa.com/github/](http://toolwa.com/github/)

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210506235642.png)

## 4\. 加速你的 Github

[github.zhlh6.cn](https://github.zhlh6.cn)

输入 Github 仓库地址，使用生成的地址进行 git ssh 等操作

## 5\. 谷歌浏览器 GitHub 加速插件(推荐-方便快捷)

如果可以直接访问谷歌商店，可以下载GitHub 加速工具，安装。

不方便的可以这里下载安装：

链接：[pan.baidu.com/s/1b3xzNrJb…](https://pan.baidu.com/s/1b3xzNrJbkl3Q3N-n9gQW6A) 

提取码：tm97

## 6\. GitHub raw 加速

GitHub raw 域名并非 github.com 而是 raw.githubusercontent.com，上方的 GitHub 加速如果不能加速这个域名，那么可以使用 Static CDN 提供的反代服务。

将 raw.githubusercontent.com 替换为 raw.staticdn.net 即可加速。

## 7\. GitHub + Jsdelivr

jsdelivr 唯一美中不足的就是它不能获取 exe 文件以及 Release 处附加的 exe 和 dmg 文件。

也就是说如果 exe 文件是附加在 Release 处但是没有在 code 里面的话是无法获取的。所以只能当作静态文件 cdn 用途，而不能作为 Release 加速下载的用途。

## 8\. 通过 Gitee 中转 fork 仓库下载

网上有很多相关的教程，这里简要的说明下操作。

访问 gitee 网站：[gitee.com/](https://gitee.com/) 并登录，在顶部选择“从 GitHub/GitLab 导入仓库” 如下：

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/1.png)

在导入页面中粘贴你的Github仓库地址，点击导入即可：

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/2.png)

等待导入操作完成，然后在导入的仓库中下载浏览对应的该 GitHub 仓库代码，你也可以点击仓库顶部的“刷新”按钮进行 Github 代码仓库的同步。

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/3.png)

## 9\. 通过修改 HOSTS 文件进行加速

手动把cdn和ip地址绑定。

第一步：获取 github 的 global.ssl.fastly 地址访问：[github.global.ssl.fastly.net.ipaddress.com/#ipinfo](http://github.global.ssl.fastly.net.ipaddress.com/#ipinfo) 获取cdn和ip域名：

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210507000053.png)

得到：199.232.69.194 [github.global.ssl.fastly.net](https://github.global.ssl.fastly.net)

第二步：获取github.com地址

访问：[github.com.ipaddress.com/#ipinfo](https://github.com.ipaddress.com/#ipinfo) 获取cdn和ip：

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210507000142.png)

得到：140.82.114.4 [github.com](http://github.com)

第三步：修改 host 文件映射上面查找到的 IP

windows系统：

1、修改C:\\Windows\\System32\\drivers\\etc\\hosts文件的权限，指定可写入：右击->hosts->属性->安全->编辑->点击Users->在Users的权限“写入”后面打勾。如下：

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/4.png)

然后点击确定。

2、右击->hosts->打开方式->选定记事本（或者你喜欢的编辑器）->在末尾处添加以下内容：

1.  `199.232.69.194 github.global.ssl.fastly.net`
2.  `140.82.114.4 github.com`