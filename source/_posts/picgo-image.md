---
title: 利用Picgo和GitHub搭建图床
tags: []
id: '244'
categories:
  - - 服务搭建
date: 2021-07-22 17:47:45
---

# 前言

刚开始写博客时，文章中的图片我总是在博客写好后一张张上传到我的服务器中，后来我觉得这样既麻烦又占用服务器的空间，于是我转向了图床，我选择用另一台服务器搭建图床，将图片上传到图床上，然后通过外链来使用我所要用的图片，但这样过了一段时间后，当我的服务器到期时，如果我不选择续费，那么储存在上面的图片也将消失，如果选择搬迁又要在文章中更改图片的外链，这样一来就十分麻烦。最终我找到了一个自动化程度高、并且不需要担心图片丢失的方法来存储图片——利用Picgo+GitHub搭建一个好用的图床。

以下便是具体的操作步骤。

# GitHub方面

## 新建一个GitHub仓库

打开GitHub，点击New repository。

![image-20210722170922637](https://cdn.jsdelivr.net/gh/ntgoaywh/picgo/img/image-20210722170922637.png)

Repository name任意填，Description写不写都行，选择Public，最后点击Create repository。

![image-20210722171456242](https://cdn.jsdelivr.net/gh/ntgoaywh/picgo/img/image-20210722171456242.png)

## 获取Token

点击个人头像--Settings--Developer settings--Personal access tokens，然后点击Generate new token，Note任意填写，Select scopes只需要勾选第一个repo即可，最后点击Generate token

![image-20210722171848314](https://cdn.jsdelivr.net/gh/ntgoaywh/picgo/img/image-20210722171848314.png)

![image-20210722172016238](https://cdn.jsdelivr.net/gh/ntgoaywh/picgo/img/image-20210722172016238.png)

这时便会生成token，一定要把它复制下来并保存好，因为它只出现一次。

![image-20210722172143874](https://cdn.jsdelivr.net/gh/ntgoaywh/picgo/img/image-20210722172143874.png)

# Picgo方面

## 安装Picgo

Picgo的下载地址为：[https://github.com/Molunerfinn/PicGo/releases](https://github.com/Molunerfinn/PicGo/releases)

Windows下载exe，Mac下载dmg，下载完成后安装即可。

## 配置Picgo

这是Picgo的界面，简介美观。

![image-20210722172551098](https://cdn.jsdelivr.net/gh/ntgoaywh/picgo/img/image-20210722172551098.png)

点击图床设置-- GitHub图床，设定仓库名这一栏：你的GitHub用户名/你的仓库名

设定分支名这一栏：main或者master或其他你自己设定的分支（默认为main）

设定Token这一栏：刚才生成的Token

指定存储路径这一栏：可留空，如果你想放在文件夹中，填写文件夹的名字再加上反斜杠/即可。

设定自定义域名这一栏：可留空，如果你想使用jsdelivr的cdn服务加快图片打开速度，那么你可以填写：[https://cdn.jsdelivr.net/gh/GitHub](https://cdn.jsdelivr.net/gh/GitHub)用户名/仓库名。

总体内容如下图所示，最后点击确定即可。

![image-20210722172652468](https://cdn.jsdelivr.net/gh/ntgoaywh/picgo/img/image-20210722172652468.png)

# 图床使用

一般情况下，当我们想上传图片时，只需将图片拖动到Picgo的界面上传或者直接点击剪贴板图床上传（一般用于截图）。

![image-20210722173508025](https://cdn.jsdelivr.net/gh/ntgoaywh/picgo/img/image-20210722173508025.png)

## 快速上传（基本自动化）

我平时主要使用Typora写作，在Typora的设置中选择图像，在插入图片时这一栏选择上传图片，在上传服务这一栏选择PicGo.app,这样当我们截图并将图片粘贴到Typora中时，图片便会自动上传至GitHub，无需再打开Picgo的界面进行上传，此时Typora文章中的所有图片地址均显示为外链，这个方法在我看来是非常好用的并且强烈推荐的，省去了多余的步骤，实现了基本的自动化。

![image-20210722173718490](https://cdn.jsdelivr.net/gh/ntgoaywh/picgo/img/image-20210722173718490.png)