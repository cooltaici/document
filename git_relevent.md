**廖雪峰git教程**：https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000
### 1.0 Git安装
#### 1.1 windows下
&emsp;下载windows下的git安装包https://gitforwindows.org/，按默认安装即可。作者在安装后使用的时候出现:
``` bash
fatal: open /dev/null or dup failed: No such file or directory
```
这种属于文件缺失，C:\Windows\System32\drivers\null.sys，从别的电脑拷过来替代即可。</br>
#### 1.2 linux下
&emsp;如果是debian版本，直接在终端执行：
``` bash
&emsp;
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
将暂存区提交到仓库分支。可以想到的是，commit完之后，执行git status之后工作区就没有要git add/rm的内容了
``` bash
git commit -m "comment summary"
```
#### 3.3 管理修改
### 4.0 分支管理
查看修改 </br>
``` bash
git status
git add/rm fine/folder
```
撤销本地所有修改  </br>
``` bash
git reset HEAD .
```
