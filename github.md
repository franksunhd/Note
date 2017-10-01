## 源码管理工具GIT 的使用

[TOC]

- SVN : 是一个开放源码的版本控制系统,不是分布式的.
- GitHub 是存储源码的,(林纳斯-托瓦兹 linus Tovals)-- kernel / git

### 1.安装GIT

```shell
$ sudo apt-get install git
```

### 2.创建版本库(本地仓库)

```shell
$ mkdir demo
$ cd demo
```

#### 1) git init 将当前目录创建为GIT仓库

- .git 为隐藏目录

#### 2) 创建README文件

- 仓库中没有文件,创建一个README文件,用来存放每次修改信息

```shell
$ vim README
或者 
$ touch README
```

#### 3) git status 查看当前目录下的文件状态

#### 4) git add filename 跟踪文件

```shell
$ git add .
```

- 跟踪文件,加入git 版本库,完成之后状态修改.

#### 5) 配置用户信息

##### 配置用户名

```shell
$ git config --global user.name "franksun"
```

##### 配置Email

```shell
$ git config --global user.email "sun_si_yan@163.com"
```

##### 配置VIM

```shell
$ git config --global core.editor vim
```

#### 6) 提交

```shell
$ git commit
```

#### 7) 查看提交信息

```shell
$ git log
```

#### 8) 删除文件恢复

```shell
$ rm filename
$ git checkout filename
```

- 只有文件修改过 未提交前或用rm 误删时会出现

#### 9) 从仓库中删除文件

```shell
$ git rm filename
$ git commit
```

- 并没有从仓库真正删除,需要commit提交记录

#### 10) 版本回退

- 一次提交就是一次版本更新
- 回退到提交版本

```shell
$ git reset --hard commitID
```

- 这个命令后,使用 git log命令不会查到所有的log信息,不会获取到这个ID之后的ID
- git reflog 相当于一个列表,需要使用reset命令恢复

#### 11) 忽略文件

```shell
$ touch .gitignore
```

- 这个目录下可以存放a.out等编译文件,文件都在跟踪时忽略

#### 12) 版本之间对比

```shell
$ git diff
//在提交之后重新修改并未跟踪提交有效
```

**若跟踪并提交则需使用**

```shell
$ git diff commitD1 commitD2

/*
提示:
diff --git a/hello.c b/hello.c
...
---a/hello.c
+++b/hello.c

@@ -1,7 +1,13 @@  //原有1~7行,增加6行,+1~13
*/
```

#### 13) patch

- 指补丁,这里更多是指程序的一些BUG,需要我们进行fixed,那fixed源码文件就是patch
- patch 实际就是保存两个文件的差异
- 用git 生成patch

```shell
$ git format-patch -p1
```



- git 打 patch 就是已经有patch 文件了,但客户端版本低,打patch可以修补文件

```shell
$ git am patch-name
```

### 3.分支

- 工作流:是对工作流程及其各操作步骤之间业务规则的抽象,概括(workflow)描述.工作流建模即将工作流程中的工作如何前后组织在一起的逻辑和规则,在计算机当中以恰当的模型表达并对其实施计算.
- 工作流管理系统:是处理工作流的电脑软件系统.(WFMS)

#### 1) 创建分支

```shell
$ git checkout -b 分支名 标签名
```

- 可根据标签名创建分支并切换

```shell
$ git branch 分支名(-dev)			//只是创建,没有切换
$ git checkout -b 分支名			//创建并切换
```

一般包括的分支有:

- master 主分支 (发布版)
- develop 开发部分
- hotfixes 紧急的
- release branches 测试部分
- feature branches 与开发部分同级同步

#### 2) 显示分支

```shell
$ git branch -av 
```

- 显示当前仓库有多少分支

#### 3) 切换分支

```shell
$ git checkout 分支名
```

#### 4) 删除分支

```shell
$ git branch -D 分支名
```

#### 5) 合并分支(merge)

```
$ git checkout master
$ git merge develop
```

- 若出现冲突

```shell
$ git mergetool
```

### 4.标签 

#### 1) 什么是标签

- 标签就是给提交 标识上易懂的名称
- GIT可以使用2中种标签名称:轻标签和注释标签

#### 2) 创建标签

- 为最新的版本设置标签

```shell
$ git tag 标签名
```

- 为指定的ID设置标签

```
$ git tag 标签名 ID值
```

#### 3) 显示标签

- 显示现在所有的全部标签

```shell
$ git tag
```

- 显示包含标签资料的历史资料

```shell
$ git log --decorate
```

#### 4) 删除标签

```shell
$ git tag -d 标签名
```

#### 5) 同步标签

```shell
$ git push origin --tags
```

### 5.远程仓库

#### 1) 添加远程仓库

- 首先在github上创建一个目录
- 在本地仓库目录下执行

```shell
$ git remote add origin URL
```

- 实现远程仓库和本地仓库的关联
- 相关的URL可在  .git/config 文件中找到

#### 2) 查看分支状态

```shell
$ git branch -av
```

- 若不同步,分情况讨论:是同步到远程还是同步到本地

#### 3) 远程仓库同步到本地

- 只是同步差异,而且只是查,不是真正同步.

```shell
$ git fetch origin
$ git pull
```

- 适合于已经拉去文件到本地,但服务器的git 已经更新.

#### 4) 远程仓库克隆到本地

- 本地没有目录,并且克隆全部信息

```shell
$ git clone URL 
```

#### 5) 本地仓库同步到远程

```shell
$ git push -u origin 远程分支名(master)
```

#### 6) 如何删除远程服务器GITHUB的文件及文件夹

**按照以下步骤即可(本地删除)**

1. git pull (you git url)
2. git checkout
3. rm -r (dirName)
4. git add --all
5. git commit -m "remove (dir)"
6. git push -u origin master
7. input your name and password




























