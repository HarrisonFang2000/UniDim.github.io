# **Git的使用流程的总结**

## **Git是什么:**Git是目前世界上最先进的分布式版本控制系统

**工作区：Workspace**

**暂存区：Index / Stage**

**本地仓库：（仓库区）Repository**

**远程仓库：Remote**

## **一：使用git提交代码到版本库的步骤：**

```md
第一步：使用 git add 文件名（多个文件中间用空格隔开），这个其实是将文件添加到了暂存区。
例如：git add test1.php test2.php （提交多个文件到暂存区）
```

```md
第二步：使用 git commit  -m '备注' ，这个其实是将暂存区的文件提交到当前分支上。
```

```md
第三步：git pull origin 远程分支      【拉去远程的最新代码】
```

```md
第四步：git push origin 远程分支     【提交本地仓库代码到远程仓库】
```

### **接下来进行一个demo操作：**

### 添加 test1.php test2.php 到当前的暂存区里面：

```md
git add 文件一  文件二
```

> 注意：⚠️如果想撤销已经add的文件，操作如下：【 --hard 撤销已经add的文件，直接回退到上一次commit版本】

> `git status` 查看一下提交的状态，其中前面绿色的是已经add过的文件
>
> `git reset --hard HEAD` 是把所有add的文件都撤销
>
> `git reset --hard`  目录/撤销的文件是把某个文件撤销

### **提交暂存区的 test1.php test2.php 文件到本地仓库里面：（-m 后面是提交的备注）**

```sql
git commit -m '提交的备注'
```

#### 修改已经提交的备注，使用 git commit --amend

**注意：⚠️如果想撤销已经commit的文件，操作如下：【 --soft 撤销已经commit的文件，已经add到文件不会撤销】**

**撤回上一次提交的文件：**

`git reset --soft HEAD`

**撤销指定版本的提交：**

`git reset --soft 版本号`     【例如：`git reset --hard  f16fb64d282ce8a38c64d5d4099dcf184499be00 `】

**如果进行了两次提交，都想撤回，可以使用 `HEAD~2`**

#### **查看当前提交的日志：**

```bash
git log
```

```mipsasm
git pull origin 远程分支  【拉去远程仓库最新代码】
```

