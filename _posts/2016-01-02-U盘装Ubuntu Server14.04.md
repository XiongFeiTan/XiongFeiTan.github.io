---
layout: post
title: U盘装Ubuntu Server14.04
categories: [ubuntu, server]
comments: true
description: U盘装Ubuntu Server 14.04 CDROM 无法挂载或无法检测问题，小问题.
---

## U盘装Ubuntu Server 14.04 CDROM 无法挂载或无法检测问题

---

* 1，刻录好盘之后，再把ISO文件拷贝到U盘里面。

* 2，电脑重启设置U盘启动。

* 3，直接安装。。。

* 4，无法检车CDROM时，回到安装menu中，选择进入shell。

* 5，输入ls /dev/sd*, 查看设备，如：/dev/sda /dev/sda1 /dev/sda3 /dev/sda5 /dev/sdb /dev/sdb4 。

* 6，U盘就是/dev/sdb ,U盘上的分区就是dev/sdb4

* 7，然后在根目录下，创建文件夹：mkdir usbdev

* 8，再把U盘挂载到这个目录下面：mount /dev/sdb4 /udev

* 9，然后挂载U盘中的ISO文件：mount /usbdev/ubuntu-14.04.3-server-amd64.iso  /cdrom

* 10，exit ，退出后继续安装就可以解决。

---










