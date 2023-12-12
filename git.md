Git教程
# Git简介
Git是目前世界上最先进的分布式版本控制系统
## Git的诞生
Linus在1991年创建了开源的Linux。在2002年以前世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码。
Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git

## 集中式vs分布式
集中式版本控制系统，版本库是集中存放在中央服务器的。集中式版本控制系统最大的毛病就是必须联网才能工作。
分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库。
和集中式版本控制系统相比，分布式版本控制系统的安全性要高很多

# 安装Git
* 在Linux上安装Git
首先，你可以试着输入git，看看系统有没有安装Git
如果用Debian或Ubuntu Linux，通过sudo apt-get install git就可以直接完成Git的安装，非常简单。
如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入：./config，make，sudo make install这几个命令安装就好了。
* 在Windows上安装Git
在Windows上使用Git，可以从Git官网直接下载安装程序，然后按默认选项安装即可。
安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功
* 安装完成后，还需要最后一步设置，在命令行输入：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。
注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

# 创建版本库
版本库又名仓库，英文名repository，可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。

* git init 把目录变成Git可以管理的仓库。目录会多一个隐藏目录.git，管理版本库。
* 把文件添加到版本库
所有的版本控制系统，只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等

把一个文件放到Git仓库只需要两步。
1. 用命令git add告诉Git，把文件添加到仓库：
\$ git add readme.txt
2. 用命令git commit告诉Git，把文件提交到仓库：
\$ git commit -m "wrote a readme file"
-m后面输入的是本次提交的说明，可以输入任意内容，最好是有意义的
* 为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件
```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

# 时光机穿梭
git status命令可以让我们时刻掌握仓库当前的状态
git diff命令能看具体修改了什么内容

## 版本回退
* git log 命令显示从最近到最远的提交日志.
如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数：

* 在Git中，HEAD表示当前版本,上一个版本就是HEAD\^,上上一个版本就是HEAD\^^。

* 使用git reset --hard commit_id 在版本的历史之间穿梭

* Git在内部有个指向当前版本的HEAD指针。所以HEAD指向哪个版本号，就把当前版本定位在哪。

* git reflog 命令用来记录每一次命令

## 工作区和暂存区
工作区（Working Directory）
就是在电脑里能看到的目录

版本库（Repository）
工作区有一个隐藏目录.git,是Git的版本库。
Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

git add 实际是把文件修改添加到暂存区
git commit 实际上是把暂存区的所有内容提交到当前分支
创建Git版本库时，Git自动为我们创建了唯一一个master分支

## 管理修改

## 撤销修改

## 删除文件

# 远程仓库

# 分支管理

# 标签管理