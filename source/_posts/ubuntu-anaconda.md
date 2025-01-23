---
title: Ubuntu安装Anaconda时出现的一些问题
tags: []
id: '198'
categories:
  - - LInux
date: 2021-04-28 17:02:34
---

今天给电脑安装了Ubuntu，在给Ubuntu安装Anaconda后，在终端输入conda可检测Anaconda是否成功安装，若提示没有该命令，那么需要输入source ~/.bashrc 来更新环境变量，如果发现这样还是没用，那么需要添加环境变量，

编辑~/.bashrc文件，在最后面加上

```
export PATH=/home/limttkx/anaconda3/bin:$PATH
```

![](https://blogjkfff-1302429038.cos.ap-beijing.myqcloud.com/img/4281.jpg)

保存退出后，再次输入

```
source ~/.bashrc
```

然后输入 **conda list** 测试是否成功，到这为止算是没有问题。

安装了Anaconda后，终端的界面会有一些改变，在用户名前会多出（base），这时因为Anaconda自动加入了命令到 ~/.bashrc中， 在我们打开终端的时候自动 执行了 **conda activate base** 命令。

![2](https://blogjkfff-1302429038.cos.ap-beijing.myqcloud.com/img/4282.png)

一个命令又可以回去：

```
conda deactivate
```

但是如果使用了上述命令，在终端输入Python进入命令行后，之前安装的Anaconda就无法起到作用了。

进入Python后也有了一点小改变，会出现Anaconda,Inc的字样。

![](https://blogjkfff-1302429038.cos.ap-beijing.myqcloud.com/img/4283.png)

如果安装Anaconda是在非root环境下进行的，当我们使用sudo -i进入root用户后，输入conda会提示没有该命令，这时只需同样编辑~/.bashrc文件，在末尾加上**export PATH=/home/limttkx/anaconda3/bin:$PATH**，便可成功使用Anaconda了。

最后要注意一点，export PATH=/home/limttkx/anaconda3/bin:$PATH中的limttkx是我的Ubuntu系统的用户名，这里要根据自己设置的用户名来进行更改。