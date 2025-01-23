---
title: 一键PT脚本安装qBittorrent+Deluge+rTorrent+Transmission
tags:
  - PT
id: '72'
categories:
  - - 服务搭建
date: 2021-01-25 19:21:57
---

# 注意事项

1.  本脚本只支持 x86\_64 (amd64) 架构，其他架构都不支持。ARM 用户建议使用 [QuickBox ARM](https://github.com/amefs/quickbox-arm)
2.  本脚本只在独服和 KVM 虚拟化的 VPS 下测试，OpenVZ、Xen 等其他虚拟化架构仍可以尝试使用，但不保证没问题
3.  本脚本目前支持 Debian 9/10, Ubuntu 16.04/18.04. _推荐使用 Debian 10 或 Ubuntu 18.04_
4.  本文的使用说明中的图片是一两年前的，与当前脚本存在较大出入（但文字内容是及时更新的）
5.  建议重装完系统后使用此脚本，非全新安装的情况下（比如你先跑了个其他盒子脚本再跑这个）不确定因素太多容易翻车
6.  目前没有简单易用的卸载方法。如果你有卸载的需求，使用前请三思

# 项目地址

[https://github.com/Aniverse/inexistence](https://github.com/Aniverse/inexistence)

# 一键脚本

### 如果你是新手，对很多选项不了解，直接用这个（替换下账号密码部分）

```
bash <(wget --no-check-certificate -qO- https://github.com/Aniverse/inexistence/raw/master/inexistence.sh) \
-y --tweaks --bbr --rclone --no-system-upgrade --flexget --tr-deb --filebrowser \
--de 1.3.15 --rt 0.9.8 --qb 4.1.9 -u 这十二个字换成你的用户名 -p 这十个字换成你的密码
```

### 如需自定义

```
bash <(wget --no-check-certificate -qO- https://github.com/Aniverse/inexistence/raw/master/inexistence.sh)
```

### 嫌太长，短命令

```
bash <(wget -qO- https://git.io/abcde)
```

# 安装指导

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119131234.png)基本信息

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119131726.png)

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119131834.png)

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119132018.png)

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119132055.png)

之后耐心等待安装，安装时间视安装软件数量以及系统性能而定，最终会得到各个软件WebUI的访问地址，之后重启系统便可成功安装。

# 管理

需要进行相关操作时，输入

```
mingling
```

即可

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119132736.png)

## 输入1

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119132840.png)

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119132928.png)

## 输入2

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119133018.png)

## 输入7

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119133223.png)

可通过选项02安装魔改bbr，通过选项03配置IPv6

## 输入6

![img](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210119133340.png)

可观察各个软件的运行情况，以及通过相关命令管理。

# 相关问题

1.  **_是否升级系统_** 低于 `Ubuntu 18.04`、`Debian 10` 的 LTS 系统可以选择用脚本升级系统（Ubuntu 20.04 暂不支持） 一般来说整个升级过程应该是无交互的，应该不会碰到什么问你 Yes or No 的问题 升级完后会直接执行重启命令，重启完后你需要再次运行脚本来完成软件的安装
2.  **_账号密码_** **`-u <username> -p <password>`** 你输入的账号密码会被用于各类软件以及 SSH 的登录验证 用户名需要以字母开头，长度 4-16 位；密码需要同时包含字母和数字，长度至少 8 位
3.  **_是否更换软件源_** **目前默认直接换源不再提问，如果不想换源，请在运行脚本的使用 `--no-source-change` 参数** 这个选项决定是否替换 `/etc/apt/sources.list` 文件。 其实大多数情况下无需换源；但某些盒子默认的源可能有点问题，所以我干脆做成默认都换源了
4.  **_线程数量_** **`--mt-single`**、**`--mt-double`**、**`--mt-half`**、**`--mt-max`** **目前默认直接使用全部线程不再提问，如果不想使用全部线程，请在运行脚本的使用以上的参数来指定** 编译时使用几个线程进行编译。一般来说用默认的选项，也就是全部线程都用于编译就行了 某些 VPS 可能限制下线程数量能避免编译过程中因为内存不足翻车
5.  **_安装时是否创建 swap_** **`--swap`**，**`--no-swap`** **目前默认对于内存小于 1926MB 的服务器直接启用 swap 不再询问，如不想使用 swap 请用 `--swap-no` 参数** 一些内存不够大的 VPS 在编译安装时可能物理内存不足，使用 swap 可以解决这个问题 实测 1C1T 1GB 内存 的 Vultr VPS 安装 Flood 不开启 swap 的话会失败，开启就没问题了 目前对于物理内存小于 1926MB 的都默认启用 swap，如果内存大于这个值那么你根本就不会看到这个问题……
6.  **_qBittorrent_** **`--qb 4.2.3 --qb-static`**、**`--qb 3.3.11`**、**`--qb no`** static 指静态编译版本，deb 指使用 efs 菊苣编译好的 deb 包来安装。这两种安装方法的最大特点是安装速度非常快 因为 static 和 deb 安装已经很快了，因此去除了从 repo 或 ppa 安装的选项
7.  **_Deluge_** **`--de 1.3.15_skip_hash_check`**、**`--de 1.3.9`**、**`--de no`** 默认选项为从源码安装 1.3.15 2.0.3 目前运行在 Python 2.7 下，且仍然有一些 PT 站不支持 2.0.3，因此不推荐使用 此外还会安装一些实用的 Deluge 第三方插件：

