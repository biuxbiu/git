# Git

`Git` 的一些常规操作

## 目录

* [查看你的git设置](base/?id=查看你的git设置)
* [设置账户关联](base/?id=设置账户关联)
* [初始化一个仓库](base/?id=初始化一个仓库)
* [添加到暂存区](base/?id=添加到暂存区)
* [提交到本地版本库](base/?id=提交到本地版本库)
* [commit提交规范](base/?id=commit提交规范)
* [推送到远端](base/?id=推送到远端)
* [修改分支名字](base/?id=修改分支名字)
* [查看状态](base/?id=查看状态)
* [拷贝一个仓库到本地](base/?id=拷贝一个仓库到本地)
* [分支操作](base/?id=分支操作)
* [创建远程分支在本地](base/?id=创建远程分支在本地)
* [设置当前仓库的git地址](base/?id=设置当前仓库的git地址)
* [合并分支](base/?id=合并分支)
* [查看提交历史](base/?id=查看提交历史)
* [Git工作流](base/?id=Git工作流)
* [新建本地仓库一波流](base/?id=新建本地仓库一波流)
* [常见问题](base/?id=常见问题)
    * [push 问题](base/?id=push-问题)
    * [windows 的 Authentication 问题](base/?id=windows-的-Authentication-问题)
    * [port 443](base/?id=port-443)
* [杀进程](base/?id=杀进程)
* [查看提交记录](base/?id=查看提交记录)
* [查看最近一次提交的内容](base/?id=查看最近一次提交的内容)
* [放弃本地的的修改](base/?id=放弃本地的的修改)
* [比较两个文件的差异](base/?id=比较两个文件的差异)
* [删除已经新增的文件或者文件夹](base/?id=删除已经新增的文件或者文件夹)
* [git log中文乱码](base/?id=git-log-中文乱码)


## 查看你的git设置

```
git config --list
```

## 设置账户关联

```
git config --global user.name "biuxbiu"
git config --global user.email "xxx@example.com"
```

## 初始化一个仓库

```
git init
```

## 添加到暂存区

你初始化一个仓库之后，你可以往里面添加一个文件，然后使用 `git add` 方法将这个文件添加到暂存库

```
git add -u      //添加更新过的文件到暂存区
git add -A      //添加全部文件(包括修改过的，新增的，删除的等等文件)到暂存区
git add .       //添加所有修改到暂存区
git add *.js    //将 .js 结尾的文件所有修改添加到暂存区
git add js-*    //将 js- 开头的文件所有修改添加到暂存区
```

## 提交到本地版本库

然后使用 `git commit` 方法将提交版本到本地仓库

```
git commit -m 'message'      
```

<br>
<br>

#### commit提交规范

```
feat：新增 feature
fix：修复 bug
hotfix：紧急修复 bug
docs：仅修改文档，比如 README, CHANGELOG, CONTRIBUTE等等
refactor：代码重构，没有加新功能或者修复 bug
chore：改变构建流程、或者增加依赖库、工具等
revert：回滚到上一个版本
style：仅修改空格、格式缩进、逗号等等，不改变代码逻辑
test：测试用例，包括单元测试、集成测试等
```

## 推送到远端

然后使用 `git push` 方法将提交版本推送到远端仓库

```
git push  
```

!>当你 `git push` 的时候，可能会出现以下的情况：
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.
    git pull `<remote>` `<branch>`
If you wish to set tracking information for this branch you can do so with:
    git branch --set-upstream-to=origin/`<branch>` master

那是因为你没有和远端分支建立关系

```
git branch --set-upstream-to origin/master master
```

!>如果你遇到<br>
fatal: branch 'master' does not exist

那是因为你不在这个分支上，你需要切换回到这个 `master` 分支，然后在进行操作：

```
git checkout master
```

!>如果你本地是一个分支，然后想拉远端的一个分支，那你也要跟远端分支建立关系

假设我本地有一个 `dev` 分支，想跟远端的 `dev` 分支建立关系的话：

```
git branch --set-upstream-to origin/dev dev

//origin/dev 是远端的分支
//dev 是本地的分支

//或者你可以直接
git branch -u origin/dev        //直接关联远端分支
```

!>有时候即便你关联了，但是你每一次 `push` 的时候都会提示你 `git push HEAD:origin xxxxx` 这样的情况出现，那有可能是因为你本地的分支名字与远端的分支名字不一致导致的，所以你最好需要改一下分支名字；

## 修改分支名字

说改就改

```
git branch -m oldName newName
```

