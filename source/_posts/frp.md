---
title: 利用腾讯轻量服务器搭建FRP服务
tags: []
id: '75'
categories:
  - - 服务搭建
date: 2021-01-25 19:30:17
---

在如今这个IPV4缺乏的年代，家庭宽带获取到公网IPV4相对比较困难，特别是移动用户，基本上就是默认不给公网IPV4，这时候，如果我们想要把内网的资源映射到公网上去，可能会需要用到内网穿透。而FRP就是提供这种服务的一种工具废话少说，现在开始进入正题。

# 一.腾讯轻量服务器购买

对于预算较低的用户，香港地区24的轻量还是非常推荐的，[点此购买。](https://buy.cloud.tencent.com/lighthouse?region=5&blueprintType=PURE_OS&blueprintId=lhbp-8l0svqtk&bundleId=bundle_linux_sml1_1t)

![购买界面](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210122001444.png)

这边我们选择系统镜像，我们以centos8为例。

# 二.开启端口

在腾讯云防火墙开启相应端口（以映射web服务为例，开启80端口，默认已经开启）。

![端口](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210122001639.png)

# 三.远程登录服务器，下载源码（以最新版为例)

```
wget https://github.com/fatedier/frp/releases/download/v0.35.0/frp_0.35.0_linux_amd64.tar.gz
```

# 四.解压并编辑配置文件

```
tar -zxvf frp_0.35.0_linux_amd64.tar.gz
```

```
cd frp_0.35.0_linux_amd64
```

```
vi frps.ini
```

```
#修改frps.ini内容如下：
[common]
​
# frp server的工作端口，默认7000，可以更改
bind_port = 7000
​
# http和https的端口定义
vhost_http_port = 80
vhost_https_port = 443
​
# 连接时需要的认证token，类似于密码，可选填
#token = 000000
​
# 子域名，可选填
# subdomain_host = frps.com
​
# 404 页面
custom_404_page = /root/frp_0.31.1_linux_amd64/404.html
​
# dashboard图形管理页面使用端口
dashboard_port = 7500
​
# dashboard帐号
dashboard_user = admin
# dashboard登陆密码，可以自己修改，这里用admin
dashboard_pwd = admin
```

并按照配置要求开放防火墙端口（此处为7000）。

# 五.设置开机启动

## 添加systemd配置文件：

```
vim /usr/lib/systemd/system/frp.service
```

文件内容如下：

```
[Unit]Description=The nginx HTTP and reverse proxy serverAfter=network.target remote-fs.target nss-lookup.target​[Service]Type=simpleExecStart=/usr/local/frp/frps -c /usr/local/frp/frps.iniKillSignal=SIGQUITTimeoutStopSec=5KillMode=processPrivateTmp=trueStandardOutput=syslogStandardError=inherit​[Install]WantedBy=multi-user.target
```

ExecStart的内容请根据自己frp安装目录修改。

## 设置开机启动

```
systemctl daemon-reload
```

```
systemctl enable frp
```

## 启动 frp

```
systemctl start frp
```

## 查看frp是否启动

```
ps aux  grep frps
```

# 六.客户端配置

客户端下载地址：[https://github.com/fatedier/frp/releases/download/v0.35.0/frp\_0.35.0\_windows\_amd64.zip](https://github.com/fatedier/frp/releases/download/v0.35.0/frp_0.35.0_windows_amd64.zip)

解压到自己喜欢的目录，进入该文件夹，可以看到很多文件名中带有"frps"的文件以及文件名中带有"frpc"的文件，分别对应frp的服务器端和客户端，我们正在配置的是客户端，因此文件名中带有"frps"的文件均无需保留，可以删除。

删除后应具有以下文件/文件夹：

![文件夹](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210122003451.png)

用记事本打开frpc.ini（电脑上有Notepad++的话用Notepad++编辑更好，因为这种配置文件会因为编码类型的改变而出现问题，Notepad++更改编码类型会很方便），编辑内容如下：

```
[common]server_addr = x.x.x.x    # 填写自己的云服务器公网IP地址，有域名的读者也可以填写域名server_port = 7000       # 云服务器设置的端口为7000，所以这里填7000# token = 000000         # 与frps.ini设置的token一致，没设置则删去​[test1]                  # []内可以自己起一个拉风的名字^_^type = tcp               # 传输协议，可以是tcp或者udplocal_ip = 127.0.0.1     # 计算机网络中，127.0.0.1代表本地地址local_port = 80          # 需要映射出去的端口号，80为http默认端口号，此端口号必须被本机放行remote_port = 10000      # 映射到云服务器上面的端口号，必须被云服务器的防火墙放行
```

大功告成，可以运行了。在打开CMD或者Windows Terminal用cd命令进入frpc.ini所在目录，输入：

```
frpc.exe -c frpc.ini
```

检查是否有相关进程正在运行。

# 七.配置完成，尽情享用