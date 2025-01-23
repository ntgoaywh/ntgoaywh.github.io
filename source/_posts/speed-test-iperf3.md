---
title: 测试 VPS 本地连接最大速度 iperf3
tags: []
id: '83'
categories:
  - - 服务搭建
date: 2021-01-25 19:35:41
---

大多 VPS 测速脚本使用 speedtest、fast.com 测速节点，很多时候不能真实反映本地连接速度，最直接方法还是从本地发起测试。有个 iperf3 工具可以从本地测试 VPS 可达的最大带宽速度，支持 TCP /UDP 多线程并发测速。

# 获取安装 iperf3

## Centos

```
    yum -y install iperf3
```

## Ubuntu/Debian

```
apt-get -y install iperf3
```

VPS 和本地都要安装。CentOS 或 Ubuntu 系统可以直接在自带软件源里获得。其它 Linux 发行版、macOS 或 Windows 系统，可以从[这里下载](https://iperf.fr/iperf-download.php)。

Windows 版本下载解压后，不是直接运行 .exe 文件，而是将解压文件（不包括文件夹）放入到 **`系统盘:\Windows\System32`** 文件夹下，之后以管理员身份运行“命令提示符”输入测速命令。

# iperf3 测速用法

先在 VPS 上运行 iperf3 进程。其中 `-s` 参数表示服务器端，`-p` 指定使用端口（默认端口 5201。别忘了[防火墙放行端口](https://www.hostarr.com/firewalld-tutorial/)）。如果需要以守护进程后台运行，追加 `-D` 参数。

```
iperf3 -s -p 5201 
```

然后在本机发起测速。其中 `-c` 参数表示客户端并指定测速服务器地址，`-p` 指定服务器端口，`-t` 指定测试时长（单位秒），`-P` 指定并发连接数（越高越能测试到速度极限），`-R` 表示下载测速（不加参数则测试上传速度）。如果要测试 UDP 连接，追加 `-u` 参数。[点此查看完整参数](http://software.es.net/iperf/invoking.html#iperf3-manual-page)。

```
iperf3 -c x.x.x.x -p 5201 -t 60 -P 10 -R
```

运行结果如下图，\[SUM\] 行就是测试数据（以 receiver 为准），带宽测速平均每秒427Mbits。

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210117183504.png)