*   `AutoRemovePlus` 是自动删种插件，支持 WebUI 与 GtkUI
*   `ltconfig` 是一个调整 `libtorrent-rasterbar` 参数的插件，在安装完后就启用了 `High Performance Seed` 模式
*   `Stats`、`TotalTraffic`、`Pieces`、`LabelPlus`、`YaRSS2`、`NoFolder` 都只能在 GUI 下设置，WebUI 下无法显示
*   `Stats` 和 `TotalTraffic`、`Pieces` 分别可以实现速度曲线和流量统计、区块统计
*   `LabelPlus` 是加强版的标签管理，支持自动根据 Tracker 对种子限速，刷 Frds 可用
*   `YaRSS2` 是用于 RSS 的插件 隐藏选项 21，是可以跳过校验、全磁盘预分配的 1.3.15 版本 **使用修改版客户端、跳过校验 存在风险，后果自负**

1.  **_rTorrent_** **`--rt 0.9.8`**、**`--rt 0.9.3 --enable-ipv6`**、**`--rt no`** 这部分是调用我修改的 [rtinst](https://github.com/Aniverse/rtinst) 来安装的 注意，`Ubuntu 18.04` 和 `Debian 9/10` 因为 OpenSSL 的原因，只能使用 0.9.6 及以上的版本，更低版本无法直接安装

*   安装 rTorrent，ruTorrent，nginx，ffmpeg，rar，h5ai 目录列表程序
*   0.9.2-0.9.4 支持 IPv6 用的是打好补丁的版本，属于修改版客户端
*   0.9.6 支持 IPv6 用的是 2018.01.30 的 feature-bind 分支，原生支持 IPv6
*   设置了 Deluge、qBittorrent、Transmission、Flexget WebUI 的反代
*   ruTorrent 版本为来自 master 分支的 3.9 版，此外还安装了如下的第三方插件和主题
*   `club-QuickBox` `MaterialDesign` 第三方主题
*   `AutoDL-Irssi` （原版 rtinst 自带）
*   `Filemanager` 插件可以在 ruTorrent 上管理文件、右键创建压缩包、生成 mediainfo 和截图
*   `ruTorrent Mobile` 插件可以优化 ruTorrent 在手机上的显示效果（不需要的话可以手动禁用此插件）
*   `Fileshare` 插件创建有时限、可自定义密码的文件分享链接
*   `GeoIP2` 插件，代替原先的 GeoIP 插件，精确度更好，支持 IPv6 地址识别

1.  **Flood** **`--flood`** **是否安装的问题已被移除，只能使用命令行参数安装** Flood 是 rTorrent 的另一个 WebUI，界面更为美观，加载速度快，不过功能上不如 ruTorrent 第一次登陆时需要填写信息，端口号是 5000，挂载点是 127.0.0.1
2.  **_Transmission_** **`--tr-deb`**、**`--tr 2.83`**、**`--tr no`** Transmission 默认选择从预先编译好的 deb 安装最新版 2.94（解决了文件打开数问题） 此外还会安装 [加强版的 WebUI](https://github.com/ronggang/transmission-web-control)，更方便易用 **_隐藏和从 repo/ppa 安装的选项均已移除_**
3.  **_FlexGet_** **`--flexget`**、**`--no-flexget`** Flexget 是一个非常强大的自动化工具，功能非常多。大多数国内盒子用户主要用它来 RSS（它能做的事情远不止 RSS） 目前脚本里安装 Flexget 时版本会指定为 3.0.31，同时如果系统自带的 Python3 版本低于 3.6 还会升级 Python3 我启用了 daemon 模式和 WebUI，还预设了一些模板，仅供参考 注意：脚本里没有启用 schedules 或 crontab，需要的话自己设置
4.  **_FileBrowser Enhanced_** **`--filebrowser`**、**`--no-filebrowser`** File Browser 提供了网页文件管理器的功能, 可以用于上传、删除、预览、重命名以及编辑盒子上的文件 脚本安装的是 [荒野无灯的 Docker 版 FileBrowser Enhanced](https://hub.docker.com/r/80x86/filebrowser)，[功能更加强大](https://raw.githubusercontent.com/ttys3/filebrowser-enhanced/master/FBvsFBE.zh.png) 这个增强版还可以在网页上右键获取文件的 mediainfo、制作种子、截图、解压等等，对 PT 来说也非常实用 还有一个在 [http://ip:7576](http://ip:7576/) 网址、使用 root 运行、挂载 / 目录的 filebrowser，需要输入 `systemctl enable filebrowser-root --now` 手动启用
5.  **_系统设置_** **`--tweaks`**、**`--no-tweaks`** 默认启用，具体操作如下：

*   安装 [vnstat](https://github.com/vergoh/vnstat) 2.6 以及 [vnstat dashboard](https://github.com/alexandermarston/vnstat-dashboard/)，可以在网页上查看流量统计
*   （注：vnstat dashboard 使用的前提是用脚本安装了 rTorrent，且在 Debian 8 下不可用）
*   修改时区为 UTC+8
*   语言编码设置为 en.UTF-8
*   设置 `alias` 简化命令（私货夹带）
*   修改 screenrc 设置
*   将最大可用空间的硬盘分区的 Linux 保留空间调整到 1%（原先是 5%）

1.  **_Remote Desktop_** **`--vnc`**、**`--x2go`** **是否安装的问题已被移除，只能使用命令行参数安装** 远程桌面可以完成一些 CLI 下做不了或者 CLI 实现起来很麻烦的操作，比如 BD-Remux，wine uTorrent 推荐使用 noVNC，网页上即可操作
2.  **_wine / mono_** **`--wine`、`--mono`** **是否安装的问题已被移除，只能使用命令行参数安装** `wine` 可以实现在 Linux 上运行 Windows 程序，比如 DVDFab、uTorrent `mono` 是一个跨平台的 .NET 运行环境，BDinfoCLI、Jackett、Sonarr 等软件的运行都需要 mono
3.  **_rclone_** **`--rclone`** **是否安装的问题已被移除，只能使用命令行参数安装** rclone 是一个强大的网盘同步工具。默认不安装。安装好后需要自己输入 rclone config 进行配置 此外这个选项还会安装 [gclone](https://github.com/donwa/gclone)
4.  **_Some additional tools_** **`--tools`** **是否安装的问题已被移除，只能使用命令行参数安装** 安装下列软件：

*   `mediainfo` 用最新版是因为某些站发种填信息时有这方面的要求，比如 HDBits
*   `mkvtoolnix` 主要是用于做 BD-Remux
*   `eac3to` 需要 wine 来运行，做 remux 时用得上
*   `ffmpeg` 对于大多数盒子用户来说主要是拿来做视频截图用，安装的是静态编译版本

1.  **_BBR_** **`--bbr`**、**`--no-bbr`** **是否安装的问题已被移除，只能使用命令行参数安装** （如果你想安装魔改版 BBR 或 锐速，请移步到 [TrCtrlProToc0l](https://github.com/Aniverse/TrCtrlProToc0l) 脚本） 会检测你当前的内核版本，大于 4.9 是默认不安装新内核与 BBR，高于 4.9 是默认直接启用BBR（不安装新内核） 注意：更换内核有风险，可能会导致无法正常启动系统
2.  **_libtorrent-rasterbar_** **`--lt RC_1_1`**、**`--lt RC_1_0`**、**`--lt system`**、**`--lt 1.1.12`** **选择哪个版本的问题已被移除，默认使用 RC\_1\_1，只能使用命令行参数自行指定** libtorrent-rasterbar 是 Deluge 和 qBittorrent 所使用的后端，除非 qBittorrent 使用静态编译版本，不然只要选择安装 Deluge 和 qBittorrent 中的任意一样，libtorrent 都是必装的。鉴于 lt 与 de/qb 兼容的情况比较复杂，现在脚本里直接统一使用 libtorrent RC\_1\_1（版本号 1.1.14）。如果你需要自定义版本号，请使用 `--lt <version>` 参数（自定义版本时，不保证脚本能正常工作）

# 其他

若安装Flexget失败可能是Python版本造成的，使用以下命令升级itertools后再重新安装Flexget即可

```
pip install more-itertools==5.0.0
```

```
pip install sentry
```