!>注意，本地分支的名字最好不要有 `origin` ，因为在关联的时候，如果你的本地分支也出现 `origin` 的字眼，`git` 会难以判断含糊不清，难以判断。所以，如果你远端分支如果是 `origin/dev-biubiu`,那你本地最好就是 `dev-biubiu` 。不要含有 `origin` 字眼。


>如果你要看关联的分支信息，你可以执行 `git branch -vv` （两个 v） ，就可以看到你每个本地分支所捆绑的远端分支。

如果你只是要拉取远端最新的分支内容的话，你只需要

```
git pull git@xxxxxxx.git dev
//git@xxxxxxx.git 远端的 remote
//dev remote 上，你要拉的分支
```

!>当你遇到 `git push origin HEAD` 和 `git push origin HEAD:master` ，你就要看看本地分支是否与远端仓库准确的关联拉了。

你可以查看以下本地分支与远端分支的关联情况：

```
git branch -vv              //两个 `v`
```

## 查看状态

```
git status              //查看本地仓库的状态
git status -s           //列出本地仓库的增删改动文件
                        //(A 新增，M 修改，D 删除，?? 未添加到Git中)
```

## 拷贝一个仓库到本地


```
git clone [gitUrl]                              //从远程仓库拷贝一个版本库到本地
git clone [gitUrl] [localUrl]                   //从远程仓库拷贝一个版本库到指定目录
git clone [gitUrl] -b [localUrl]                //从远程仓库拷贝一个指定版本库到本地
git clone [gitUrl] -b [localUrl] 【localUrl】    //从远程仓库拷贝一个指定版本库到指定目录
```


## 分支操作

```
git branch                  //查看本地仓库所有分支
git branch -vv              //查看分支的关联信息
git branch -a               //查看远端和本地的所有分支
git branch -r               //查看远程分支
git branch -b dev           //新建一个 `dev` 分支
git branch dev              //本地创建 `dev` 分支
git branch dev -d           //删除 `dev` 分支
git branch -m dev pro       //更改分支名字
git checkout -b dev         //本地创建 `dev` 分支并且切换到 `dev`分支
git checkout dev            //切换到 `dev`分支
git checkout .**            //放弃所有更改
git checkout fileName       //放弃对 `fileName` 的所有更改
git push                    //push 所有分支
git push origin master      //推送的远端的主分支
git push origin dev         //推送的远端的 `dev` 分支
git push origin -d dev      //删除远端的 `dev` 分支
git push -u origin master   //将本地分支推送到远程，如果远程没有分支，建立它并把它设置为主分支
```

#### 创建远程分支在本地

有时候我们需要将远端分支拉下来，并且创建一个分支

```
git checkout -b dev origin/dev

// dev 是本地的分支名字
// origin/dev 是远程分支
```

**举个例子**

```
git checkout -b dev-biubiu origin/dev-biubiu
//dev-biubiu  本地分支的名字
//origin/dev-biubiu 远端分分支名字
```

把某个分支拉取到本地

```
git pull origin dev-biubiu
```

## 设置当前仓库的git地址

```
git remote add origin [url]         //将 [url] 的地址作为本地仓库的地址
git remote rm origin                //删除当前仓库地址
```

!>更换 `git` 地址的话，其实就是先删除这个 `git url` 然后再重新添加就好

```
git remote rm origin
git remote add origin [url]
```

## 合并分支

```
git add -A                      //你需要先把 `dev` 分支提交到远程
git commit -m 'dev'
git push        
git checkout master             //然后你需要切换到主分支 `master`
git merge dev                   //合并 `dev` 分支到 `master` 主分支
```

## 查看提交历史

```
git log                 //查看提交历史
git log [commitId]      //查看某次 `commit` 提交的内容
git log -p [fileName]      //查看某次 `commit` 提交的内容
git log --pretty=oneline
```

## Git工作流

我们平常在修改之后基本会有哪几个命令会用到的？

```
git status               //先检查一下本地的修改
git add -A               //将修改的部分添加到暂存区
git commit -m 'xxx'      //添加注释
git pull                 //拉取远程最新的代码
git push                 //推送到远端
```

## 新建本地仓库一波流

你可以新建一个本地仓库，然后尝试执行以下操作：

```
git init                                //新建一个仓库
git add -A                              //把文件提交到暂存区
git commit -m 'new repository'          //把暂存区的文件提交到本地仓库
git remote add origin [url]             //设置远端服务器的 'git' 地址
git push -u origin master               //把仓库对送到远端服务器的主分支
```

