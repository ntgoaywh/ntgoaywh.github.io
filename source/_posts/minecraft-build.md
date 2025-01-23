---
title: 用腾讯轻量搭建带WEB控制台的MC服务器
tags: []
id: '102'
categories:
  - - 服务搭建
date: 2021-01-27 23:55:07
---

众所周知mc多好玩，大家都喜爱，可是守护进程有点麻烦，screen经常会有些问题，所以不如搞个面板，顺便也解决守护进程问题 （能不用手就不用手），腾讯轻量大家应该都有，直接开始。

# 一.安装宝塔

选择好相应的系统后，用对应的脚本安装宝塔面板。

## Centos安装命令

```
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
```

## 试验性Centos/Ubuntu/Debian安装命令独立运行环境（py3.7） 可能存在少量兼容性问题 不断优化中

```
curl -sSO http://download.bt.cn/install/install_panel.sh && bash install_panel.sh
```

## Ubuntu/Deepin安装命令

```
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && sudo bash install.sh
```

## Debian安装命令

```
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && bash install.sh
```

## Fedora安装命令

```
wget -O install.sh http://download.bt.cn/install/install_6.0.sh && bash install.sh
```

## Linux面板7.5.1升级命令

```
curl http://download.bt.cn/install/update6.shbash
```

## 图简便

直接选用应用镜像

![宝塔](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210126221312.png)

# 二.BDS

bds是mc官方搞的一个基岩版服务端，可以直接运行，分有win/linux

链接 [https://www.minecraft.net/en-us/download/server/bedrock](https://www.minecraft.net/en-us/download/server/bedrock)

![2](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210126221829.png)

# 三.面板

选择GitHub上一位大佬的面板，使用的是nodejs

## 项目地址

[https://github.com/LomotHo/bedrock-console](https://github.com/LomotHo/bedrock-console)

# 四.部署服务

连接服务器，然后依次进行以下步骤

### 创建文件夹

```
mkdir mc
```

### 进入文件夹

```
cd mc
```

### 下载面板

```
git clone https://github.com/LomotHo/bedrock-console.git &&cd bedrock-console
```

### 新建文件夹并进入文件夹

```
mkdir bedrock &&cd bedrock
```

### 下载MC服务端

```
wget https://minecraft.azureedge.net/bin-linux/bedrock-server-1.16.201.02.zip
```

### 解压文件

```
unzip bedrock-server-1.16.201.02.zip
```

### 切换到上级目录

```
cd ..
```

### 安装nodejs

#### Centos

```
yum install nodejs -y
```

#### Ubuntu/Debian

```
apt-get install nodejs -y
```

### 运行nodejs

```
cd vue
```

```
npm i
```

```
npm run build
```

```
cd ..
```

```
npm i
```

```
node app.js
```

### 防火墙

![firewall](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210127234428.png)

打开图上所示的端口

# 五.访问

在浏览器中输入 ip:3000 就能控制了

打开宝塔-软件商店-安装Supervisor管理器

![supervisor](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210127234649.png)

就可以自由玩了

# 六.Docker方式部署(懒人必备)

## 项目地址

[https://github.com/LomotHo/bedrock-console](https://github.com/LomotHo/bedrock-console)

其中有docker版本，完成后既能有守护进程，也有面板。

# 七.其他

腾讯的docker加速器 [https://mirror.ccs.tencentyun.com](https://mirror.ccs.tencentyun.com)，配置在腾讯的服务器，内网速度很快。