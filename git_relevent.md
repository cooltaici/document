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
### 4.0 分支管理
#### 4.1 创建和合并分支

