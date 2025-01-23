---
title: (转载)网站使用CloudFlare自选节点IP教程，免费CDN加速VPS
tags: []
id: '98'
categories:
  - - 服务搭建
date: 2021-01-26 21:12:38
---

网站套CloudFlare自选ip节点教程！很多站长注册使用CloudFlare免费CDN加速网站全球访问速度，还带防御功能，隐藏服务器真实IP。但是CF自动分配的IP比较慢。所以我们利用CloudFlare Partner 和Dnspod来自定义节点优化加速效果。

## 使用CFP，CNANE方式接入CF

CFP是指Cloudflare Partner，第三方合作伙伴。如果在Cloudflare官网添加网站，必须把域名的NS地址改成CF官方的。使用CFP的话可以通过CNAME方式接入CF，然后自选IP。

先到Cloudflare.com注册一个账号。本文以笨牛网CFP面板为例，到笨牛网CFP面板： [https://cdn.bnxb.com](https://cdn.bnxb.com/) 直接用CF账号登录，笨牛网是汉化的CFP设置面板，网站CDN加速其实是Cloudflare官方提供。

登录后，如下图：域名接入—添加域名：比如 主域名：pigji.com 子域名：www.pigji.com  
![img](https://cdn.jsdelivr.net/gh/couldbeloveu/newimg/cloudflare/bnxb2.png)

然后点击菜单 ：域名列表，就可以看到刚刚添加的域名呢。  
![img](https://cdn.jsdelivr.net/gh/couldbeloveu/newimg/cloudflare/bnxb3.png)

点击域名进入下图所示界面，点击 解析设置，可以看到域名原本的A记录解析。强调：全部删除重新添加自己需要的A记录。回源地址就是你网站服务器主机的IP地址  
![img](https://cdn.jsdelivr.net/gh/couldbeloveu/newimg/cloudflare/bnxb4.png)  
添加完成，页面下方会给出Cloudflare提供的CNAME记录值。

然后我们就需要到DNSPOD添加CNAME记录呢。

## DNSPOD解析准备

不是强制用Dnspod.cn，只要可以分国内、国外线路解析域名的DNS服务商就行，比如 华为DNS，DNS.com等。本文以DNSPOD为例。

假如域名在国外注册，登录域名管理后台，修改域名NS地址为dnspod的NS地址，如下图：  
![img](https://cdn.jsdelivr.net/gh/couldbeloveu/newimg/cloudflare/bnxbgains.png)

然后回到DNSPOD添加你的域名就行，这样你的域名的解析权就转移到DNSPOD来了。  
然后我们按CFP提供的值，添加CNAME记录，如下图：

![img](https://cdn.jsdelivr.net/gh/couldbeloveu/newimg/cloudflare/bnxb7.png)

## 回到CFP面板设置相关参数

回到笨牛CFP面板这边，点击：主要设置，开始设置CloudFlare的加速与防御功能，如下图：  
![img](https://cdn.jsdelivr.net/gh/couldbeloveu/newimg/cloudflare/bnxb5.png)  
如果是静态网站可以全站缓存，如果是WP，DISCUZ就按上图我这样的来吧。

还有防火墙：IP黑名单、IP白名单，UA屏蔽、防CC等功能，自行探索。高级设置懂的就按需设置，不懂的默认就行。

然后去 ping.chinaz.com检测一下，看看自己域名的解析IP是不是变成Cloudflare的呢。  
这样的好处就是你的真实IP隐藏起来了。

## 最重要的 自选节点IP

一旦你成功套上cloudflare后，下一步你就可以利用DNSPOD分线路解析的功能开始自选IP。  
默认线路是 CF的CNAME记录，不要修改。  
然后我们添加境内线路，和移动线路的A记录  
等于境内（电信联通）+移动，自定义IP，如下图  
![img](https://cdn.jsdelivr.net/gh/couldbeloveu/newimg/cloudflare/bnxb6.png)

哪些Cloudflare的节点IP适合国内用户，自己去寻找呢，下方有推荐部分IP， 也有提供CF的所有节点IP段。

## 推荐节点IP，有可能失效

**电信推荐节点：洛杉矶 圣何塞**  
104.16.160.1-104.16.160.254  
104.19.150.1-104.19.150.254

**电信推荐节点 CF与百度合作**  
162.159.208.4-162.159.208.103  
162.159.209.4-162.159.209.103  
162.159.210.4-162.159.210.103  
162.159.211.4-162.159.211.103

**联通推荐节点**  
联通不好找，随电信的IP吧  
104.19.150.1-104.19.150.254

**移动推荐节点：走香港**  
141.101.115.1 - 141.101.115.254  
172.64.32.1 - 172.64.32.254  
198.41.214.1 - 198.41.214.254  
104.25.176.1 - 104.25.176.254  
104.18.177.1 - 104.18.177.254

**其它推荐节点**  
104.23.128.14  
104.22.32.14  
104.24.32.14  
172.67.96.14  
198.41.208.14

注意：移动部分地区，CF节点被运营商阻断，导致网站有时无法访问。如果出现移动线路无法访问，可把移动线路解析到： 1.0.0.1

## 来自网友的测试cloudflare优秀IP

网友测试地点是长三角地区，时间为傍晚，不同地区和时间测试有差异。

##### 电信

大多数都是走 LAX洛杉矶  
已知的例外：  
104.16.32.0 - 104.16.63.255 SJC  
104.16.144.0 - 104.16.159.255 SJC  
104.18.16.0 - 104.18.31.255 SJC  
103.21.244.0/24 FRA 或 DUS  
162.159.36.0/24 SJC  
162.159.46.0/24 SJC  
162.159.128.0 - 162.159.200.0 AMS 、FRA 、LHR  
198.41.211.0/24 LHR

不同 IP 的下载速率差异较大，中位数为 150KB/s  
顺便一提，测试中只有电信 4G 的 1.1.1.0/24 是不通的

##### 联通

大多数可访问段来自 LAX洛杉矶

已知的例外：  
104.16.32.0 - 104.16.63.255 SJC  
104.17.0.0 - 104.17.15.255 SJC  
104.19.144.0 - 104.19.159.255 SJC  
104.20.0.0/16 SJC  
104.22.0.0 - 104.22.63.255 SJC  
104.22.64.0 - 104.22.79.255 FRA  
104.23.96.0 - 104.23.143.255 SJC  
104.24.0.0/16 MUC 、SJC 、LAX  
104.26.0.0/16 SJC  
104.27.0.0/16 MUC 、SJC 、SEA 、FRA  
172.67.0.0/16 SJC 、FRA 、LAX  
103.21.244.0/24 SJC  
141.101.113.0/24 SJC  
162.159.36.0/24 SJC  
162.159.46.0/24 SJC  
162.159.160.0/24 LHR  
162.159.224.0 - 162.159.239.0 MUC

不同 IP 的下载速率差异较小，中位数为 250KB/s，SJC 、MUC 平均较快

##### 移动

可访问段来自的地域比较零散

1.0.0.0/24 LAX  
1.1.1.0/24 LAX

104.16.0.0/12 大多数为 LAX 、SJC 交替出现  
在此基础上，还会参杂有：  
104.16.0.0/16 HKG 、SEA  
104.17.0.0/16 HKG 、SEA  
104.18.0.0/16 FRA 、HKG 、SEA  
104.19.0.0/16 HKG  
104.20.0.0/16 SIN  
104.24.0.0/16 SIN  
104.26.0.0/16 SEA  
104.31.0.0/16 SEA

172.64.0.0/13 大多数为 LAX 、SJC 交替出现  
除了 172.64.64.0 - 172.64.79.0 为 HKG

103.21.244.0/24 SJC  
141.101.64.0/18 SJC 、LAX 、HKG  
162.158.0.0/15 SJC 、LAX  
173.245.48.0/20 LAX  
190.93.240.0/20 HKG  
198.41.128.0/17 SJC 、LAX 、HKG

不同 IP 速率差异较大，中位数为 73KB/s，  
SEA 平均较快，个别 HKG 速度很快

## CloudFlare官方公布的所有节点IP

官方节点更新地址：  
https://www.cloudflare.com/zh-cn/ips

IPv4  
173.245.48.0/20  
103.21.244.0/22  
103.22.200.0/22  
103.31.4.0/22  
141.101.64.0/18  
108.162.192.0/18  
190.93.240.0/20  
188.114.96.0/20  
197.234.240.0/22  
198.41.128.0/17  
162.158.0.0/15  
104.16.0.0/12  
172.64.0.0/13  
131.0.72.0/22  
Also available as a [IPv4 text list](https://www.cloudflare.com/ips-v4).

IPv6  
2400:cb00::/32  
2606:4700::/32  
2803:f800::/32  
2405:b500::/32  
2405:8100::/32  
2a06:98c0::/29  
2c0f:f248::/32  
Also available as a [IPv6 text list](https://www.cloudflare.com/ips-v6).

## 其他第三方CFP站点

https://cdn.moeelf.comhttps://cf.tlo.xyz

## 部分垃圾域名无法使用CF的服务

部分免费域名被Cloudflare嫌弃，如 .ga, .gq, .ml, .tk 等垃圾后缀域名无法使用CF，被限制使用。  
去Namesilo.com 买6位数字的.xyz域名特别便宜，com域名也才8刀多，使用优惠码 NEW2020 首单还能优惠1美元。

## 套CloudFlare后获取用户真实IP地址

适合宝塔面板 + Nginx，修正网站日志里面访客IP为CDN节点IP的问题。

宝塔面板后台—Nginx设置—配置修改  
找到

```
include proxy.conf;
```

在其上方添加：

```
set_real_ip_from 0.0.0.0/0;
real_ip_header X-Forwarded-For;
```

![img](https://cdn.jsdelivr.net/gh/couldbeloveu/newimg/cloudflare/bnxbrealip1.png)

然后记得重载Nginx配置就行，或者重启。

原文来自：[https://www.pigji.com/598.html](https://www.pigji.com/598.html)