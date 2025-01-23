---
title: 给 Windows Terminal配置代理
tags: []
id: '126'
categories:
  - - 服务搭建
date: 2021-02-05 00:13:40
---

#   
前言

今天突然想到Windows Terminal也是可以走代理的，于是在网上查阅了相关资料，在这里分享下我所用的方法。

# 命令

有一个坑是，**cmd**，**Git Bash**，**PowerShell** 设置的方式不同，这里分开来说。

## Cmd

**cmd** 中用 `set http_proxy` 设置

```
set http_proxy=http://127.0.0.1:1080set https_proxy=http://127.0.0.1:1080​set http_proxy_user=userset http_proxy_pass=pass​set https_proxy_user=userset https_proxy_pass=pass​# 恢复set http_proxy=set https_proxy=​# Ubuntu 下命令为 export# export http_proxy=http://127.0.0.1:1080
```

就是**前两条命令**。

## Git Bash

**Git Bash** 中用 `export http_proxy` 设置

```
export https_proxy=http://127.0.0.1:1081export http_proxy=http://127.0.0.1:1081# orexport ALL_PROXY=socks5://127.0.0.1:1080​# 恢复unset https_proxyunset http_proxyunset ALL_PROXY
```

## PowerShell

```
# NOTE: registry keys for IE 8, may vary for other versions$regPath = 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Internet Settings'​function Clear-Proxy{    Set-ItemProperty -Path $regPath -Name ProxyEnable -Value 0    Set-ItemProperty -Path $regPath -Name ProxyServer -Value ''    Set-ItemProperty -Path $regPath -Name ProxyOverride -Value ''​    [Environment]::SetEnvironmentVariable('http_proxy', $null, 'User')    [Environment]::SetEnvironmentVariable('https_proxy', $null, 'User')}​function Set-Proxy{    $proxy = 'http://example.com'​    Set-ItemProperty -Path $regPath -Name ProxyEnable -Value 1    Set-ItemProperty -Path $regPath -Name ProxyServer -Value $proxy    Set-ItemProperty -Path $regPath -Name ProxyOverride -Value '<local>'​    [Environment]::SetEnvironmentVariable('http_proxy', $proxy, 'User')    [Environment]::SetEnvironmentVariable('https_proxy', $proxy, 'User')}
```

**纠结于应该用**`set`**还是 `export` 还有一个判断方法是，敲一下这两个命令，如果返回一个长长的列表，就表示应该用这个命令，反之，如果返回找不到这个命令，就不应该用这个命令。**

## 要点

1.  一定要加 `http://`，直接写域名或者 IP 不行。
2.  **http** 和 **https** 都要设置。

然后如果想验证是否成功配置了代理的话，用 `ping` 命令是不可以的

## 查询代理是否存在

```
envgrep -I proxy
```

# ping 还是不行的原因

ping的协议不是http，也不是https，是ICMP协议。

# 验证方式

```
curl -vv http://www.google.com
```

用这条命令来验证，如果返回如下结果表示代理设置成功。

![](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210205002117.png)