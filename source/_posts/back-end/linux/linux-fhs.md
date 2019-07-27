---
title: Linux 文件系统层次标准(FHS)
date: 2018-05-04 18:30:00
categories: Linux
tags: 
  - linux
---

在Linux系统中，目录、字符设备、块设备、套接字、打印机等都被抽象成了文件（Linux系统中一切都是文件）。

Linux系统中的一切文件都是从“根（/）”目录开始的，并按照文件系统层次化标准[FHS](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)（Filesystem Hierarchy Standard）。采用树形结构来存放文件。另外，Linux系统中的文件和目录名称是严格区分大小写的，并且文件名称中不得包含“斜杠（/）”。

<!--more-->

Linux系统中常见的目录名称以及相应内容

|目录名称 | 应放置文件的内容|
|:-------- |:----------|
|/   |  主层次的根，也是整个文件系统层次结构的根目录|
|/boot | 开机所需文件—内核、开机菜单以及所需配置文件等|
|/dev | 以文件形式存放任何设备与接口|
|/etc | 配置文件|
|/home | 用户主目录|
|/bin | 存放单用户模式下还可以操作的命令|
|/lib | 开机时用到的函数库，以及/bin与/sbin下面的命令要调用的函数|
|/sbin | 开机过程中需要的命令|
|/media | 用于挂载设备文件的目录|
|/opt | 放置第三方的软件|
|/root | 系统管理员的家目录|
|/srv | 一些网络服务的数据文件目录|
|/tmp | 任何人均可使用的“共享”临时目录|
|/proc | 虚拟文件系统，例如系统内核、进程、外部设备及网络状态等|
|/usr/local | 用户自行安装的软件|
|/usr/sbin | Linux系统开机时不会使用到的软件/命令/脚本|
|/usr/share | 帮助与说明文件，也可放置共享文件|
|/var | 主要存放经常变化的文件，如日志|
|/lost+found | 当文件系统发生错误时，将一些丢失的文件片段存放在这里|
