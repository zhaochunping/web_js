# git的相关操作

[TOC]

## 1、gitbask

- cd /d/gitsample/    (跟踪目录)

- git init

- 查看本地添加了哪些远程分支地址 git remote（具体查看：git remote -v）

- git remote rm origin (先删除远程仓库以防其他的远程链接占用)

- git remote add origin https://username:password@github.com/username/nihao.git   （可用）
  (将本地仓库关联到远程仓库，执行完后没有输出，说明就成功了)

  git remote add origin git@github.com:zhaochunping/web_js.git

- fetch将远程主机的最新内容拉到本地，不进行合并：git fetch origin master

- pull 则是将远程主机的master分支最新内容拉下来后与当前本地分支直接合并 fetch+merge：git pull origin master

- 下载项目： git pull git@github.com:zhaochunping/web_js.git

  **git pull** 命令用于从远程获取代码并合并本地的版本。

  **git pull** 其实就是 **git fetch** 和 **git merge FETCH_HEAD** 的简写。 

- 删除缓存区所有命令 ： git rm -r --cached .

- 上传文件：git add push.txt（或者git add --all）

- 查看状态，绿色表示添加成功：git status

- 把add的文件commit到仓库：git commit -m "push.txt"

- （git pull --rebase origin master）

- git push -u origin master

- 创建分支：git branch branchname

- 切换分支：git checkout branchname

- 合并分支：git merge branchname

- git help pull

```
//常见命令
git push origin master //把本地源码库push到Github上
git pull origin master //从Github上pull到本地源码库
git config --list //查看配置信息
git status //查看项目状态信息
git branch //查看项目分支
git checkout -b host//添加一个名为host的分支
git checkout master //切换到主干
git merge host //合并分支host到主干
git branch -d host //删除分支host
```

成功的上传步骤：

- cd /d/gitsample/text/（本地仓库路径）
- git init（生成.git文件夹）
- git add .（所有或者git add push.txt）
-  git commit -m "my commit"
-  git remote rm origin（待用）
- git remote add origin https://github.com/username/repositoryname.git （仓库地址）
- $ git push -u origin master（输入github密码，成功上传）

更新步骤：

- git add .
- git commit -m "update test"
- git push -u origin master //提交修改到项目主线

下载文件步骤：

- git remote add origin https://github.com/username/repositoryname.git
- git pull origin master

## 2、常见问题

### 2.1git init运行后无.git文件

是因为文件管理默认隐藏了.git文件夹；

### 2.2 .git文件加内容

***hooks***（钩）**：存放一些**shell**脚本

***Info****：**exclude**：存放仓库的一些信息*

***logs****：保存所有更新的引用记录*

***objects****：存放所有的**git**对象*

***refs：***

***COMMIT_EDITMSG***：*最新提交的一次Commit Message，git系统不会用到，给用户一个参考*

***config：****git仓库的配置文件*

***description：****仓库的描述信息，主要给gitweb等git托管系统使用*

***heads：****保存当前最新的一次提交的哈希值*

***index****：暂存区（**stage**），一个二进制文件*

***FETCH_HEAD****： 是一个版本链接，指向着目前已经从远程仓库取下来的分支的末端版本*

***HEAD****：映射到**ref**引用，能够找到下一次**commit**的前一次哈希值（看上面**logs**的图）*

***ORIG_HEAD***:*HEAD指针的前一个状态*

### 2.3  git 只 pull 某一个文件/夹

```js
 $ git config core.sparsecheckout true
//core.sparsecheckout用于控制是否允许设置pull指定文件/夹，true为允许。
//在.git/info/sparse-checkout文件中（如果没有则创建）添加指定的文件/夹
 $ git pull origin master
```



## 3、git分区

git三个分区：工作区modified；暂存区staged；本地库committed；

- 工作区改完了代码，就用 `git add` 提交到暂存区。
- 从暂存区提交到本地库，`git commit -m "comment reason"`
- `git log` 可以查看到提交过的信息

工作区workspace =>【git add】 =>暂存区Index=>【git commit】=>本地库Local repository =>【git push】 =>远程库 remote repository

远程库 remote repository =>【git fetch】=>本地库Local repository

远程库 remote repository =>【git pull】=>工作区workspace

