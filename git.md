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
Git跟踪并管理的是修改，而非文件。
用git diff HEAD -- readme.txt命令可以查看工作区和版本库里面最新版本的区别

## 撤销修改
git checkout -- file用版本库里的版本替换工作区的版本(git restore \<file>)
总之，就是让这个文件回到最近一次git commit或git add时的状态.

git reset HEAD \<file>可以把暂存区的修改撤销掉，重新放回工作区(git restore --staged \<file>)

## 删除文件
在Git中，删除也是一个修改操作
确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit

# 远程仓库
使用 GitHub
由于本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：
1.创建SSH Key
打开Shell（Windows下打开Git Bash），创建SSH Key：
```shell
$ ssh-keygen -t rsa -C "youremail@example.com"
```
一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

2.登陆GitHub，打开“Account settings”，“SSH Keys”页面：
然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容

## 添加远程库
现在的情景是，你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步。

首先登录GitHub创建一个新的仓库。

然后在本地仓库目录运行命令：
```
git remote add origin git@github.com:CoderGzj/Git.git
```
添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的

下一步，就可以把本地库的所有内容推送到远程库上
git push -u origin master
由于远程库是空的，第一次推送master分支时，加上了-u参数

推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样
从现在起，只要本地作了提交，就可以通过命令：
git push origin master

* 删除远程库
使用git remote rm \<name>。
使用前，建议先用git remote -v查看远程库信息，然后，根据名字删除。
此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

## 从远程库克隆
现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

首先，登陆GitHub，创建一个新的仓库。

现在，远程库已经准备好了，下一步是用命令git clone克隆一个本地库：
```
git clone git@github.com:CoderGzj/Git.git
```

# 分支管理
Git的分支是与众不同的，无论创建、切换和删除分支，Git在1秒钟之内就能完成

## 创建于合并分支
在版本回退里已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。
主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

首先，我们创建dev分支，然后切换到dev分支
```shell
$ git checkout -b dev
// git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
$ git branch dev
$ git checkout dev
```

用git branch命令查看当前分支。git branch命令会列出所有分支，当前分支前面会标一个*号。

然后就可以在dev分支上正常提交，dev分支的工作完成就可以切换回master分支。

现在把dev分支的工作成果合并到master分支上：
\$ git merge dev
git merge 命令用于合并指定分支到当前分支。

合并完成后，就可以放心地删除dev分支了：
\$ git branch -d dev

* switch
实际上，切换分支这个动作，用switch更科学。因此，最新版本的Git提供了新的git switch命令来切换分支：
创建并切换到新的dev分支，可以使用：
\$ git switch -c dev
直接切换到已有的master分支，可以使用：
\$ git switch master

```
小结
Git鼓励大量使用分支：
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>或者git switch <name>
创建+切换分支：git checkout -b <name>或者git switch -c <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>
```

## 解决冲突
当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。

## 分支管理策略
通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
--no-ff参数，表示禁用Fast forward
因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。

分支策略
在实际开发中,应该按照几个基本原则进行分支管理：
首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
干活都在dev分支上，也就是说，dev分支是不稳定的，到版本发布时把dev分支合并到master上，在master分支发布版本；
每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

## Bug分支
每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。

Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。git stash
刚才的工作现场存到哪去了？用git stash list命令查看。

Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
1.git stash apply，但是恢复后stash内容并不删除，需要用git stash drop来删除；
2.git stash pop，恢复的同时把stash内容也删了

Git提供了cherry-pick命令，能复制一个特定的提交到当前分支。

小结
```
修复bug通过创建新的bug分支进行修复，然后合并，最后删除；
当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场；
在master分支上修复的bug，想要合并到当前dev分支，可以用git cherry-pick <commit>命令，把bug提交的修改“复制”到当前分支，避免重复劳动。
```

## Feature 分支
开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D \<name>强行删除。

## 多人协作
当从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且远程仓库的默认名称是origin。
要查看远程库的信息，用git remote
用git remote -v显示更详细的信息

**推送分支**
推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：
git push origin master
git push origin dev

但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？
* master分支是主分支，因此要时刻与远程同步；
* dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
* bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
* feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

**抓取分支**
多人协作时，大家都会往master和dev分支上推送各自的修改。
当伙伴从远程库clone时，默认情况下，伙伴只能看到本地的master分支。

伙伴要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是用这个命令创建本地dev分支：
git checkout -b dev origin/dev
现在就可以在dev上继续修改，然后时不时地把dev分支push到远程。

伙伴已经向origin/dev分支推送了他的提交，如果碰巧你也对同样的文件作了修改，并试图推送：推送失败，有冲突。
解决办法：
先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：
git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：
git branch --set-upstream-to=origin/dev dev

因此，多人协作的工作模式通常是这样：
1. 首先，可以试图用git push origin \<branch-name>推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用git push origin \<branch-name>推送就能成功！

如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to \<branch-name> origin/\<branch-name>。

## Rebase
命令git rebase
rebase操作可以把本地未push的分叉提交历史整理成直线；
rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

# 标签管理
发布一个版本时，通常先在版本库中打一个标签（tag），这样就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。

Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针,标签不能移动，所以创建和删除标签都是瞬间完成的。

## 创建标签
首先，切换到需要打标签的分支上

然后，命令git tag \<name>就可以打一个新标签：

用命令git tag查看所有标签

默认标签是打在最新提交的commit上的。如果忘了打标签，方法是找到历史提交的commit id，然后打上就可以了。git tag \<name> commit id

注意，标签不是按时间顺序列出，而是按字母排序的。可以用git show \<tagname>查看标签信息

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字

## 操作标签
命令git push origin \<tagname>可以推送一个本地标签；

命令git push origin --tags可以推送全部未推送过的本地标签；

命令git tag -d \<tagname>可以删除一个本地标签；

命令git push origin :refs/tags/\<tagname>可以删除一个远程标签。

# 使用GitHub
在GitHub上，可以任意Fork开源仓库；
自己拥有Fork后的仓库的读写权限；
可以推送pull request给官方仓库来贡献代码。

# 使用Gitee
因为git本身是分布式版本控制系统，可以同步到另外一个远程库，当然也可以同步到另外两个远程库。

使用多个远程库时，我们要注意，git给远程库起的默认名称是origin，如果有多个远程库，需要用不同的名称来标识不同的远程库。

# 自定义Git
Git还有很多可配置项。
比如，让Git显示颜色，会让命令输出看起来更醒目：
git config --global color.ui true

## 忽略特殊文件
忽略某些文件时，需要编写.gitignore
.gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理

## 配置别名