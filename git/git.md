# 客户端
## git pull
	先从服务器上拉取，防止冲突
	将remote的URL设置为不同的服务器，则可以从不同的服务器上拉取
可以使用
```shell
git pull origin branchname --allow-unrelated-histories
```
## git add
1. git add .

	添加当前目录下所有的文件

2. git add -u

	添加仓库中所有有改动并且以及追踪的文件

3. git add --all

	添加所有文件包含之间未追踪的文件

## git commit
	先提交的本地仓库，其实本地仓库和服务器的仓库是没有什么区别的，只是服务器仓库方便共享
```shell
git commit -m "message"
```
这条命令应该被删除
```shell
git commit --allow-empty #不写注释提交
```

## git push
	将本地的提交推送到服务器上，而所谓的服务器是仓库中的remote指定的
	push的时候要指定push到哪个分支
	所以有如下命令
```shell
git push -u origin master #-u 表示总是push到master
```
# 服务端
## git init
	建立本地仓库，本地仓库的内容放在隐藏目录.git下

## git init --bare
	建立空的服务端仓库,之前的.git内容下的文件直接放在文件夹内

# 拉取版本
	仓库URL表示方法
1. windows如下

	**Url本地 file:///[repositories path]**

2. linux直接写路径即可

	**Url本地 [repositories path]**
	**Url远端 https://[host]/path**
	**UrlSSH git@github.com:/path**

## git clone
	git clone URL
	从服务器，可以是ssh或者http方式。也本地其他人正在工作的git仓库(这样不用密码)
## git pull
	先用git init创建本地仓库
	然后用git remote add 添加一个远端仓库
	最后用git pull origin master
## git fetch
	对本地的仓库的remote的URL修改，然后可以使用git fetch来获取最新的服务器端内容
	git fetch获取的文件在.git文件夹内并未checkout到本地

## git checkout
1. 切换到任意commitid git checkout abcde_hash(提交的hash值前5位就够了)
2. 切换到任意branch git checkout branch_name
3. 恢复被误删的文件git checkout filename
4. 对于单个文件切换到某次提交git checkout commitid filename

# 远端仓库
## git remote
1. 查看远端URL
```shell
git remote -v #获取服务端的url

# 也可以用下面的命令
git config --get remote.origin.url
```

2. 查看远端名字

	git remote show origin

3. 添加和删除代码仓库

```shell
git remote add origin URL
git remote rm origin
```

5. git基于ssh协议的文件传输

	只要有ssh,任意linux都可以作为git服务器
```shell
git clone jumhorn@192.168.10.155:/media/leetcode
```
# 分支
## git branch
1. 查看分支git branch
2. 新建分支git branch branchname
3. 切换分支git checkout branchname

# 标记
## git tag
	To create a tag on your current branch, run this:
```shell
#If you want to include a description with your tag
git tag tagname
# When pushing to your remote repo, tags are NOT included by default. You will need to explicitly say that you want to push your tags to your remote repo:
git push origin --tags
```

1. git切换到tag版本
```shell
git checkout tagname
git checkout v2.9.5
```
# 修改本地提交
## git reset
	Reset current HEAD to the specified state
1. 放弃本地未提交的修改

	--hard \
Resets the index and working tree. Any changes to tracked files in the working tree since \<commit> are discarded.

2. 撤销提交回到之前版本

	完成Commit命令的撤销，但是不对代码修改进行撤销
	不加filename表示整个git目录,加filename表示单个文件
```shell
git reset –hard commitid
git reset commitid [filename]
```
## git revert
	用一次提交将旧的代码覆盖新的版本，起到回滚作用

# 工作区管理
## git rm
```shell
# 删除git add的文件所有文件
git rm -–cached -r .
# 删除git add的指定文件
git restore --staged <file>
```

## git mv
	重命名或者移动到其他位置

## git clean
```shell
# To remove directories
git clean -fd
# To remove ignored files
git clean -fX
# To remove ignored and non-ignored files
git clean -fdx
```

# 忽略文件
## .gitignore
	支持通配符
	如果文件名和文件夹名字一样，无法区分

