---
title: It is required that your private key files are NOT accessible by others的解决办法
tags: []
id: '207'
categories:
  - - LInux
date: 2021-04-28 19:53:07
---

今天在Ubuntu上想通过终端ssh直接连接我的服务器，我使用的是密钥登录，然而当我输入

```
ssh -i cali.pem ubuntu@my ip
```

后，出现Are you sure you want to continue connecting (yes/no)? ，我输入了yes后，却无法连接，出现了

```
It is required that your private key files are NOT accessible by others.
```

这里的错误是由于密钥的权限过大所引起的，解决方法为chmod 600。

直接在终端输入

```
chmod 600 cali.pem
```

这里的cali.pem是我的密钥名称。

然后再执行一遍ssh登录命令。

最终便可以远程登录成功。