---
title: 《Git-Pro》Git初识
comments: true
date: 2016-09-25 20:11:53
tags: Git
categories:
- 技术
---

**获取Git仓库**

有两种取得Git 项目仓库的方法。1.在现有的项目或者目录下导入所有的文件到Git中 2.从一个服务器克隆一个现有的Git仓库。

**1.在现有目录中初始化仓库**

```c
git init
```

该命令创建了.git子目录，它紧紧包含初始化Git仓库中所有的必须文件，这些文件是Git仓库的骨干。如果你是在已经存在文件的文件夹中初始化Git仓库，我们应该开始跟踪这些文件并且提交。git add 命令来指定对文件的跟踪，让后git commit提交。

```c
git add test.c
git add README.md
git commit -m "初始化项目版本"
```

这样test.c和README.md已经处于版本控制之下。

**2.克隆现有的仓库**

使用git clone命令，git clone的是该Git仓库服务器上的几乎所有数据，而不是复制完成你的工作所需要的文件。当你执行clone命令的时候，默认配置下远程Git仓库中的每一个文件的每一个版本都将被拉取下来。使用命令`git clone [url]`。比如要从github或者gitlab上克隆某个项目：

```c
git clone https://github.com/AgentEric/xxxx/oooo
```

这个命令会在当前目录下创建一个名字为"oooo"的目录，并且在这个目录下初始化一个.git文件夹，从远程仓库拉取所有的数据放入.git文件计划i啊，然后从中读取最新版本的文件的拷贝。进入"oooo"文件夹，所有的项目文件已经在里面了，准本就绪并且等待我们的开发和使用。另外：如果我们想在克隆远程仓库的时候自定义本地仓库的名字：

```c
git clone https://github.com/AgentEric/xxxx/oooo myName
```

这样除了执行与上一个命令同样的操作外，本地创建的仓库名字变为 myName。

**检查当前文件状态**

`git status`

**跟踪新文件**

`git add README.md`

`git add`命令使用文件或者目录的路径作为参数，如果参数是目录的路径，该命令将递归地跟踪目录下的所有文件。

**暂存已修改的文件**

`git add`命令是多功能命令：*她可以用来开始跟踪新文件，或者把已经跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已经解决状态等。*所以，对她的理解最正确的是：**添加内容到下一次提交中。**

注意：同一个文件可能会出现在暂存区和非暂存区。git 暂存了每一次运行`git add`命令时的版本，而不是在运行`git commit`命令时候的当前目录下的版本。所以运行了`git add`之后如果又作了修改，需要重新运行`git add`把最新的版本重暂存起来。

基本的Git工作流程如下：

1. 在工作目录中修改文件
2. 暂存文件，将文件的快放入暂存区域
3. 提交更新，找到暂存区域的文件，将快照永久性存储到Git仓库目录。

如果Git目录中保存着特定版本文件，则属于**已提交committed**状态。如果作了修改并已放入暂存区，就属于**已暂存staged**状态。如果上次取出后，作了修改但还没有放到暂存区域，则是**已修改modified**状态。

- committed：已提交表示数据已经安全地保存在本地数据库 中。
- modified: 已修改表示修改了文件，但是还没有保存到数据库中。
- staged: 已暂存表示对一个已经修改文件的当前版本作了标记，使之包含在下次提交的快照中。

命令行
只有在命令行模式，才能执行Git的所有命令，而大多数的GUI软件只实现了Git所有命令或者功能的子集，并且提供图形界面来降低难度。

Git保证完整性

Git中所有数据在存储前都会计算校验和，然后以校验和引用。用以计算校验和的机制叫SHA-1散列（hash,哈希），它由40个十六进制的字符串（0-9 a-f）组成的字符串，基于Git中文件的内容和目录结构计算出来的。<u>注意</u>：[谷歌攻破SHA-1算法](http://tech.sina.com.cn/it/2017-02-24/doc-ifyavwcv8684013.shtml)，本来哈希碰撞本来是不应该发生的但是当哈希算法存在漏洞时，攻击者可以制造出碰撞，用来攻击那些依靠哈希值来校验文件的系统，植入恶意文档造成恶果。Chrome、Firefox以及Edge已经公开宣布弃用SHA-1。关于为什么Google着急弃用SHA-1，请看这篇[文章](http://daily.zhihu.com/story/4195991)。

初次运行Git前的配置

Git自带一个git config的工具来帮助设置控制Git外观和行为的配置变量。

- /etc/gitconfig 文件：包含系统上每一个用户以及她们仓库的通用配置。如果带有 - -sytem选项的git config，它会从此文件读写配置变量。
- ~/.gitconfig或~/.config/git/config文件：只针对当前用户。可以传递 - -global选项让Git读写此文件。
- 当前使用仓库的Git目录中的config文件（.git/gitconfig）:只针对该仓库

`git config`命令有三层作用域分别是 `--system --global--local`，越往后优先级越高，local配置会覆盖所有的，如果local空则读取global，如果global空则读取system。每一个级别覆盖上一个级别的配置，所以.git/config的配置会覆盖/etc/gitconfig中的配置变量。

查看配置项

`git config --list`查看特定的配置项`git config user.name`

获取帮助：`git help config`

设置默认文本编辑器（我习惯vim）

`git config --global core.editor vim`

（未完待续……）