![image-2960960-20220828182741983-1453346532](https://cdn.jsdelivr.net/gh/HarrisonFang2000/ImgStg/img/202212181625810.png)

```perl
git push origin master  【推送本地仓库代码到远程仓库】
```

## 二：删除远程仓库的文件或者目录：

**1.指定目录下的文件：**

```bash
git  rm  -r  --cached  目录 / 文件  【例如：git rm -r --cached   test / test.txt    （ 删除test目录下的test.txt文件 ）】
```

**2.删除指定目录：**

```bash
git  rm   -r --cached  目录     【例如：git rm -r --cached  test   （删除目录test）】
```

**3.推送本次提交**

```perl
git push 
```

## 一、新建代码库

```shell
# 在当前目录新建一个Git代码库
$ git init
# 新建一个目录，将其初始化为Git代码库
$ git init [project-name]
# 下载一个项目和它的整个代码历史
$ git clone [url]
```

## 二、配置

```ruby

# 显示当前的Git配置
$ git config --list
 
# 编辑Git配置文件
$ git config -e [--global]
 
# 设置提交代码时的用户信息
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```

## 三、增加/删除文件

```shell

# 添加指定文件到暂存区
$ git add [file1] [file2] ...
 
# 添加指定目录到暂存区，包括子目录
$ git add [dir]
 
# 添加当前目录的所有文件到暂存区
$ git add .
 
# 添加每个变化前，都会要求确认
# 对于同一个文件的多处变化，可以实现分次提交
$ git add -p
 
# 删除工作区文件，并且将这次删除放入暂存区
$ git rm [file1] [file2] ...
 
# 停止追踪指定文件，但该文件会保留在工作区
$ git rm --cached [file]
 
# 改名文件，名放入并且将这个改暂存区
$ git mv [file-original] [file-renamed]
```

## 四、代码提交

```ruby

# 提交暂存区到仓库区
$ git commit -m [message]
 
# 提交暂存区的指定文件到仓库区
$ git commit [file1] [file2] ... -m [message]
 
# 提交工作区自上次commit之后的变化，直接到仓库区
$ git commit -a
 
# 提交时显示所有diff信息
$ git commit -v
 
# 使用一次新的commit，替代上一次提交
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message]
 
# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] [file2] ...
```

## 五、分支

```shell

# 列出所有本地分支
$ git branch
# 列出所有远程分支
$ git branch -r
# 列出所有本地分支和远程分支
$ git branch -a
# 新建一个分支，但依然停留在当前分支
$ git branch [branch-name]
# 新建一个分支，并切换到该分支
$ git checkout -b [branch]
# 新建一个分支，指向指定commit
$ git branch [branch] [commit]
# 新建一个分支，与指定的远程分支建立追踪关系
$ git branch --track [branch] [remote-branch]
# 切换到指定分支，并更新工作区
$ git checkout [branch-name]
# 切换到上一个分支
$ git checkout -
# 建立追踪关系，在现有分支与指定的远程分支之间
$ git branch --set-upstream [branch] [remote-branch]
# 合并指定分支到当前分支
$ git merge [branch]
# 选择一个commit，合并进当前分支
$ git cherry-pick [commit]
# 删除分支
$ git branch -d [branch-name]
# 删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
# 把当前master分支改名为main, 其中`-M`的意思是移动或者重命名当前分支
$ git branch -M main
```

## 六、标签

```ruby

# 列出所有tag
$ git tag
 
# 新建一个tag在当前commit
$ git tag [tag]
 
# 新建一个tag在指定commit
$ git tag [tag] [commit]
 
# 删除本地tag
$ git tag -d [tag]
 
# 删除远程tag
$ git push origin :refs/tags/[tagName]
 
# 查看tag信息
$ git show [tag]
 
# 提交指定tag
$ git push [remote] [tag]
 
# 提交所有tag
$ git push [remote] --tags
 
# 新建一个分支，指向某个tag
$ git checkout -b [branch] [tag]
```

## 七、查看信息

```shell

# 显示有变更的文件
$ git status
# 显示当前分支的版本历史
$ git log
# 显示commit历史，以及每次commit发生变更的文件
$ git log --stat
# 搜索提交历史，根据关键词
$ git log -S [keyword]
# 显示某个commit之后的所有变动，每个commit占据一行
$ git log [tag] HEAD --pretty=format:%s
# 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
$ git log [tag] HEAD --grep feature
# 显示某个文件的版本历史，包括文件改名
$ git log --follow [file]
$ git whatchanged [file]
# 显示指定文件相关的每一次diff
$ git log -p [file]
# 显示过去5次提交
$ git log -5 --pretty --oneline
# 显示所有提交过的用户，按提交次数排序
$ git shortlog -sn
# 显示指定文件是什么人在什么时间修改过
$ git blame [file]
# 显示暂存区和工作区的差异
$ git diff
# 显示暂存区和上一个commit的差异
$ git diff --cached [file]
# 显示工作区与当前分支最新commit之间的差异
$ git diff HEAD
# 显示两次提交之间的差异
$ git diff [first-branch]...[second-branch]
# 显示今天你写了多少行代码
$ git diff --shortstat "@{0 day ago}"
# 显示某次提交的元数据和内容变化
$ git show [commit]
# 显示某次提交发生变化的文件
$ git show --name-only [commit]
# 显示某次提交时，某个文件的内容
$ git show [commit]:[filename]
# 显示当前分支的最近几次提交
$ git reflog
```

## 八、远程同步

```ruby

# 下载远程仓库的所有变动
$ git fetch [remote]
 
# 显示所有远程仓库
$ git remote -v
 
# 显示某个远程仓库的信息
$ git remote show [remote]
 
# 增加一个新的远程仓库，并命名
$ git remote add [shortname] [url]
 
# 取回远程仓库的变化，并与本地分支合并
$ git pull [remote] [branch]
 
# 上传本地指定分支到远程仓库
$ git push [remote] [branch]
 
# 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --force
 
# 推送所有分支到远程仓库
$ git push [remote] --all
```

## 九、撤销

```ruby

# 恢复暂存区的指定文件到工作区
$ git checkout [file]
 
# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]
 
# 恢复暂存区的所有文件到工作区
$ git checkout .
 
# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]
 
# 重置暂存区与工作区，与上一次commit保持一致
$ git reset --hard
 
# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]
 
# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]
 
# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]
 
# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
$ git revert [commit]
 
# 暂时将未提交的变化移除，稍后再移入
$ git stash
```

## 回退

```perl
撤销已经push的文件例如：
首先会退版本：git reset --soft xxx(版本号)
然后将修改的保存在暂存区：git stash
提交代码：git push -f 
将代码从暂存区取出：git stash pop
```

## **提交部分代码：**

```lua
git status      //查看仓库状态

git add 需要提交的文件名       //添加需要提交的文件名(加路径 参考git status打印出来的文件路径)

git stash -u -k      //忽略其他文件，把现修改的隐藏起来 这样提交的的时候就不会提交未被add的文件

git commit -m      "哪里做了修改可写入"

git pull      //拉取代码

git push      //推送到远程仓库

git stash pop      //恢复之前忽略的文件(非常重要的一步)
```

原文链接：[https://www.cnblogs.com/carver/articles/16633353.html](https://www.cnblogs.com/carver/articles/16633353.html)

标签: #git
