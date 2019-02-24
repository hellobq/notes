# git 清单

## 新建代码库

``` bash
# 在当前目录下新建一个代码库
$ git init

# 从远端克隆一份代码库和它的历史记录
$ git clone [url]

# 克隆远端仓库某一个分支  // 和clone后再checkout一样的
$ git clone -b [branch-name] [url]

```

## 基本配置

``` bash
# 设置邮箱、用户名
$ git config --global user.email '[your-email]'
$ git config --global user.name '[your-name]'

# 查看当前仓库的配置
$ git config --local --list

# 查看用户的配置
$ git config --global --list

# 查看git的系统配置
$ git config --system --list

# 查看所有配置（系统 + 用户 + 当前仓库）
$ git config --list

```

## 增加文件、撤销

``` bash
# 撤销文件的更改
$ git checkout -- [file-name] [file-name]

# 撤销目录下更改后的文件
$ git checkout -- [dir]

# 撤销所有更改后的文件
$ git checkout -- .


# 添加文件到缓存区
$ git add [file-name] [file-name]

# 添加目录（包括子目录）到缓存区
$ git add [dir]

# 添加全部文件到缓存区
$ git add .


# 撤销已被add进暂存区的文件
$ git reset HEAD [file-name] [file-name]

# 撤销已被add进暂存区的某个目录下的文件（包括子目录）
$ git reset HEAD [dir]

# 撤销已被add进暂存区的所有文件
$ git reset HEAD .

```

## 提交、撤销

``` bash
# 提交暂存区到本地仓库
$ git commit -m 'commet'

# 更改上次提交的注释
$ git commit --amend -m 'new-comment'

# 撤销提交，让代码为上次版本
$ git reset --hard HEAD^

# 撤销提交到指定版本
$ git reset --hard [hash]

```

## 分支

``` bash
# 查看所有本地分支
$ git branch

# 查看所有远端分支
$ git branch -r

# 查看所有本地和远端分支
$ git branch -a

# 基于当前分支来新建一个分支（但依然停留在当前分支）,新的分支和当前分支的提交日志也是相同的
$ git branch [branch-name]

# 切换到某个分支
$ git checkout [branch-name]

# 新建并切换到一个新的分支
$ git checkout -b [branch-name]

# 合并指定分支到当前分支
$ git merge [branch-name]

# 删除分支
$ git branch -d [branch-name]

# 删除远端某个分支
$ git push origin -d [branch-name]

# 分支重命名
$ git branch -m old-name new-name

```

## 查看信息

``` bash
# 查看本地仓库的状态
$ git status

# 查看本地仓库的提交日志（commit），用来找到“回到过去”的hash
$ git log

# 查看本地仓库的命令日志，用来找到“重返未来”的hash
$ git reflog

# 显示工作区和暂存区的差别
$ git diff

```

## 远程同步

``` bash
# 将远程某一分支最新内容拉到本地，但是本地代码没任何的更新，因为没有merge
$ git fetch [branch-name]

# 将远端同一分支的最新内容拉到本地，同时merge
$ git pull [remote-name] [branch-name]

# 显示远程仓库名
$ git remote

# 显示所有的远程仓库名和用户权限
$ git remote -v

# 显示远程仓库的信息
$ git remote show [remote-name]

# 和远程仓库链接
$ git remote add origin [url]

# 取消与当前远程仓库的链接
$ git remote remove [remote-name]

# 把当前分支推送到远程仓库对应的分支上
$ git push [remote-name] [branch-name]

# 把当前分支推送到远程仓库的其他某个分支上
$ git push [remote-name]:[remote-branch-name] [branch-name]

```

## 暂存

``` bash
### 切换到另外一个分支、却不想把当前分支的内容提交时，可选择将当前分支的内容暂存起来。

# 把当前分支更改了的内容暂存起来
$ git stash

# 查看暂存内容
$ git stash list

# 把暂存的内容弹出来
$ git stash pop

# 清理掉暂存（如果不想要之前分支暂存的东西的话...）
$ git stash clear

```

## git reset 参数解释

- --mixed（默认）：改变了提交日志，但是工作区并未发生改变。
- --soft：经过git reset --mixed commitId后，又做了一次git add .操作。
- --hard：改变了提交日志，并且工作区也发生了改变。当前分支回到了老版本。

## git revert 

撤销某一次的提交。比如一个本地分支test-br，依次增加三个文件，有三个提交历史：

commit1、commit2、commit3。

此时执行git revert [第二次的hash值]。只会撤销第二次的提交，提交历史会增加一个commit记录（revert commit2），工作区发生了改变（去除第二次提交的文件更改）

因此：git revert 和 git reset的最大区别是：前者是撤销了某一次提交，增加一个新的提交日志，是一个新的版本。后者可能会撤销多次提交，可能会删除多个记录，回到老版本了。

git revert 解决本地仓库版本低于远端仓库。假如有一次提交，并且把代码推送到了远端，回头发现代码写的并不好，要重置到上一次的历史版本。如果在本地执行：

``` bash
git reset --hard [上个版本的hash]   
git add . 
git commit -m '...'
git push...

```

发现远端不让你push，它让你先pull一下，但是如果你pull一下的话，你的代码又会被重置到当前版本。这样就造成了死循环。试想如果回到上个版本并且生成新的hash，在推送的话，不就不需要pull了嘛（因为本地版本比远端多个hash，也就比远端版本新）。

## .gitignore 文件匹配

> 所有空行和以#开头的行都被忽略;
> .gitignore 必须和 .git文件位于统一目录，否则不生效;
> 遵循标准的[glob](https://github.com/isaacs/node-glob)匹配规则。

``` bash
# test.js文件
test.js

# 屏蔽当前目录的.log文件
*.log

# 屏蔽当前目录以test开头的所有文件
test.*

# 屏蔽dist目录下的所有文件
dist/

# 屏蔽dist目录下的.js文件（不包括子目录）
dist/*.js

# 屏蔽dist目录下（包括子目录）下的.js文件
dist/**/*.js

# 屏蔽dist目录下（包括子目录）下的.js文件，但是a.js不要屏蔽
dist/**/*.js
!dist/**/a.js

# 屏蔽根目录下所有文件名包含a/b/c字母的.js文件
/[abc]*.js

# 不想屏蔽src这个空文件夹，在src/建立一个.gitkeep空文件即可。

```

## 踩一踩

### git无法pull仓库: refusing to merge unrelated histories

对于已经存在的仓库，里边有个已定的项目。如果某天你不要这个项目，你可以：
- clone下来，删除源仓库代码（或者将源仓库代码移到其他分支上），把新的代码扔到master分支。
- 直接在新的代码目录上创建仓库，准备push。但是git它让你先pull，但是pull时也会出错，因为git有历史版本的记忆，你当前的项目不是原来项目。此时需要手动让git**忘记**原来项目的历史记录:
  ``` bash
  $ git pull origin master --allow-unrelated-histories

  ```
  然后再删除->添加->push

### 未merge的分支不能删除: The branch 'br' is not fully merged.

新建的一个分支，写好代码并且commit（也可能已经把它push到远端了）后，如果没merge它，那么通过git branch -d  [branch-name]是删除不了的，你可以：
- 先merge到其他分支，然后再删除。
- 直接强制删除。git branch -D [branch-name]

### github 上如何团队开发项目
Settings -> Collaborators 添加用户名/邮箱即可。
