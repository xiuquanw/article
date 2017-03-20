---
title: mac os ftp配置使用实践
date: 2017-03-19 15:42:00
tags: mac ftp
---

> 需求背景：mac的文件系统和移动硬盘的ntfs文件系统不兼容，如何传文件变成了一件有意思的事情，本文将剑走偏锋，通过FTP实现文件传输需求。

## 启动ftp服务
mac 默认是有ftpd的服务，但是并未开启，需要执行以下命令
```
sudo -s launchctl load -w /System/Library/LaunchDaemons/ftp.plist
```
服务检查，如果显示server ready，则表示FTP服务已经OK
```
 ~ :ftp localhost
Trying ::1...
Connected to localhost.
220 ::1 FTP server (tnftpd 20100324+GSSAPI) ready.
```
这就完了？当然不，这个时候使用client访问的时候，发现默认会显示用户home目录下的所有东西，处于解决强迫症和安全性考虑，需要改一下，那么就继续下面的配置吧!

## 配置ftp服务
### 配置哪些用户才能使用ftp
```
sudo vi /etc/ftpusers

#内容如下
yourusername allow shareGroup
* deny
```
简单解释一下:
行1：指定的用户可以访问，并定义的一个class[shareGroup] ，非常重要，后面配置chroot需要。
行2：其他所有用户都拒绝访问。
### 配置用户的root目录
这个就是解决ftp登录上去之后所能看到的根目录
```
sudo vi /etc/ftpd.conf

#内容如下
umask all 022
chroot shareGroup /Users/yourusername/dir
```
### 重启ftp服务
```
sudo -s launchctl unload -w /System/Library/LaunchDaemons/ftp.plist
sudo -s launchctl load -w /System/Library/LaunchDaemons/ftp.plist
```

## 关闭ftp服务
处于安全考虑，用完ftp服务就关了吧，unload即可。
```
sudo -s launchctl unload -w /System/Library/LaunchDaemons/ftp.plist
```

## ftp客户端
- chrome浏览器 直接ftp://your_ftp_server_ip
- FlashFXP 一个超级好用的client

