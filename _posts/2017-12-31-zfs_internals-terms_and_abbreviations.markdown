---
layout:     post
title:      "ZFS Internals"
subtitle:   "Terms and Abbreviations"
date:       2017-12-31 00:00:00
author:     "lils"
header-img: "img/post-bg-unix-linux.jpg"
catalog: true
tags:
    - 文件系统
---

## Terms and Abbreviations
- ZPL(ZFS POSIX Layer): POSIX文件系统层，实现了vfs需要的接口，提供zfs文件系统API。  
- ZVOL(ZFS volume): block device模块，对外显示为一个块设备，用户空间可以像操作普通块设备一样操作zvol。  
- zpool: zfs文件系统将多块盘抽象成一个存储池(zpool)进行管理。  
- VDEV(virtual device): 一个zpool由多个盘组成，每个盘都是一个vdev, eg: zpool create zp1 /dev/sda1 /dev/sda2 /dev/sda3。  
- SPA(Storage Pool Allocator): 内存中zpool的数据结构，负责管理pool的空间申请和释放。  
- dnode: zfs中一切皆对象，dnode是表示对象的数据结构。  
- blkptr(block pointer): 一个对象由很多block组成，block有blkptr操作。  
- ZIO: zfs io framework，输入输出子系统，管理从磁盘读写数据的过程。  
- ARC(Adaptive Replacement Cache): 数据缓存模考，类似于传统文件系统的page cache层，进入ZIO前要先查缓存。  
- DMU(Data Managment Unit): 管理和操作zfs对象的模块。  
- _phy: 尾缀，表示ondisk的数据结构，例如dnode_phys。  
- DSL(Datasets and Snapshots Layer): 管理和做作数据集和快照的模块。  
- ZIL(ZFS Intent Log): 类似日志文件系统，io操作记录在log中。  
- ZAP(ZFS Attibute Processor): 存储zfs对象的属性。  
- TXG(Transaction Group): 事务组。  
- DBUF(DMU Buffer): 负责IO事务和COW机制的数据缓存。  
- zfs label: 位于vdev头部和尾部，用于描述vdev。  
- MOS(Meta Object Set): pool的元数据对象集，索引的起点。  
- uberblock: 类似于传统文件系统的super block，位于vdev label中,包含指向MOS的blkptr。  
- mateslab: 负责空间管理，内存结构。  
- spacemap: 负责空间管理，盘上结构。  
- DVA(Device Virtual Address): blkptr中的数据结构，描述block位于哪个vdev和offset。  
- metanode: 对象集或pool中的元数据对象，通过该对象可以找到文件系统的根目录对象"/"。

![zfs_architecture_diagram](/img/in-post/zfs_architecture_diagram.png)
					
