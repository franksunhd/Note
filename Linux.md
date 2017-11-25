## Linux软件包管理、文件传输服务(TFTP)器的配置、网络文件系统NFS的配置

[TOC]

### 1. Linux软件包管理

#### 软件包管理机制

- 对操作系统上的软件进行管理的机制

Linux 常见的软件包机制:

- RPM  软件包 (常用命令:rpm  yum)
- DEB  软件包  (常用命令:dpkg  apt-get)

### 2. Deb软件包机制

#### 1) 本地安装包管理

- 安装

```shell
$ sudo dpkg -i sl_3.03-17_amd64.deb
```

- 卸载

```shell
$ sudo dpkg -r sl
```

- 彻底卸载(包括配置文件)

```shell
$ sudo dpkg -P sl
```

- 查看安装状态

```shell
$ sudo dpkg -s sl
```

- 查看安装路径

```shell
$ sudo dpkg -L sl
```

- 列出所有安装的软件包

```shell
$ sudo dpkg --get-selections
```

#### 2) 在线安装包管理

- 更新本地源

```shell
$ sudo apt-get update
```

- 软件包安装

```shell
$ sudo apt-get install sl
```

- 软件包卸载

```shell
$ sudo apt-get remove sl
```

- 软件包彻底卸载

```shell
$ sudo apt-get remove --purge sl
```

- 二进制软件包下载

```shell
$ sudo apt-get download sl
```

- 软件包源码下载

```shell
$ sudo apt-get source sl
```

- 查看软件包的安装状态

```shell
$ sudo apt-cache policy sl
```

- 查看软件包信息

```shell
$ sudo apt-cache show sl(无论是否安装)
```

- 升级软件包

```shell
$ sudo apt-get upgrade
```

#### 3) deb包相关配置文件

- / etc / apt / sources.list  包含deb软件包源的文件
- / var / lib / apt / list / * 对软件源进行更新之后的本地软件
- / var / cache / apt / archive 在线安装时的软件包下载目录
- / var / log / dpkg.log 本地软件包管理的日志文件
- / var / log / apt / *.log  在线软件包管理的日志文件

### 3. 文件传输服务器(TFTP)的配置和使用

#### 1) 概念

- 简单文件传输协议:是TCP/IP协议族中用来连接客户机和服务器之间进行简单文件传输的协议.(端口:69)
- 它只可以实现上传和下载文件的功能

#### 2) 安装客户端和服务端

- 检查状态

```shell
$ sudo dpkg -s tftpd-hpa
$ sudo dpkg -s tftp-hpa
```

- 安装

```shell
$ sudo apt-get update
$ sudo apt-get install tftpd-hpa
$ sudo apt-get install tftp-hpa
```

- 配置

```shell
$ sudo vi /etc/default/tftpd-hpa
//修改最后一行 --secure -c -l
```

- 启动服务(在root下)

```shell
service tftpd-hpa start
```

- 重启服务

```shell
service tftpd-hpa restart
```

- 停止服务

```shell
service tftpd-hpa stop
```

#### 3) TFTP服务测试

- 客户端连接服务器 

```shell
tftp IP地址
```

- 输入上传文件命令

```shell
put 文件名
```

- 输入下载文件命令

```shell
get 文件名
```

- 退出

```shell
quit
```

### 4.Linux网络文件系统NFS配置和使用

#### 1) 概念

- 网络文件系统NFS是FreeBSD支持的文件系统的一种,它允许网络中的计算机通过TCP/IP网络共享资源.

#### 2) 安装和配置

- 检查状态

```shell
$ sudo dpkg -s nfs-kernel-server
```

- 在线安装

```shell
$ sudo apt-get update
$ sudo apt-get install nfs-kernel-server
```

- 配置

```shell
/etc/expotts
```

> eg:  / nfs_dir  * (rw , sync ,  no_subtree_check , no_root_squash )
>
> nfs_dir 路径  
>
> \* 主机名  
>
> sync操作同步
>
> no_subtree_check 不进行子目录检查
>
> no_root_squash 默认root下

根目录下创建目录

> nfs_dir
>
> mkdir nfs_dir
>
> chmod 777 nfs_dir/

- 启动服务

```shell
service nfs-kernel-server start
```

- 重启服务

```shell
service nfs-kernel-server restart
```

