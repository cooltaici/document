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
### 3.0 文件管理
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