# 版本合并
## git merge
	git merge branchname
	将branchname合并到当前所在branch分支(开发过程中应该多次将mater合并到branches),按提交时间顺序合并

## git rebase
```shell
# 人为控制按照节点来合并，比如将branch所提交节点的全部放在master所提交节点之后
git rebase branchname
# 删除某次提交
git rebase -i commitid
```
## git diff
	查看文件不同
```shell
git diff commitid filename
# 红色表示删除，绿色表示新增
```
# 日志查看
## git log
1. 查看当前分支的log
```shell
# 查看单个文件历史
git log filename
# 向后查看4次提交
git log -4 filename
```
2. 查看单个文件的日志
```shell
#一行输出
git log –pretty=oneline filename
```
3. 查看更详细的状态
```shell
git log --stat
```
## git reflog
	查看HEAD指针的commitid
	救命的功能
1. 拯救已经提交的文件
```shell
# 不小心使用了git reset commitid --hard退回了之前版本，但是新版本未push到服务器
git reflog #便于查找commitid
git checkout commitid
git branch tmp
git checkout master
git merge tmp
git branch -d tmp
```
2. 拯救未提交已经add的文件(暂不可行)
```shell
# no luck
git fsck --unreachable --no-reflogs --no-cache HEAD
```

# 子模块
## git submodule
1. 创建submodule
```shell
git submodule add repository
```
2. clone带submodule的仓库

	下载这种仓库时，默认submodule下的文件夹为空
```shell
# 应该在clone时指定 –recursive
git clone -recursive
# 将子模块更新到特定版本(当时创建的默认版本)
git submodule init
git submodule update
# 将子模块更新到最新版本
git submodule foreach git pull
```
# 储藏
## git stash
	写了一堆垃圾舍不得删，又必须删的时候，代码放入回收站
## stash 提取及删除
1. git stash list   列出stash
2. git stash pop    选择最新的stash
3. git stash clear  清除stash

# svn到git
1. 对应不是标准的SVN库
```shell
git svn clone repositoriesUrl --no-metadata -authors-file filepath.txt
```
2. 对应标准的SVN库
```shell
git svn clone svn项目地址 --no-metadata --trunk=trunk/ --branches=branches --tags=tags --authors-file=./userinfo.txt -s 文件夹名 \
```
## 常用参数
* -r 可指定开始版本号
* -s指定clone下来的文件夹名
* --trunk表示主开发项目
* --branches表示分支项目
* --ignore-refs表示不包含后面的分支项目
* --tag表示打标签的项目
* --authors-file表示svn用户映射到git的用户文件
* --no-metadata参数可阻止git导出SVN包含的一些无用信息。后面还可以加文件夹名字作为clone后的目录，如果没有默认是当前路径

## authors-file的内容
	JumHorn JumHorn<JumHorn@gmail.com>

# 杂记
## 修改历史提交信息
	修改用户名的例子
1. git rebase -i commitid(5位hash值)

	表示修改从commitid之后的提交
	如果想要修改第一次提交,使用如下命令
```shell
git rebase -i --root
```

2. pick改为edit

将需要修改的提交的pick改为edit后退出，然后逐一修改

3. 修改用户名
```shell
git commit --amend --author "JumHorn \<JumHorn@gmail.com>" --no-edit
```

**没有--no-edit还可以对提交信息进行修改**

4. 继续完成
```shell
git rebase --continue
```

5. 修改服务器数据
```shell
git push --force
```

## Head游离
	Head detached from xxx
	Head和master不同步，head超前，master落后
	回到master会丢失head部分，应该为head新建分支，将分支合并到master
```shell
git branch tmp
git checkout master
git merge tmp
git branch -d tmp # 删除创建的tmp分支
```

## 文件模式
	对于使用不同的换行造成的比较时的影响
	忽略文件模式，在该命令后使用其他原始的命令
```shell
git -c core.fileMode=false diff
git -c core.fileMode=false status
```
## 帮助文档
	git \<command> --help
	在windows下可以直接弹出帮助文档

## 使用http协议每次都要输入密码
```shell
git config --global credential.helper store
```

## git diff不用less用cat
```shell
# 防止linux上没有less
git config --global core.pager cat
```