---
title: Git安装和简单使用
date: 2018-11-25 15:22:18
tags: [Git] 
categories: "Git"
---

#### 在Windows上安装Git   
在Windows上使用Git，可以从[Git官网](https://git-scm.com/downloads)直接下载安装程序，然后按默认选项安装即可。   
安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

安装完成后，还需要最后一步设置，在命令行输入：
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
<!-- more -->
基本操作步骤
```
git init
git clone https://xxxxxxxxx.git

git pull 远程库名 master
git add -A   #表示把项目里面全部文件添加进列表 
git commit -m "Hello world"
git push -u 远程库名 master   #第一次使用push的时候加上-u,以后可不加
```

##### 使用步骤   
###### 1.初始化 

```
mkdir gitTest
cd gitTest
git init
```
成功提示  Initialized empty Git repository in XXX.git/

###### 2.把文件添加到仓库,用命令git add告诉Git

```
$ git add readme.txt
```
###### 3.把文件提交到仓库,用命令git commit告诉Git

```
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```
简单解释一下git commit命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的   

---
> 初始化一个Git仓库，使用git init命令。   
> 添加文件到Git仓库，分两步：   
> 1.使用命令git add <file>，注意，可反复多次使用，添加多个文件；   
> 2.使用命令git commit -m <message>，完成。   

###### 4.运行git status命令看看结果

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
git status命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，readme.txt被修改过了，但还没有准备提交的修改。
###### 5.用 git diff 查看修改内容，顾名思义就是查看difference。

知道修改哪些内容后可以
1. git add
2.git commit
3.再运行git status看看当前仓库的状态.

> 要随时掌握工作区的状态，使用git status命令。   
> 如果git status告诉你有文件被修改过，用git diff可以查看修改内容

###### 6.用git log命令查看从最近到最远的提交日志
看到的一大串类似1094adb...的是commit id（版本号）
###### 7.时光穿梭机，回退到上一个版本。   
Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100 。
回退到上一个版本。

```
$ git reset --hard HEAD^
HEAD is now at e475afc add distributed
```
> HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令
```
git reset --hard commit_id
```
> 穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。

###### git log 退出 英文状态下按 Q
--- 
### git放弃修改
本地修改了一堆文件(并没有使用git add到暂存区)，想放弃修改
单个文件/文件夹：

```
$ git checkout -- filename
```

所有文件/文件夹：

```
$ git checkout .
```

本地新增了一堆文件(并没有git add到暂存区)，想放弃修改。 
单个文件/文件夹：

```
$ rm filename / rm dir -rf
```

所有文件/文件夹：

```
$ git clean -xdf
```

// 删除新增的文件，如果文件已经已经git add到暂存区，并不会删除！
本地修改/新增了一堆文件，已经git add到暂存区，想放弃修改。 
单个文件/文件夹：

```
$ git reset HEAD filename
```

所有文件/文件夹：

```
$ git reset HEAD .
```



###### GIT 单个文件修改比较

```
1. git log 文件名           （查看提交的ID）
2. git diff commitid:文件名 commitid:文件名
```


git log -p 文件名 可以看到具体文件修改记录

