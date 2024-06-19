

## Basic

这节笔记没用

- why vcs
  - track history、work together
- types
  - centralized (subversion, team foundation server )
  - distributed (git, mercurial)
- why git
  - free、open source、super fast、scalable、cheap branching and merging

### settings

- levers
  - system
  - <u>**global我只用这个**</u>
  - local
##### basic settings

```bash
git config --global user.name "ljt"
git config --global user.email "2073887899@qq.com"
git config --global core.editor ”code --wait“ #code --w 是windows下如果wait选项没有用的话，试试这个-w选项 #code is vscode
git config --global -e # open global settings
git config --global core.autocrlf "" #自动换行要不要加\r windows肯定是要的所以要用windows - true, mac - input
```

##### help messages

```bash
git config --help # details
git config -h # brief
```
### 总结一下
这一节主要要学会git的安装，

重点是全局配置git，

对应配置模块config，尤其是[basic settings](#####basic settings)

## creating snapshots

- staging area(last snapshot version)

once first commit be created staging area exists.

```bash
git add file1 # add file1 to staging area
```

```bash
git commit -m 'first commit' # every commit git store fill content not diff
```

- add and commit to staging at same time

```bash
git commit -ma 'Refactor code.'
```

- **你可以看到git现在里面有什么东西**

```shell
git ls-files
```

- remove from staging area

```bash
git rm --cached -r bin/
```

- **移动git里面的文件**

```shell
git mv file1.txt file1.js
```

- **忽略某些文件**

```shell
echo logs/ > .gitignore
```

github上有写好的，可以照抄[github.com/github/gitignore](github.com/github/gitignore)，你可以直接搜索java

### status

```bash
git status -sb
# -s short，长话短说
```

### diff, difftool

```bash
git diff # the diff of working directory and staging area
git diff --stages   # the diff of staging area and last commit
```

- 也要试试用vscode来进行可视化合并代码，首先要配置一下

```bash
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
git config --global -e #检查一下$LOCAL %REMOTE有没有在全局设置里面，有的时候执行上面一句会失效
```

- 开始使用vscode来对比两个版本

```bash
git difftool
git difftool --staged
```

### show, ls-tree, restore, clean

- `show` will show git objects
  - commits
  - blobs(files)
  - trees(directories)
  - tags

```bash
git show HEAD # HEAD is last commit
git show HEAD~1 # HEAD~n is nth commit before last commit
git show HEAD~1:.gitignore # show the whole file
```

```bash
git ls-tree HEAD~1 # show all
```

- replace `reset` with `restore`
- `restore` move the version to the last version

```bash
git restore --staged file2.js
```

```bash
git clean -fd # remove un-tracking files in working directory
```

## Browsing history

### `--state`, `--patch`

```bash
git log --oneline --stat # the diff line numbers
git log --oneline --patch # the diff detail
```

### filter commits

```bash
git log --oneline -3 # last 3 commits
git log --oneline --author="XING YAHAO"
git log --oneline --after="2020-08-17"
git log --oneline --after="yesterday"
git log --oneline --after="one week ago"
git log --oneline --grep="commit   lomessage term"
git log --oneline -S "git" # search all commit include the search contents and show commit
git log --oneline -S "git" --patch # show the diff it self
git log --oneline fb0d..dad47 # show between range of two commits
git log --oneline netlify.toml # all the commits that modified specific file
git log --oneline -- netlify.toml # file name is ambiguous
git log --oneline --patch -- netlify.toml # show commit content
```

### format git log

```bash
git log --pretty=format:"%an committed %h on %cd" # %an -> author name, %h -> hash value, %cd -> committed date
git log --pretty=format:"%Cgreen%an%Creset committed %h on %cd" # %Cgreen %Creset  change color
```

### viewing a commit

```bash
git show HEAD~2
git show HEAD~2:packages/react-reconciler/src/ReactFiberCommitWork.new.js # see the final version of the commit
git show HEAD~2 --name-only
git show HEAD~2 --name-status
```

### viewing the changes between commits

```bash
git diff HEAD~2 HEAD # find the all differences between two commits
git diff HEAD~2 HEAD fixtures/concurrent/time-slicing/src/index.js # find the differences in specific file
git diff HEAD~2 HEAD --name-only
git diff HEAD~2 HEAD --name-status
```
### checking out a commit

```bash
git checkout c0a77029c # You are in 'detached HEAD' state
git log --oneline -all
git checkout master
```

### finding bugs using bisect

开始找bug，`git bisect start`

一直二分的查找错误，最后再`git bisect reset`

```bash
git bisect start #开始找bug
git bisect bad
git bisect good c0a77029c #这里就是最尾端的git提交
git bisect good
git bisect bad
git bisect reset
```

### finding contributors using shortlog

简单的看所有的贡献者

```bash
git shortlog -n -s -e  #numbered #surpress #email
git shortlog -nse --after="" --before=""
```
### viewing history of a file

```bash
git log toc.txt
git log --oneline toc.txt
git log --oneline --stat --patch .gitignore
```

### restoring a deleting file

删除多了文件

```bash
git rm toc.txt
git commit -m "Removed toc.txt"
git log --oneline -- toc.txt
git checkout a642e12 toc.txt
git commit -m "Restored toc.txt"
```

### git blame and finding the author line by line

```bash
git blame .gitignore
git blame -e .gitignore
git blame -e -L 1,3 .gitignore
```
### tagging

```bash
git tag v1.0 {hash} // lightweight tag
git checkout v1.0
git tag -a v1.1 -m "My version 1.1"  // annotate tag
git tag -n # show tag message
git show v1.1
git tag -d v1.1
```

### 使用其他GUI界面来查看提交历史

Vs来查看提交的历史（GitLens插件）、使用GitKraken

## Branching

### working with branches

```bash
git switch bugfix
git switch -C bugfix/login-form # switch and create new branch
git branch -m bugfix bugfix/signup-form # rename {oldname} {newname}
git branch -d fix/signup-form
git branch -D 
```
### comparing branches

```bash
git log master..fix/signup-form [--oneline]
git log master..fix/signup-form --patch
git diff master..fix/signup-form
git diff --name-only fix/signup-form #不要给我展示细节，文件名字就可以了
git diff --name-status fix/signup-form #或者说我名字和状态都给我显示也可以
```
### stashing

```bash
#当又要切换别的地方了，我手上的工作还没有做完，可以暂存一下。
git stash push -m "New tax rules"
git stash push -am "New stash one" # new file stash
git stash list
git stash show stash@{1}
git stash show 1 #上一句的简化
git stash apply 0
git stash drop 0
git stash clear
```
### merging

这里必须要结合例子，要不然很容易混乱，并不是理解不了，但是是容易混乱的一个点。

#### fast-forward merges(if branches have not diverged)

```bash
git merge [-ff] bugfix/login-form #使用标识会更好一点，默认有ffmerge就用这个
```

#### three-way merges(if branches have diverged)

```bash
git merge -no-ff bugfix/password-form
git config --global merge.ff false #禁用fast-forward merge
git config --global pull.ff only
[merge]
    ff = false
[pull]
    ff = only
#可以不用上面的配置了
git config --global ff no
```
### viewing merged and unmerged branches

```bash
git branch --merged
git branch -d bugfix/signup-form
git branch --no-merged
```

### merge conflicts

graphical merge tools and difftool to vscode

```bash
git config --global merge.tool vscode
git config --global mergetool.vscode.cmd 'code --wait $MERGED'
git config --global mergetool.keepBackup false

git config --global diff.tool vscode
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'
```

```
[merge]
        tool = vscode
[mergetool "vscode"]
        cmd = code -n --wait $MERGED
[diff]
        tool = vscode
[difftool "vscode"]
        cmd = code -n --wait --diff $LOCAL $REMOTE
```

### visual merge tool可视化来合并冲突

- Kdiff
- P4Merge
- Winmerge（Windows Only）

**<u>如果有JetBrain家系列产品的话，没必要额外安装</u>**，像idea对git的可视化合并冲突功能就已经很强大了。

### aborting a merge

```bash
git merge --abort
```

### undoing a faulty merge撤回错误的合并

#### `reset`，认为这个提交是垃圾要丢掉所以我要回退版本

```bash
git reset --hard HEAD~1 # move git pointer to one commit before, apply snapshot to staged area and working directory
git reset --mixed HEAD~1 # default,move git pointer to one commit before, apply snapshot to staged area and working directory
git reset HEAD~1
git reset --soft HEAD~1 # default, move git pointer to one commit before

git reset --hard 882b232 # move pointer to any commit even not show in log history
```

#### `revert`，就算是错误也要保留，只不过重新再来一次

```bash
git revert -m 1 HEAD
#这里的HEAD在master分支上，
#所以他找master分支的之前一个版本，
#在这个合并提交上，
#进行revert翻转回master的一个分支。
```

### squash merging防止污染历史提交记录

很适合那种<u>**短命**</u>（一两天的，几个小时）分支，本来只是来修复一些小小bug，但是却给日志留下了差不多的记录。这时候用这个squash

这个**<u>commit不是merged commit</u>**应该是normal commit

```bash
git merge --squash bugfix/photo_upload #别掉以轻心，他并没有生成一个提交commit
# ff changes to staged area
# Updating f10f470..0d9b74a
# Fast-forward
# Squash commit -- not updating HEAD
# LICENSE   | 1 +
# README.md | 1 +
git commit -m "fixed: in photo upload"

# this branch won't show in
git branch --merge # squash merged branch won't show
git branch --unmerged # will show
git branch -D fix/photo_upload # force delete only，用D是因为git不认为它被合并了，这也是为什么不是merged commit的原因了
```
### rebase改变分支的命根子

本地使用没问题，要是多人协作，肯定会一团糟。

很容易在多人协作中出现毁灭性操作。

**<u>慎重慎重再慎重。</u>**

- no merge conflict（很少出现。。。）

```bash
git switch -C 'feature/shopping-cart'
git commit
git switch master
git commit
git switch feature/shopping-cart
git rebase master
git switch master
git merge --ff feature/shopping-cart
```

- merge conflict

```bash
git rebase master
# Auto-merging toc.txt
# CONFLICT (content): Merge conflict in toc.txt
# error: could not apply 97e93a6... Update toc.txt 1
# Resolve all conflicts manually, mark them as resolved with
# "git add/rm <conflicted_files>", then run "git rebase --continue".
# You can instead skip this commit: run "git rebase --skip".
# To abort and get back to the state before "git rebase", run "git rebase --abort".
# Could not apply 97e93a6... Update toc.txt 1
git mergetool
git rebase --continue #所以merge也应该用continue
git rebase --skip #跳过也行
git rebase --abort
#有的时候你abort放弃rebase了，但是发现文件目录竟然多了XXX.txt.orgin文件，
#这个是合并分支工具自动生成的备份文件，如果不想要的话可以
git config --global mergetool.keepBackup false
```

### cherry picking，每个commit就像一个樱桃水果，任意的挑水果吧
```bash
git cherry-pick a1f63e6
# Auto-merging toc.txt
# CONFLICT (content): Merge conflict in toc.txt
# error: could not apply a1f63e6... Update toc.txt 1
# hint: after resolving the conflicts, mark the corrected paths
# hint: with 'git add <paths>' or 'git rm <paths>'
# hint: and commit the result with 'git commit'
git add .
git commit
```
### picking a file from another branch
```bash
git switch -C feature/send-mail
git add .
git commit
git switch master
git restore --source=feature/send-mail -- mail.txt
```

### Working with Branches in VSCode，试试看吧我觉得一般

<u>**还是要用GitLens这个插件**</u>

<u>**可视化分支要用GitGraph插件**</u>

## Collaborating

### remote tacking branch

```bash
git remote
git remote -v
```
### fetching

```bash
git fetch origin # download all commit
git branch -vv
git merge origin/master
```

### pulling(fetch + merge)，这个pull也是不简单

```bash
git pull # if branch diverse three way merge
git pull --rebase # avoid three way merge --rebase
#往往我们用rebase选项，因为我们不想真的要合并吧
#要么合并，要么pull的时候rebase，这个没有对错，看个人喜好，论坛都吵了很久了。
```

### pushing

```bash
git push origin master # default will be git push
#1.其实默认remote就只有一个orgin。
#2.我现在是觉得就是应该不允许使用 --force 或者说-f选项，强制push，
#要不然把别人的贡献覆盖掉了，凌驾于别人之上就很无语。
#除非除非你搞糟了整个history。
#3.为什么会被rejected，是因为就是别人在这一个分支做出贡献了，
#你们两个的提交记录都不一样，不允许push
```

### Storing Credentials保存凭据

```bash
#简单的解决办法是，用缓存时间。
#我输了一遍密码，让他在默认15分钟内之后再也不用输入密码。
#这个缓存时间自己定。
git config --global credential.helper cache
#或者使用ssh-keygen来配置一个电脑凭据。这个我会。
```

### sharing tags

```bash
git tag v1.0
git push origin v1.0
git push origin --delete v1.0
git tag -d v1.0
```

### releases发布版本，这个是github的功能不是git的

<u>**这个很适合项目发布个版本，记得编译一下。**</u>

### sharing branches

```bash
git branch -vv
git branch -r #remote branch related to what branch
git push -u origin feature/change-password #-u是缩写，--setupstream
git push -d origin feature/change-password
git branch -r
```

### collaboration workflow真实的Git合作场景

看视频，这里不好说

```bash
git switch -C feature/change-password origin/feature/change-password
git remote prune origin #同步github上的远程端
```

### Github Pull Requests

看视频，基本实在github网页上运行

### GitHub issues也就是assignment的别名

### GIthub Labels

### Github Milestones不就是DDL的另一种说法，和issue的联动

### keeping a forked repository up to date

```bash
git remote
git remote -v
git remote add upstream {BASE_URL} #{BASE_URL}要被被fork的链接代替，就是原本的仓库的git地址
git remote
git remote -v
git remote rename upstream base #也可以换个名字
git remote rm base
git fetch upstream #这里肯定不是origin这个仓库了，所以不能缩写git fetch
git switch master
git merge base/master
```

## rewriting history学完上面所有后，你会遇到这些问题

<u>**不要重写PUBLIC HISTORY**</u>

这个视频的例子包括了很多小问题

- 打错字了
- 换了图表的颜色
- 加了一个jar包
- 一个commit做了两件主要的事情
- 一个一点描述都没有的commit

复习一下reset、revert

**实际修改一个commit就是创建了一个新的commit**，可以联想一下java的String对象

### undoing commits

```bash
git reset --hard HEAD~1
git diff --cached
```

### reverting commits翻转的方式撤销自己的提交

```bash
git revert HEAD~2
git revert HEAD~3..HEAD # revert (3, 0] commit
git revert --no-commit HEAD~3..HEAD #后面的那个HEAD可以省略，
#这样就可以把三个commit用一个commit的方式进行revert好
git revert --continue
```

### recovering lost commits恢复丢失的提交

```bash
git reflog
git reset --hard HEAD@{1}
```

### amending the last commits修改这个commit

```bash
git add .
git commit --amend #这里可以后面再加上 “”，里面写新的commit message

#万一提交包括的多的东西怎么办
git reset --mixed HEAD~1
git clean -fd #去除untracked file
```

### amending an earlier commit修改更早更早的commit

恐怖的rebase，简直了毁灭性。因为创建一堆一摸一样的commit

```bash
git rebase -i {HASH} #交互的rebase
# do your change such as
git commit --amend
# do your change end
git rebase --abort #发现搞砸了，赶紧丢掉
git rebase --continue
```

### dropping commits删除一堆commits

```bash
git rebase -i 6cbd931^ # ^ means parent
# drop commit
```

### rewording commit messages重命名你的commit

```bash
git rebase -i f283d7524^
# reword
#把pick选择用reword这个选项替代
```

### reordering commits给你的commit排序

```bash
git rebase -i f283d7524^
# move commit order
#就是排序就好
```

### squashing commits压缩你的commit

```bash
git rebase -i f283d7524
#在交互界面把pick改成squash。
#git就会把你的commit归到上面，上面的commit，方向是↑。
# squash

#这里回到原来的状态，演示一下和squash差不多的选项，fixup选项
git reflog
git reset --hard HEAD@{9}

git rebase -i f283d7524
# fixup选项和sqush没有什么区别，就差一个重命名commit的过程
```

### splitting a commit分割commit，一个commit里面有两个功能但是这两个功能没有关系

```bash
git rebase -i f283d7524
# 使用edit 命令
git reset --mixed HEAD^ # HEAD^ == HEAD~1
# to change and commit it 1比如git add package.txt; git commit -m "Update Google Map SDK version 1.0 -> 2.0"
# to change and commit it 2然后git add . ; git commit -m "Add term of service"
git rebase --continue
```

## extra tips


### Push commit to different remote branch

```bash
git push origin local-name:remote-name
```

### Dry run push

```sh
git push -nu origin xxx
# -n --dry-run
# -u --set-upstream
```

#### Update forked repository to original repository latest

```bash
git remote add upstream https://github.com/original/repository.git

git fetch upstream

git rebase upstream/master

git push origin master --force
```

## 目录

[TOC]






- [Basic](#basic)
  - [settings](#settings)
      - [basic settings](#basic-settings)
      - [help messages](#help-messages)
- [creating snapshots](#creating-snapshots)
  - [status](#status)
  - [diff, difftool](#diff-difftool)
  - [show, ls-tree, restore, clean](#show-ls-tree-restore-clean)
- [Browsing history](#browsing-history)
  - [`--state`, `--patch`](#--state---patch)
  - [filter commits](#filter-commits)
  - [format git log](#format-git-log)
  - [viewing a commit](#viewing-a-commit)
  - [viewing the changes between commits](#viewing-the-changes-between-commits)
  - [checking out a commit](#checking-out-a-commit)
  - [finding bugs using bisect](#finding-bugs-using-bisect)
  - [finding contributors using shortlog](#finding-contributors-using-shortlog)
  - [viewing history of a file](#viewing-history-of-a-file)
  - [restoring a deleting file](#restoring-a-deleting-file)
  - [git blame and finding the author line by line](#git-blame-and-finding-the-author-line-by-line)
  - [tagging](#tagging)
- [Branching](#branching)
  - [working with branches](#working-with-branches)
  - [comparing branches](#comparing-branches)
  - [stashing](#stashing)
  - [merging](#merging)
    - [fast-forward merges(if branches have not diverged)](#fast-forward-mergesif-branches-have-not-diverged)
    - [three-way merges(if branches have diverged)](#three-way-mergesif-branches-have-diverged)
  - [viewing merged and unmerged branches](#viewing-merged-and-unmerged-branches)
  - [merge conflicts](#merge-conflicts)
  - [aborting a merge](#aborting-a-merge)
  - [undoing a faulty merge](#undoing-a-faulty-merge)
    - [`reset`](#reset)
    - [`revert`](#revert)
  - [squash merging](#squash-merging)
  - [rebasing](#rebasing)
  - [cherry picking](#cherry-picking)
  - [picking a file from another branch](#picking-a-file-from-another-branch)
- [Collaborating](#collaborating)
  - [remote tacking branch](#remote-tacking-branch)
  - [fetching](#fetching)
  - [pulling(fetch + merge)](#pullingfetch--merge)
  - [pushing](#pushing)
  - [sharing tags](#sharing-tags)
  - [sharing branches](#sharing-branches)
  - [collaboration workflow](#collaboration-workflow)
  - [keeping a forked repository up to date](#keeping-a-forked-repository-up-to-date)
- [rewriting history](#rewriting-history)
  - [undoing commits](#undoing-commits)
  - [reverting commits](#reverting-commits)
  - [recovering lost commits](#recovering-lost-commits)
  - [amending the last commits](#amending-the-last-commits)
  - [amending an earlier commit](#amending-an-earlier-commit)
  - [dropping commits](#dropping-commits)
  - [rewording commit messages](#rewording-commit-messages)
  - [reordering commits](#reordering-commits)
  - [squashing commits](#squashing-commits)
  - [splitting a commit](#splitting-a-commit)
- [extra tips](#extra-tips)
  - [Push commit to different remote branch](#push-commit-to-different-remote-branch)
  - [Dry run push](#dry-run-push)
    - [Update forked repository to original repository latest](#update-forked-repository-to-original-repository-latest)