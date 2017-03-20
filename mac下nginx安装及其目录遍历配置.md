---
title: mac下nginx安装及其目录遍历配置
date: 2017-03-19 22:50:25
tags: nginx
---

>背景：mac开发机，本地搭建nginx服务，对服务端存储的文档做展示。

## 安装nginx
直接通过brew安装
```
brew install nginx
```

## 启动nginx
```
nginx
```

## 停止nginx
```
nginx -s stop
```

## 重新加载nginx
```
nginx -s reload
```

## 配置文件遍历
```
vi /usr/local/etc/nginx/nginx.conf
# server 节点
location /share {
            root   /Users/yourusername/dir_needed_share;
            autoindex on;
            autoindex_exact_size off;
            autoindex_localtime on;
        }
```
几个关键点：

- /share 和root 配置的目录必须是可达到的路径 <font color=#FF0000>**即/Users/yourusername/dir_needed_share/share 此路径可达，否则访问时会报404**</font>
- autoindex 为必填选型 默认开启  
- autoindex_exact_size off 则会将文件的大小以合适的单位显示M,G等，否则显示字节数

## 一些文件路径
用brew安装的nginx 一些文件路径不一样需要注意

- 安装目录
```  
/usr/local/Cellar/nginx/1.10.3
```   

- 配置文件路径
```  
/usr/local/etc/nginx/nginx.conf
``` 

- 日志文件路径
```    
/usr/local/var/log/nginx $ ls -lrt
total 80
-rw-r--r--  1 staff  admin  29646  3 19 14:45 access.log
-rw-r--r--  1 staff  admin   6430  3 19 19:11 error.log
```   
