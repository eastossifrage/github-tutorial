<!--
author: 东方鹗
date: 2016-06-03
title: 第二章 使用 GitHub 的前期准备
tags: git, github, 你应该会玩github
category: git
status: publish
summary: 在使用 GitHub 建立仓库之前，我们需要做一些前期的准备，建立 GitHub 账户并进行初始化设置等工作。请认真准备，不要因为前期的重视，后面留有遗憾。
-->

> 在使用 GitHub 建立仓库之前，我们需要做一些前期的准备，建立 GitHub 账户并进行初始化设置等工作。请认真准备，不要因为前期的重视，后面留有遗憾。

## 使用前的准备

### 创建账户

首先让我们来创建 GitHub 账户。请打开创建账户的页面。[https://github.com/join?source=header-home](https://github.com/join?source=header-home)

如下图所示。你需要进行用户注册。
![01.png-82.5kB][1]
填写完所有信息后，点击 Create an account，就能完成账户的创建。庄户创建完成后会直接进入登录状态，用户可以立即开始使用 GitHub。如果你向分享你的内容，直接分享链接 https://github.com/{username} 即可，比如作者本人的GitHub账户就是 [https://github.com/eastossifrage](https://github.com/eastossifrage)，欢迎fork me。

### 设置头像

头像是通过 Gravatra 服务显示的。可以通过[http://cn.gravatar.com](http://cn.gravatar.com)进行邮箱和头像绑定。使用过 WordPress 的读者可能对它有所了解。

此处，我们需要再次吐槽一番，在天朝@#￥@#￥@#￥@#￥@#%@#￥%@#￥。建议大家还是用翻墙工具来设置头像。

### 设置 SSH Key

GitHub 上链接已有仓库时的认证，是通过使用 SSH 的公开密钥认证方式进行的。现在让我们来创建公开密钥认证所需的 SSH Key，并将其添加至 GitHub。已经创建过的读者，请用现有密钥进行设置。

运行下面的命令创建 SSH Key。

```bash
$ ssh-keygen -t rsa -C "ossifrage@gmail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ossifrage/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/ossifrage/.ssh/id_rsa.
Your public key has been saved in /home/ossifrage/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:VorXqrLpi05WOFs7rbiDZ0jR7jIWvgo+Asi7DZtY 
ossifrage@gmail.com
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|                 |
|       .  .      |
|   .  +..+       |
|  o o+.DC .      |
|. o=oo=o+.       |
|=o=+o..o.        |
|=X=Eo+..         |
|B**=B=.          |
+----[SHA256]-----+

```

"ossifrage@gmail.com"是在创建账户时用的邮箱地址。密码需要在认证时输入。id_rsa文件是私有密钥，id_rsa.pub文件是公有密钥。

### 添加公开密钥

在 GitHub 中添加公开密钥，今后就可以用私有密钥进行认证了。

点击右上角账户的设定按钮（ Settings ），选择 SSH and GPG Keys菜单后，就会出现下图界面:
![02.png-46kB][2]
点击 New SSH key，会出现 Title 和 Key两个输入框。在 Title 中输入适当的密钥名称。Key 部分请粘贴 id_rsa.pub 文件里的内容。 id_rsa.pub 文件里的内容可以用如下方法查看。

```bash
$  cat ~/.ssh/id_rsa.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCRTPSgOY3ABxOOARDcXmob4yoayh3G0KLITlp9nFVf89hNT9jc0BI3OP2IZv/yz8MdLG2gtQsUtkKKhC2eaG23btPqI2rCcpKk4nA2T8jeXw4PRFXIDeoBfNa/jdQdfNw3qMfD...........N76vCsi2NGYxvhf4lrjZROm+XL/cux5DTBWdBGkzpuzaB8...........UVnyWYataTKBrO4BF2U5gGBPRHe3l9Qf5uIcirUhsT9lX3TIX8ZmY79+WuPorJWv6UL3DJXu8Ygbwlt/fgvy5XKk9cUQM5RdYKI82DZHRiq1G9bp4zAlaDXlSn73iSTx1or4F849b ossifrage@gmail.com
```

添加成功之后，创建账户时所用的邮箱会接到一封提示“公共密钥添加完成”的邮件。

完成以上设置后，就可以用手中的私人密钥与 GitHub 进行认证和通信了。

```bash
 ssh -T git@github.com
The authenticity of host 'github.com (192.30.252.122)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? 输入yes
Warning: Permanently added 'github.com,192.30.252.122' (RSA) to the list of known hosts.
Hi eastossifrage! You've successfully authenticated, but GitHub does not provide shell access. 显示链接成功。

```
在输入yes之后会弹出一个对话框，如下图：![03.png-32.5kB][3]
输入认证的密码即可。

### 使用社区功能

既然说 GitHub 能够以人为焦点，那么在创建账户之后，不妨试试 Follow （关注）别人。在别人的用户信息页面的右上角点击绿色的 Follow 按钮即可。

这样一来，你所 Follow 的用户的活动就会显示在你的控制面板页面中了。你可以知道你所关注的人在 GitHub 上都做了什么。

对于仓库，也可以使用 Watch 功能获取最新的开发信息。如果你经常使用的某个软件正在 GitHub 上进行开发，不妨去 Watch 一下。

## 实际动手使用

### 创建仓库

点击右上角工具栏里的 New repository （也就是右上角你的头像左侧的 + ），创建新的仓库，页面显示如下：
![04.png-52.9kB][4]

 - Repository name

在 Repository name 栏中输入仓库的名称。这里我们输入 ousikongjiantest。

- Description

Description 栏中可以设置仓库的说明。这一栏不是必须项，可以留空。

- Public 、Private

可以选择 Public 或者 Private 。这里我们选择 Public ，创建公开的仓库，所有内容都被公开。
选择 Private 可以创建私有仓库，用户可以设置访问权限，但是这项服务是收费的。

- Initialize this repository with a README

在 Initialize this repository with a README 选项上打上钩，随后 GitHub 会自动初始化仓库并设置 README 文件，让用户可以立刻 clone 这个仓库。如果想向 GitHub 添加手中已有的 Git 仓库，建议不要勾选，直接手动 push。

- Add .gitignore

下方左侧的下拉菜单非常方便，通过它可以在初始化时自动生成 .gitignore 文件。这个设定会帮我们把不需要在 Git 仓库中进行版本管理的文件记录在 .gitignore 文件中，省去了每次根据框架进行设置的麻烦。下拉菜单中包含了主要的语言及框架，选择今后将要使用的即可。

- Add a license

右侧的下拉菜单可以选择要添加的许可协议文件。如果这个仓库中包含的代码已经确定了许可协议，那么请在这里进行选择。随后将自动生成包含许可协议内容的 LICENSE 文件，用来表明该仓库的许可协议。
输入选择完成后，点击 Create repository 按钮，完成仓库的创建。页面显示如下：
![05.png-81kB][5]

### 连接仓库

下面这个 URL 便是刚刚建立的仓库的页面。
https://github.com/eastossifrage/ousikongjiantest

- README.md

README.md在初始化时已经生成好了。README.md文件的内容会自动显示在仓库的首页当中。因此人们一般会在这个文件中标明本仓库所包含的软件的概要、使用流程、许可协议等信息。如果使用 Markdown 语法进行描述，还可以添加标记，提高可读性。

- GitHub Flavored Markdown

在 GitHub 上进行交流时用的 Issue、评论、Wiki，都可以用 Markdown 语法表述，从而进行标记。准确地说应该是GitHub Flavored Markdown（ GFM ）语法。该语法是 GitHub 在 Markdown 语法的基础上扩充而来的，说白了时一种方言，但是一般情况下只要按照原本的 Markdown 语法进行描述就可以。
关于 Markdown 语法的解说，网上有很多相关资料，可以自行查阅。
使用 GitHub 后，很多文档都需要用 Markdown 语法来书写。因此需要务必学会该语法。

### 公开代码

- clone已有仓库

clone已有仓库到自己的开发环境中。参照 GitHub 页面提供的路径：
![06.png-18.5kB][6]
注意：请记住点击 SSH 按钮。

然后在自己的开发环境中进行如下操作：

```bash
git clone git@github.com:eastossifrage/ousikongjiantest.git
正克隆到 'ousikongjiantest'...
warning: 您似乎克隆了一个空仓库。
检查连接... 完成。
```

这里会要求输入 GitHub 上设置的公开密钥的密码。认证成功后，仓库便会被 clone到仓库名后的目录中。将想要公开的代码提交至这个仓库再 push 到 GitHub 的仓库中，代码便会被公开。

- 编写代码

进入开发环境的仓库,
```bash
$ cd ousikongjiantest
```

这里我们编写一个 hello_ousikongjian.py 文件，用来输出“ Hello ousikongjian!”。

```python
#! /usr/bin/env python
# -*- coding:utf8 -*-

print u'Hello ousikongjian!'

```
由于 hello_ousikongjian.py还没有添加至 Git 仓库，所以显示为 Untarcked files。

```bash
$ git status
位于分支 master

初始提交

未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）

	hello_ousikongjian.py

提交为空，但是存在尚未跟踪的文件（使用 "git add" 建立跟踪）
```

- 提交

将 hello_ousikongjian.py提交至仓库。这样以来，这个文件就进入了版本管理系统的管理之下。今后的更改管理都交由 Git 进行。

```bash
$ git add hello_ousikongjian.py
$ git commit -m "Add hello ousikong script by python"
[master （根提交） 01a256b] Add hello ousikong script by python
 1 file changed, 4 insertions(+)
 create mode 100644 hello_ousikongjian.py
```
通过 git add 命令将文件加入 *暂存区*，再通过 git commit 命令提交。
添加成功后，可以通过 git log 命令查看提交日志。

```bash
$ git log
commit 01a256be62e16688ec75a06bfe7703dab80cf5c6
Author: eastossifrage <eastossifrage@gmail.com>
Date:   Fri Jun 3 16:01:40 2016 +0800

    Add hello ousikong script by python
```

- 进行 push

之后只要执行 push，GitHub 上的仓库就会被更性。

```bash
$ git push
warning: push.default 尚未设置，它的默认值在 Git 2.0 已从 'matching'
变更为 'simple'。若要不再显示本信息并保持传统习惯，进行如下设置：

  git config --global push.default matching

若要不再显示本信息并从现在开始采用新的使用习惯，设置：

  git config --global push.default simple

当 push.default 设置为 'matching' 后，git 将推送和远程同名的所有
本地分支。

从 Git 2.0 开始，Git 默认采用更为保守的 'simple' 模式，只推送当前
分支到远程关联的同名分支，即 'git push' 推送当前分支。

参见 'git help config' 并查找 'push.default' 以获取更多信息。
（'simple' 模式由 Git 1.7.11 版本引入。如果您有时要使用老版本的 Git，
为保持兼容，请用 'current' 代替 'simple'）

对象计数中: 3, 完成.
Delta compression using up to 4 threads.
压缩对象中: 100% (2/2), 完成.
写入对象中: 100% (3/3), 313 bytes | 0 bytes/s, 完成.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:eastossifrage/ousikongjiantest.git
 * [new branch]      master -> master

```
根据提示，建议将  'push.default' 设置为 simple 模式。
这样一来，代码就在 GitHub 上公开了。不妨可以查看一下相关仓库页面。

## 小结

本文简单讲解了在 GitHub 上建立仓库并公开代码的流程。掌握这些，你就算踏入 GitHub 的世界拉。

  [1]: http://www.os373.cn/blog/img/GitHub_/01.png
  [2]: http://www.os373.cn/blog/img/GitHub_/02.png
  [3]: http://www.os373.cn/blog/img/GitHub_/03.png
  [4]: http://www.os373.cn/blog/img/GitHub_/04.png
  [5]: http://www.os373.cn/blog/img/GitHub_/05.png
  [6]: http://www.os373.cn/blog/img/GitHub_/06.png