如果已经初始化，只需要添加仓库地址就好：

```
git remote add origin [gitUrl]
git push -u origin master
```

## 常见问题

#### push 问题

!>fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream

意思是没有与远程分支建立关系，需要跟远程分支建立关系之后才能推送；

解决方法：
```javascript
git push -u origin master
```

<br>
<br>

#### windows 的 Authentication 问题

!>fatal: Authentication failed for 'http://xxxxx.git/'

解决方法：

```
这个问题是因为管理凭证出现了问题，需要重新设置一下就好；

打开 `控制面板` - `用户账户` - `凭证管理器` 

将你的凭证都删掉了，然后重新回到终端执行命令与句，它会弹出弹窗要你输入账户和密码。输入正确就 ok 了。
```

<br>
<br>

#### port 443

!>fatal: unable to access 'https://github.com/xxxxx/xxx.git/': Failed to connect to github.com port 443: Timed out

这个问题可能是代理的问题，有时候是因为网路不稳定的问题造成的，如果还是不行的话，重新设置代理或者取消代理试试。

解决方法：

```
//重置代理
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy http://127.0.0.1:1080

或者

//取消代理
git config --global --unset http.proxy
git config --global --unset https.proxy
```

## 杀进程

先做一个记录，后面详细说明一下：

```
netstat -aon|findstr "80"

//TCP    127.0.0.1:49180        127.0.0.1:49181        ESTABLISHED     2120
//TCP    127.0.0.1:49181        127.0.0.1:49180        ESTABLISHED     2120
//TCP    127.0.0.1:59179        127.0.0.1:59180        ESTABLISHED     5172
//TCP    127.0.0.1:59180        127.0.0.1:59179        ESTABLISHED     5172
//TCP    [::]:80                [::]:0                 LISTENING       1168

//然后查看目前的端口是谁在使用；看到 `1168` 在使用，那我们就看看 `1168` 对应的应用程序是哪个

tasklist|findstr "1168"

//httpd.exe                     1168 Services                   0     17,356 K


//找到这个对应的应用程序是 `httpd.exe` 之后就讲这个应用程序杀死

taskkill -f -t -im httpd.exe

//成功: 已终止 PID 2308 (属于 PID 1168 子进程)的进程。
//成功: 已终止 PID 1168 (属于 PID 840 子进程)的进程。
```

## 查看提交记录

```javascript
git log
```

## 查看最近一次提交的内容

我们还可以查看提交的内容简要

```
git log -1 --stat           //查看最近1次提交的内容
git log -3 --stat           //查看最近3次提交的内容
```

我们也可以查看指定的 `commit` 内容

```javascript
git show da29aad58eeec803     //后面为 `commit` 的版本号
```


## 放弃本地的的修改

```
git checkout .                                  //放弃本地的所有修改，注意有一个点
git checkout static/src/pages/index.css         //放弃对本地 index.css 的修改
git checkout static/src/pages/index.html        //放弃对本地 index.html 的修改
git checkout static/src/pages/index.js          //放弃对本地 index.js 的修改
```

## 比较两个文件的差异

比较两个不同的文件

```
git diff                                    //查看尚未暂存的文件更新了哪些部分
git diff filename 　　　　　　                //查看尚未暂存的某个文件更新了哪些
git diff –cached                            //查看已经暂存起来的文件和上次提交的版本之间的差异
git diff –cached filename 　　               //查看已经暂存起来的某个文件和上次提交的版本之间的差异
git diff ffd98b b8e7b0		                //查看某两个版本之间的差异
git diff ffd98b:filename b8e7b00:filename   //查看某两个版本的某个文件之间的差异
```

## 删除已经新增的文件或者文件夹

```
git clean -n    //查看将要删除的内容
git clean -f   //删除已经新增的文件
git clean -df  //删除已经新增的文件和文件夹
git clean -xdf  //删除所有文件，包含隐形文件
```

## git log 中文乱码

安装了 `oh-my-zsh` 之后发现 `git log` 的中文乱码了，只需要执行

```
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
```

>执行了之后需要将终端重启。




## git 中的存储

有时候我们在 `dev` 分支改一个文件，然后需要回到 `master` 分支去改别的东西，这个时候如果没有 `存储` 我们的修改，我们是切不去 `master` 的。

所以我们要把他 `存储` 起来:

```
git stash
```

<br>

改完之后想要回到 `dev` 分支，我们需要把 `存储` 的修改给释放出来，这个时候我们要执行：

```
git stash pop

//或者

git stash apply
```





[...]
