---
title: 安装ubuntu和windows双系统出现ACPI error、花屏等问题的解决办法
tags: []
id: '186'
categories:
  - - LInux
date: 2021-04-26 23:54:47
---

今天在给Win10的电脑安装Ubuntu时出现了下图所示的问题，显示ACPI BIOS Error，acpi=off，并且出现了很多乱码，在网上搜索半天后，使用了许多办法，最终找到了正确的解决办法。

![](https://blogjkfff-1302429038.cos.ap-beijing.myqcloud.com/img/error.jpg)

解决方案：

1.  出现ubuntu安装界面时无需选择任何选项，按e进入一个新界面，新的界面会显示如下的内容：

```
setparams  'Ubuntu'

​           

        set gfxpayload=keep

        linux /casper/vmlinuz file=/cdrom/pressed/ubuntu.seed maybe-ubiquity quiet splash ---

​                initrd                   /casper/initrd
```

2\. 将`splash`后的`---`换成`nomodeset`，注意splash与---之间有空格，按F10保存即可。

3\. 后续还要装显卡驱动，博主装的是ubuntu20，自带N卡驱动，所以没有后续了。