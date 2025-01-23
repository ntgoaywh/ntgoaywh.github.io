---
title: 从零开始搭建一个属于自己的博客(纯小白教程)
tags: []
id: '138'
categories:
  - - 建站知识
date: 2021-02-11 01:32:55
---

# 前言

趁着寒假有时间，我回顾了我搭建博客的过程，于是想分享下自己的经验，写一篇小白也能看懂的教程，让每个人都能够搭建属于自己的博客。

# 所需条件

一个博客首先需要一台服务器（VPS/独服），虚拟主机也可以，能将博客托管在上面，同时还需要一个能访问到它的域名，也就是要取一个名字。有了服务器和域名，再加上相关的脚本，一个博客就能成功搭建。

# 搭建过程

## 服务器选购

服务器（VPS）我选择在腾讯云 [https://cloud.tencent.com/](https://cloud.tencent.com/) 购买，这里我选择购买腾讯云的轻量应用服务器。

首先腾讯云的账号自行注册，这里可以使用微信登录并注册，注意要完成实名认证。

![1](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209014036.png)

![2](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209014143.png)

因为使用香港以及国外服务器是不需要备案的，所以这里避免备案以及后续一些不必要的麻烦我们选择购买香港地域的，当然新加坡和硅谷地区也可以，这里还考虑到香港离大陆是最近的，访问速度最快。

镜像方面我们选择系统镜像，具体的系统看个人喜好，我一般选择Debian，注意：因为版权的原因，选择Windows系统是要贵一点的。

![3](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209014608.png)

实例套餐方面，选择最低一档24元一个月的就足够搭建博客了，实例名称随意，购买时长可先选择一个月试试效果，所有选择完后，勾选同意协议，点击立即购买。

![](https://blog.jkfff.com/wp-content/uploads/2021/02/image-20210209014839381-1024x487.png)

点击提交订单

![5](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209130757.png)

选择付款方式，这里我们选择在线支付，可以用微信、QQ钱包、银行卡等支付，方便快捷。

![6](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209130639.png)

点击下一步，跳转到新页面，选择微信扫码支付

![7](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209131013.png)

支付成功后点击返回，再点击进入控制台。

![8](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209131205.png)

![9](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209131308.png)

在控制台我们便可以看到刚刚购买的轻量服务器。

![10](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209131440.png)

点击服务器名称进入管理页面，在这里可以看到服务器的相关信息

![11](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209131650.png)

此时点击远程登录

![11](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209132121.png)

点击重置密码，自己设定一个复杂的密码，避免被人盗用。当然自己也可以绑定一个密钥，更加安全，这个方法之后再说。

![12](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209132215.png)

然后输入新密码，确认新密码，其他保持默认，注意密码的设定规则。

![12](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209132549.png)

密码输入完毕后，点击下一步，勾选同意强制关机，再点击重置密码，等待几分钟便可重置成功。

![13](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209132837.png)

到这里为止，服务器的选购环节算完成了。

## 服务器登录及配置

服务器的登录需要用到SSH工具，这里我们选用FinalShell :[https://www.hostbuf.com/](https://www.hostbuf.com/)

### Win版下载地址

[http://www.hostbuf.com/downloads/finalshell\_install.exe](http://www.hostbuf.com/downloads/finalshell_install.exe)

### macOS下载地址

[http://www.hostbuf.com/downloads/finalshell\_install.pkg](http://www.hostbuf.com/downloads/finalshell_install.pkg)

点击上方链接下载并安装后，打开软件

![14](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209134145.png)

没有其他的需求，免费版的就已经够用了。

![15](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209134359.png)

### 添加服务器

按下图顺序依次点击，然后点击**SSH连接(Linux)。**

![16](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209134625.png)

![17](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210209134910.png)

其他保持默认，最后点击确定，添加好的服务器就会出现在连接管理器的列表里。

![18](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210010159.png)

此时，双击添加的服务器——腾讯云香港，出现下方的界面时点击接受并保存，进入服务器命令行操作界面。

![25](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210012829.png)

![19](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210010709.png)

### 服务器配置

一般拿到服务器，我的习惯是先dd系统，Linux dd系统就相当于Windows里的重装系统，因为有些商家的服务器系统模板有些问题或者有一些监控，这里为了避免出现问题，我们选择dd以更换为一个纯净的Linux系统。

我的博客曾分享过Linux dd的脚本：[\[Linux系统下，一键安装Centos6-7、Debian7-10、Ubuntu14-18、Windows等\](https://ioli.cc/38.html)](https://ioli.cc/38.html)，这里直接拿来使用。

我选择dd Debian10，命令为

```
wget -N --no-check-certificate https://raw.githubusercontent.com/veip007/dd/master/dd-gd.sh && chmod +x dd-gd.sh && ./dd-gd.sh
```

复制以上命令，返回到FinalXshell操作界面，点击鼠标右键选择粘贴。

![20](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210011433.png)

![21](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210011515.png)

然后按下回车键，系统便会自动进入dd流程。

![22](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210011618.png)

当出现镜像包选择时，输入7，选择Debian 10，记住dd完后的服务器密码为**cxthhhhh.com**，然后按下回车键，接下来便是耐心的等待dd完成，系统会自动断开连接。

![23](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210012106.png)

系统断开连接10分钟后再连接，视性能差异时间或长或短，重新连接只需点击操作界面下方的闪电图标，

![24](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210012439.png)

如果dd已经完成，点击闪电图标重新连接会出现安全警告，同样点击接受并保存，若点击后又断开只需再点击闪电图标直到连接上为止。

![26](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210012829.png)

因为dd了系统，服务器的密码发生了改变，需要重新输入密码，此时需输入上方所需要记住的密码**cxthhhhh.com**，但是无需记住密码。

![](https://blog.jkfff.com/wp-content/uploads/2021/02/image-20210210013239856.png)

输入密码后点击确定，会重新进入操作界面，同样的，若出现断开连接现象，只需多点击闪电图标直到连接上为止。

进入后为如下界面。

![27](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210013513.png)

此时输入

```
apt-get update -y
```

来更新下系统。

因为之前的密码太弱而且是公共密码，此时再更改服务器密码，

输入

```
passwd root
```

会让你输入新的密码并重复一遍，更改完成后会显示下图所示的界面。

![28](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210013743.png)

然后点击下方的齿轮图标进入服务器信息编辑界面。

![29](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210013935.png)

按图示操作更改密码并应用保存，然后关闭页面。

![30](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210014402.png)

到此为止服务器的配置工作也算完成了，接下来便是环境的部署。

## 服务器环境部署

### 宝塔面板安装

首先，对于小白我是推荐使用宝塔面板的，搭建网站博客等等操作通过宝塔面板都可以轻松的完成。

进入宝塔官网：[https://www.bt.cn/](https://www.bt.cn/)，点击立即安装。

![31](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210014742.png)

然后会弹出相关的脚本界面。

![32](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210014823.png)

因为服务器是Debian10系统，便复制Debian安装命令。

```
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && bash install.sh
```

然后同样粘贴在命令行操作界面，点击回车，便会自动开始安装宝塔面板。

但此时出现如下错误

![33](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210015050.png)

wget未安装，我们只需输入

```
apt-get install -y wget
```

如果是Centos系统，我们则需输入

```
yum install -y wget
```

等待wget安装后再执行一遍宝塔安装命令，此时再输入y便可成功安装。

![34](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210015307.png)

成功安装便会显示如下界面

![35](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210015657.png)

其中的外网面板地址便是宝塔面板的登录地址，这里我们需要在防火墙处开放8888端口以能正常访问到服务界面。

### 开放防火墙

登录自己的腾讯云，进入控制台，点击轻量应用服务器。

![34](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210152712.png)

再点击服务器名称进入管理界面。

![35](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210152758.png)

点击防火墙，添加规则，在端口处填入8888，点击确定后会添加此条规则。

![35](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210152852.png)

![36](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210152946.png)

![37](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210153050.png)

### 进入宝塔服务界面

在浏览器中输入上面安装宝塔面板后给出的外网登录地址，按下回车会进入登录界面，需要输入账号和密码，也就是前面所给的账号密码，输入完成后点击登录，然后会进入用户协议界面，翻到最下面，勾选**我已阅读并同意“《用户协议》”**，点击进入面板。

![38](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210153436.png)

![39](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210153754.png)

进入后会自动跳出推荐安装套件，这里我们选择左边的LNMP，把PHP的版本调成最新的PHP7.4，其他的保持不变，然后点击一键安装，此时后台就会自动开始安装LNMP。

![40](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210154123.png)

点击一键安装后会弹出消息盒子，这里我们可以知道安装的进度，然后点击右上角关闭页面。

![41](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210154308.png)

关闭消息盒子后会提示让我们强制绑定宝塔官网账号，这里我们可不绑定，用一行命令即可关闭强制登录。

在服务器的命令行操作界面，执行以下脚本，解决强制登录提醒。

```
rm -f /www/server/panel/data/bind.pl
```

![42](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210154639.png)

执行完毕后，刷新网页，强制登录的提示就没有了，此时耐心等待LNMP的安装即可。

安装完成后在消息盒子处可看到各项任务完成时间。

![43](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210224332.png)

## 域名购买

LNMP一般安装需要一些时间，趁这个时间我们去选购一个域名，同样登录腾讯云，打开首页，将鼠标放在产品上，并点击域名注册这一选项。

![43](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210225535.png)

搜索一个自己喜欢并且没有被注册的域名，挑选好后缀，将其加入购物车，最后购买付款，注意购买的域名需要实名认证，这里填写好自己的个人信息即可。

![44](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210225652.png)

### 域名解析

只有将一个域名解析到服务器的IP上，我们才能够通过域名访问到我们的博客，这里使用DNSPOD进行域名解析。

[腾讯云-控制台 (tencent.com)](https://console.cloud.tencent.com/cns)

进入DNS解析控制台，选择好域名，点击解析，进入解析页面。

![45](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210231430.png)

这里我们将这个主域名解析到我们的服务器IP上，具体步骤参考我下面给出的图。

![46](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210231827.png)

不同的主机记录对应不同的域名，主机记录为@是主域名，其余的记录均为子域名。

完成以上步骤后，等待10分钟就会解析成功。同时按下Win键+S，然后在出现的搜索框中输入cmd打开命令提示符，在命令提示符中输入

ping+空格+我们所解析的域名

若成功返回为服务器的IP，则说明我们的域名解析已经完成。

![45](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210234435.png)

## 添加网站

进入宝塔面板管理界面，点击网站。

![46](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210234944.png)

添加站点，按下图步骤进行，要记好数据库名、用户名和数据库密码。

![47](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210235244.png)

![47](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210235407.png)

添加完站点后，部署SSL证书，点击未部署，具体操作按下图所示。

![](https://blog.jkfff.com/wp-content/uploads/2021/02/image-20210210235525402-1024x57.png)

![48](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210210235631.png)

Let's Encrypt证书是免费的SSL证书，有效期为三个月，在宝塔面板上申请该证书三个月到期后会自动续期。

申请完证书后，勾选右上角的强制HTTPS，使得网站打开时能够出现一把锁。

关闭证书申请页面，进入网站根目录。

![47](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211000825.png)

博客的类型我们选择WordPress，进入WordPress官网的下载页面：[下载 WordPress.org China 简体中文](https://cn.wordpress.org/download/)

复制最新版本的下载链接：[https://cn.wordpress.org/latest-zh\_CN.zip](https://cn.wordpress.org/latest-zh_CN.zip)

点击远程下载，下载最新版本的WordPress。

![](https://blog.jkfff.com/wp-content/uploads/2021/02/image-20210211001853574-1024x524.png)

选择下载的压缩包，点击选项“解压”。

![50](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211002007.png)

![51](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211002234.png)

点击进入解压出来的文件夹。

![52](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211002406.png)

全选文件，复制所有文件。

![53](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211003325.png)

再返回到网站根目录，点击粘贴。

![54](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211003446.png)

![55](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211003544.png)

粘贴完成后，基本步骤已经全部完成。

### 添加伪静态

点击网站设置，设置伪静态。

![63](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211010132.png)

## 进入博客

在浏览器的地址栏输入博客的域名，回车后会进入WordPress的配置页面。

![56](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211004010.png)

点击现在就开始，会让我们输入数据库名等信息。

![57](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211004314.png)

若已忘记，可点击宝塔面板管理界面的数据库，在那可查看数据库的信息。

![58](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211004423.png)

信息填完后，点击提交，再点击现在安装，最后给博客取一下名字，点击安装WordPress。

![59](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211004608.png)

![60](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211004846.png)

安装完成后，点击登录，输入刚才设定的用户名和密码，最后再点击登录。

![61](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211005141.png)

![62](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211005223.png)

登录后会进入博客的后台管理界面，点击文章可以自己写文章，WordPress的玩法很多，其他的操作便由自己去探索。

![63](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211005345.png)

### 更换博客主题

首先去网上找一个自己觉得好看的主题，这里我推荐一个 [mashirozx/Sakura: A Wonderful WordPress Theme: 樱花庄的白猫博客主题 (github.com)](https://github.com/mashirozx/Sakura)

在release界面可下载最新的安装包：[下载链接](https://github.com/mashirozx/Sakura/archive/v3.3.9.zip)

进入网站根目录，点击wp-content，再点击themes，再点击远程下载，复制主题包的下载链接，点击确认。

![65](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211010844.png)

![66](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211011009.png)

下载完成后解压。

![67](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211011124.png)

进入博客后台界面，点击外观，再主题页面选择我们下载的主题Sakura，点击启用。

![68](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210211011437.png)

此时再打开我们的博客地址，主题已经发生了改变。其余各式各样的配置参考主题作者所写的文章：[WordPress 主题 Sakura ? 樱花庄的白猫 (2heng.xin)](https://2heng.xin/theme-sakura/#toc-head-30)

# 后记

依次完成以上步骤，一个博客便能成功搭建。在如今微博、知乎、B站、抖音等平台能让我们方便记录生活或学习的情况下，我觉得拥有一个自己的博客是一个非常有意义的事情，在自己的博客上可以畅所欲言，不用受这些平台的约束，自己想写什么就写什么。

这篇文章拖了快两周，总算在除夕的这天凌晨完成，也算是一个年度经验总结。