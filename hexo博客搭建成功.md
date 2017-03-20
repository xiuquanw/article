---
title: hexo博客搭建成功
date: 2017-03-04 22:01:48
tags: hexo 
---


花费3个小时，基于hexo搭建的博客终于成功上线了！
引用参考攻略，谢谢你们的技术分享：
> * [hexo简介、安装、部署](https://lanjingling.github.io/2015/09/23/hexo%E7%AE%80%E4%BB%8B/)
> * [hexo使用心得（一）](https://lanjingling.github.io/2015/09/24/ues-of-hexo-1/)
> * [hexo使用心得（二）](https://lanjingling.github.io/2015/09/24/use-of-hexo-2/)
> * [hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)



## 一些踩坑记录

### hexo DTraceProviderBindings MODULE_NOT_FOUND

虽然不影响使用但是还是逼死强迫症的节奏啊
附解决方案：
```
$ npm install hexo --no-optional
```
或者重装hexo-cli
```
$ npm uninstall hexo-cli -g
$ npm install hexo-cli -g

```

### git 部署报错

总是提示push的权限不对，到了一个错误的帐号，隐约记得之前用过一起其他github帐号push过代码，但是已经改了.ssh/config文件 ssh-add 也修改了，还是不起作用,于是乎google了一把
终于找到一个相近的问题
http://stackoverflow.com/questions/5335197/gits-famous-error-permission-to-git-denied-to-user

问题基本明朗了，mac的钥匙串缓存了github的信息，删除掉即可
操作步骤如下：
> * Open "Keychain Access.app" (You can find it in Spotlight or LaunchPad)
> * Select "All items" in Category
> * Search "git"
> * Delete every old & strange items
> * Try to Push again and it just WORKED