- 停止服务

```shell
service nfs-kernel-server stop
```

#### 3) 测试

- 创建一个挂载目录

```shell
$ mkdir /mount_nfs
```

- 客户端挂载远程NFS服务器

```shell
$ mount -t nfs 192.168.1.100 : /nfs_root_dir / mount_nfs
//              远程IP地址       远程目录		本地目录
```

- 挂载成功后操作本地,目录就相当于操作远端目录
- 取消挂载

```shell
$ umount /mnt
```

> nfs_dir 远程目录 file1 file 2 file 3
>
> mnt 本地目录

```shell
$ mount -t nfs 127.0.0.1 :/ nfs_dir / mnt
```

### 5.Linux 系统

#### 1) Linux文件系统

- 是操作系统用于明确存储设备或分区的文件和方法

**分类**

- 磁盘文件系统:本地主机实际可访问 eg:磁盘
- 网络文件系统:可远程访问 eg:NFS
- 专有/虚拟文件系统:不驻留在磁盘 eg:procsys

#### 2) 文件的归档和压缩

- 使用gzip和gunzip 对文件进行压缩和解压缩
- 使用bzip2和bunzip2对文件进行压缩和解压缩
- 使用tar对文件进行压缩和解压缩

```shell
//压缩
gzip 文件名.gz		
//解压缩
gunzip 文件名

//压缩
bzip2 文件名.bz2	
//解压缩
bunzip2 文件名.bz2

//压缩
tar czf 文件名.tar.gz		文件目录
tar cjf 文件名.tar.bz2		文件目录
tar cJf 文件名.tar.xz		文件目录
(c:表示创建;	z:表示gz格式;	j:表示bz2格式;	J:表示xz格式;	f:文件目录;)
// 解压缩
tar xzf 文件名.tar.gz
tar xf 文件名.tar.() 是什么就解成什么
```

#### 3) shell通配符

- 通配符是一种特殊的语句,由特殊字符构成,常用来模糊搜索,使用时可以代替一个或多个真正字符.
- \*

> eg :ls *  
>
> ls *.sh
>
> ls file*

- ?(任意一个)

> ls file_?

- [ ]\(只指定[ ]中的字符)

> ls file_[0123]

- [ c1 - c2]\(指定c1 到c2 区间)

> ls file_[0-3]

- [! ]\(不取[ ]中的)
- [^ ]

> ls file_[!0-3]
>
> 两位数:
>
> ls file_[0-9]\[0-9]

- ^ 和 ! 效果相似

> ls file_\[^ 0-5]*

- { }

> ls file_{0,5,9}

#### 4) 用户和组

- 用户分类
  - 超级用户:具有最高权限
  - 系统用户:服务于应用维护系统运行不能登录
  - 普通用户:登录用户
- 组分类
  - 主族
  - 附属组
- 用户和组相关文件

```shell
/etc/passwd		用户数据文件,包含用户数据信息
/etc/group		描述组的文件
/etc/shadow		用户加密的密码文件
```

- 添加用户和组

```shell
adduser / useradd
addgroup / groupadd

adduser ssy
useradd -s /bin/bash -m -g linux ssy

addgroup ssy
groupadd ssy
```

- 对用户的操作

```shell
usermod -s /bin/sh newuser2		修改用户2的bash为sh
usermod -G newuser1 newuser2	把用户2所属组再添加到组1中

gpasswd -d newuser2 newuser1	使用户2从组1中删除
gpasswd -a newuser2 newuser1	把用户2再添加回组1中

passwd ssy	修改用户密码
```

- 对组的操作(删除用户和组)

```shell
deluser newuser --remove-home	删除用户同时删除目录
userdel newuser		只删除newuser 不删除家目录

groupdel / delgroup  newuser	删除组
```

- 系统管理的相关命令

```shell
$ shutdown -r now/+60	重启 +60
$ shutdown -h now/+60	关机 +60
```

- 查看磁盘空间

```shell
$ df -h		//直观看到有多少G
$ df -aTh 	//详细
```

- 查看目录和文件大小

```shell
$ du -h home	//Home目录下的文件目录和大小
```

- Samba软件

```shelll
windows的格式为NTFS,Linux的格式为EXT4,Samba软件用于两者之间的格式转换.
```

























