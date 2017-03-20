---
title: github SSH 配置
date: 2017-03-05 16:51:45
tags: github 
---

电脑上有公司的git仓库，为了避免和github冲突，新建一对key添加到github中去，
以下是操作步骤：
```
#添加钥匙对
ssh-keygen -t rsa -b 4096 -C "youremail@xxx.com" -f /Users/username/.ssh/github_rsa
一路回车

#注意修改私钥权限
chmod 700 ~/.ssh/github_rsa

#启动ssh-agent
eval "$(ssh-agent -s)"

#将刚才添加的key放到ssh-agent中去
ssh-add -K ~/.ssh/github_rsa

#修改~/.ssh/config
添加
Host github.com
    IdentityFile ~/.ssh/github_rsa

pbcopy < ~/.ssh/github_rsa.pub
此时公钥已经复制到剪贴板，在github setting中add ssh key即可
```
[github官方配置指南](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
