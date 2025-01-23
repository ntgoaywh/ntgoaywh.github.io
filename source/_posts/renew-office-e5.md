---
title: 微软开发者E5续期教程
tags: []
id: '120'
categories:
  - - 服务搭建
  - - 资源分享
date: 2021-02-02 22:37:42
---

# 前言

微软开发者计划E5只有三个月的有效期，但是我们可以通过调用API的方式使自己的账号保持活跃，从而成功续期，以下我就来介绍一个Github上的项目AutoApiP。

# 项目地址

[AutoApiP---E5自动续期](https://github.com/ntgoaywh/AutoApiP)

## 说明

*   E5自动续期程序，但是**不保证续期**
*   设置了**周六日(UTC时间)不启动**自动调用，周1-5每6小时自动启动一次 （修改看教程）

## 相关

*   AutoApiP：[https://github.com/wangziyingwen/AutoApiP](https://github.com/wangziyingwen/AutoApiP)
*   AutoApiSecret：[https://github.com/wangziyingwen/AutoApiSecret](https://github.com/wangziyingwen/AutoApiSecret)
*   错误及解决办法/续期相关知识/更新日志：[https://github.com/wangziyingwen/Autoapi-test](https://github.com/wangziyingwen/Autoapi-test)
    *   P版错误说明已更新进程序，详细请运行后看action日志报告

## 步骤

*   准备工具：
    *   E5开发者账号（非个人/私人账号）
        *   管理员号 ———— 必选
        *   子号 ———— 可选 （不清楚微软是否会统计子号的活跃度，想弄可选择性补充运行）
    *   rclone软件，[下载地址 rclone.org](https://downloads.rclone.org/v1.53.3/rclone-v1.53.3-windows-amd64.zip) ，(windows 64）
    *   教程图片看不到请科学上网
*   步骤大纲：
    *   微软方面的准备工作 （获取应用id、密码、密钥）
    *   GIHTHUB方面的准备工作 （获取Github密钥、设置secret）
    *   试运行

#### 微软方面的准备工作

*   **第一步，注册应用，获取应用id、secret**
    
    *   1）点击打开[仪表板](https://aad.portal.azure.com/)，左边点击**所有服务**，找到**应用注册**，点击+**新注册**![1](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210203132004.png)
    
    *   2）填入名字，受支持账户类型前三任选，重定向填入 [http://localhost:53682/](http://localhost:53682/) ，点击**注册**![2](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210203132431.png)
    
    *   3）复制应用程序（客户端）ID到记事本备用(**获得了应用程序ID**！)，点击左边管理的**证书和密码**，点击+**新客户端密码**，点击添加，复制新客户端密码的**值**保存（**获得了应用程序密码**！）![3](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210203133105.png)![4](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210203133207.png)
    
    *   4）点击左边管理的**API权限**，点击+**添加权限**，点击常用Microsoft API里的**Microsoft Graph**(就是那个蓝色水晶)， 点击**委托的权限**，然后在下面的条例选中下列需要的权限，最后点击底部**添加权限赋予api权限的时候，选择以下几个（全选Read也行）**        

```
 Calendars.ReadWrite、Contacts.ReadWrite、Directory.ReadWrite.All、
         
        Files.ReadWrite.All、MailboxSettings.ReadWrite、Mail.ReadWrite、
         
        Notes.ReadWrite.All、People.Read.All、Sites.ReadWrite.All、
         
        Tasks.ReadWrite、User.ReadWrite.All
```

*   ![4](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210203133605.png)![7](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210203134208.png)![8](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210203134309.png)
    *   5）添加完自动跳回到权限首页，点击**代表授予管理员同意**如若是**子号**运行，请用管理员账号登录[仪表板](https://aad.portal.azure.com/)找到**子号注册的应用**，点击“代表管理员授权”。![9](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210203134550.png)
*   **第二步，获取refresh\_token(微软密钥)**
    *   1）进入rclone.exe所在文件夹，shift+右键，在此处打开powershell，输入下面**修改后**的内容，回车后跳出浏览器，登入e5账号，点击接受，回到powershell窗口，看到一串东西。

```
  ./rclone authorize "onedrive" "应用程序(客户端)ID" "应用程序密码"
```

*   2）在那一串东西里找到 "refresh\_token"：" ，从双引号开始选中到 ","expiry":2021 为止（就是refresh\_token后面双引号里那一串，不要双引号），如下图，右键复制保存（**获得了微软密钥**）![10](https://cdn.jsdelivr.net/gh/a08332424/blog/article/20210203135108.png)

* * *

#### GITHUB方面的准备工作

*   **第一步，fork本项目**登陆/新建github账号，回到本项目页面，点击右上角fork本项目的代码到你自己的账号，然后你账号下会出现一个一模一样的项目，接下来的操作均在你的这个项目下进行。![image](https://github.com/wangziyingwen/ImageHosting/raw/master/AutoApi/fork.png)[](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApi/fork.png)
*   **第二步，新建github密钥**
    
    *   1）进入你的个人设置页面 (右上角头像 Settings，不是仓库里的 Settings)，选择 Developer settings -> Personal access tokens -> Generate new token![image](https://github.com/wangziyingwen/ImageHosting/raw/master/AutoApi/Settings.png)[](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApi/Settings.png)![image](https://github.com/wangziyingwen/ImageHosting/raw/master/AutoApi/token.png)[](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApi/token.png)
    
    *   2）设置名字为 **GH\_TOKEN** , 然后勾选repo，点击 Generate token ，最后**复制保存**生成的github密钥（**获得了github密钥**，一旦离开页面下次就看不到了！）![image](https://github.com/wangziyingwen/ImageHosting/raw/master/AutoApiP/repo.png)[](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApiP/repo.png)
*   **第三步，新建secret**
    *   1）依次点击页面上栏右边的 Setting -> 左栏 Secrets -> 右上 New repository secret，新建4个secret： **GH\_TOKEN、MS\_TOKEN、CLIENT\_ID、CLIENT\_SECRET**![image](https://github.com/wangziyingwen/ImageHosting/raw/master/AutoApiP/setting.png)[](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApiP/setting.png)![image](https://github.com/wangziyingwen/ImageHosting/raw/master/AutoApiP/secret2.png)[](https://github.com/wangziyingwen/ImageHosting/blob/master/AutoApiP/secret2.png)**(以下填入内容注意前后不要有空格空行)**

##### GH\_TOKEN

```
github密钥 (第三步获得)，例如获得的密钥是abc...xyz，则在secret页面直接粘贴进去，不用做任何修改，只需保证前后没有空格空行
```

* * *

##### MS\_TOKEN

```
微软密钥（第二步获得的refresh_token）
```

##### CLIENT\_ID

```
应用程序ID (第一步获得)
```

##### CLIENT\_SECRET

```
应用程序密码 (第一步获得)
```

试运行

*   1）点击上栏中间的Action进入运行日志页面，中间应该有个绿色按钮（I understand my workflow...），点击。

自动刷新后，会看到左边有两个流程，一个Auto Api Pro，一个Update Token （这两个流程名字前面应该是有两个黄色感叹号的）。 分别点进去，然后会看到有个黄条（this schedule was disabled......），点击 enable workflow 按钮，**两个流程都要按这个！**

（不确定是否都需要进行这一步，我自己做视频教程的时候发现有的。如果你没有，直接忽略并往下进行，能正常运行就可以了 ）

*   2）点击两次右上角的星星（star，就是fork按钮的隔壁）启动action，再点击上面的Action选择Auto Api Pro流程 -> build -> runapi 就能看到每次的运行日志，看看运行状况

（必需点进去build里面的run api看下，api有没有调用到位，有没有出错。外面的Auto Api打勾只能说明运行是正常的，我们还需要确认api调用成功了，就像图里的一样）

![image](https://github.com/wangziyingwen/ImageHosting/raw/master/AutoApi/%E6%97%A5%E5%BF%97.png)

*   3）再点两次星星，查看是否能再次成功运行然后点击Action里的 update token 流程 -> build -> update token ，日志里显示“微软密钥上传成功”。 同时，依次点击页面上栏右边的 Setting -> 左栏 Secrets（也就是Github方面准备的第三步的secret页面），应该能看到MS\_TOKEN显示刚刚update了（这一步是为了保证重新上传到secret的token是正确的）

#### 教程最后

程序会自行按计划启动，不必操心。

但是github更新了防止薅羊毛的规则，如果仓库60天无任何变动，将会暂停Action，但是会发邮件通知，所以请留意邮箱，收到邮件请上来手动启动一下action。（我还没有收到过此邮件，但是据说邮件里会有启动链接，或者上来按两次星星按钮就行）

**P版（AutoApiP）用户请留意是否会触发此暂停规则，由于P版采取了新方案，是否能跳过github检测活跃呢？如果P版收到暂停邮件，最好在issues的这个帖子[触发暂停统计](https://github.com/wangziyingwen/AutoApiP/issues/7)里留言**

### 教程完