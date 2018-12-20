**廖雪峰git教程**：<https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000>

### 1.0 Git安装
#### 1.1 windows下
&emsp;下载windows下的git安装包<https://gitforwindows.org/>，按默认安装即可。作者在安装后使用的时候出现:
``` bash
fatal: open /dev/null or dup failed: No such file or directory
```
这种属于文件缺失，C:\Windows\System32\drivers\null.sys，从别的电脑拷过来替代即可。</br>
#### 1.2 linux下
&emsp;如果是debian版本，直接在终端执行：
``` bash
sudo apt-get install git
```
#### 1.3 git配置
windows下：
``` bash
git config --global user.name "cooltaichi"
git config --global user.email "tc080618@sina.cn"
```
### 2.0 远程管理
#### 2.1 将远程仓库（比如github）克隆到本地
执行：
``` bash
git clone url
```
#### 2.2 将本地仓库推送到远程
执行：
``` bash
git push url
```
### 3. 文件管理
git管理的是修改，这是git为什么比其它版本控制系统设计得更好的原因。使用git diff可以查看工作区和最新版本控制的差异。
``` bash
git diff HEAD -- filename
```
#### 3.1 版本回退
git log命令显示从最近到最远的提交日志,--pretty=oneline是单行显示，这个命令会显示每次commit的ID号（版本号）
``` bash
git log
git log --pretty=oneline
```
回退到上一个版本。HEAD其实就是版本指针。注：Git的版本回退非常快，因为它只要移动HEAD指针就可以了。
``` bash
git reset --hard HEAD^
```
根据commit_id回退到任意版本。
``` bash
git reset --hard commit_id
```
查询命令历史，以便获得commit_id。比如我们在回退到比较靠前的版本，又想重新回到最新版本，使用git log已经看不到了，这时候可以用git relog
``` bash
git reflog
```
#### 3.2 工作区和暂存区
见：https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013745374151782eb658c5a5ca454eaa451661275886c6000 </br>
查看工作区状态
``` bash
git status
```
将工作区的修改提交到暂存区
``` bash
git add
git rm
```

#### 3.3 管理修改
将暂存区提交到仓库分支。可以想到的是，commit完之后，执行git status之后工作区就没有要git add/rm的内容了
``` bash
git commit -m "comment summary"
```
通过下面的命令，查看各个区的版本差异：
-----------------------版本库--------------------------------------------
                                         |                           |
                                 git diff --cached                   |
                                         |                           |
-------------暂存区----------------------                        git diff HEAD
                        |                                            |
                     git diff                                        |
                        |                                            |
-----工作区--------------------------------------------------------------
#### 3.4 撤销修改
&emsp;怎样撤销工作区的修改，使用git checkout可以回到最近一次git add或git commit之前的状态。这里有两种情况：</br>
- 文件修改后还没有被放到暂存区，撤销修改就回到和版本库一模一样的状态
- 文件修改后添加到暂存区，又作了修改，那么撤销修改就是回到暂存区的状态
``` bash
git cheakout -- filename
```
注：-- 这个很重要，如果没有就变成切换到分支的命令
&emsp;上面是对工作区的撤销处理，那么如何对已经存放到暂存区的修改做撤销呢？我们可以使用git status查看暂存区的状态，然后使用git reset命令进行暂存区撤销命令：
``` bash
git reset HEAD filename
git reset HEAD .  #所有文件
```
#### 3.5 文件删除
当在工作区删除掉文件之后，使用git rm可以将删除步骤提交到暂存区，然后就可以使用git commit提交版本库了。
``` bash
git rm filename
```
### 4. 分支管理
#### 4.1 创建和合并分支
git中，使用git branch创建分支，使用git checkout切换
``` bash
git branch dev
git checkout dev
```
也可以使用一步命令直接完成创建分支到切换的目的。-b这个参数表示切换的意思
``` bash
git checkout -b dev
```
使用git branch可以列出所有分支，并且标出当前分支。
``` bash
git branch
```
分支合并，使用git merge可以将当前版本和指定版本合并。如果要合并的分支的关系是前后关系，那么合并的模式是Fast-forward模式，这种模式只是指针的指向的改变。
``` bash
git merge dev
```
放弃合并。
``` bash
git merge --abort
``
删除分支。使用git branch -d 可以删除指定分支。一般来说，在分支上完成某个任务后，先合并到master，然后再删除掉branch分支。
``` bash
git branch -d dev
```
#### 4.2 解决冲突
当两个分支都做了修改的时候，就不能使用快速合并了，这个时候要合并的话，可能会出现冲突。这个时候我们需要手动解决冲突。Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容。</br>
使用git log --graph可以查看分支合并的图。
``` bash
git log --graph --pretty=oneline --abbrev-commit
```
#### 4.3 分支管理策略
通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。其中--no-ff是禁用Fast forward模式，-m是commit参数。
``` bash
git merge --no-ff -m "merge with no-ff" dev
```
#### 4.4 Bug分支
&emsp;如果有一个编号为110的BUG需要尽快修复，需要放下手中的工作。并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？幸好，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。</br>
将当前工作区存储起来
``` bash
git stash
```
查看存储的工作区现场列表。
``` bash
git stash list
```
恢复现场，但是不删除
``` bash
git stash apply
git stash apply stash@{0}
```
恢复工作区现场，并删除
``` bash
git stash pop
```
#### 4.5 Feature分支
如果因某些原因，导致新branch分支任务取消，需要彻底删除这个分支。使用:
``` bash
git branch -D dev
```
注：使用git branch -d dev是不行的，没有合并的分支无法删除
#### 4.6 多人协作
使用git remote查看远程库的信息
```bash
git remote
git remote -v
```
使用git push推送分支
``` bash
git push origin master
git push origin dev
```
一般开发过程中有哪些分支呢？
- master。这个分支是主干分支，一般只用来推送版本，不作开发。需要时刻保持与本地同步。
- dev。开发分支，团队所有成员都要在这个上面工作
使用git clone从远程库上clone后，使用git branch只能看到master分支。创建远程的dev分支使用：
``` bash
git checkout -b dev origin/dev
```
如果有别的人，在你提交之前，对dev版本作了修改并且已经提交完毕，这时候推送的话，就会有冲突，这时候需要先git pull从origin/edv抓取下来，然后本地合并，解决冲突再进行推送。</br>
先指定本地dev分支和远程分支的链接：
``` bash
git branch --set-upstream-to=origin/dev dev
git pull 
```
#### 4.7 Rebase
### 5. 标签管理
### 6. 自定义git
