---
title: 关于8月13号Git不再支持密码验证导致hexo无法更新的问题
comments: true
categories: 'hexo, Git'
tags: 'hexo, Git'
abbrlink: 963cd05b
date: 2021-08-15 19:52:22
---

# 关于8月13号Git不再支持密码验证导致hexo无法更新的问题

问题如

<img src="关于8月13号Git不再支持密码验证导致hexo无法更新的问题\image-20210815195459091.png" alt="image-20210815195459091"  />

本人昨天刚开始找了很久也没找到为啥，今天看了看这个发现了这个remote：,于是开始在网上查找解决方法，下面是我在Github官方目录上找到的解决办法。外加Git的设置。

## 首先是打开你的Github，找到右上角头像点击，选择settings。

<img src="关于8月13号Git不再支持密码验证导致hexo无法更新的问题\image-20210815195839994.png" alt="image-20210815195839994" style="zoom:80%;" />

## 点击红框框这个Developer settings

<img src="关于8月13号Git不再支持密码验证导致hexo无法更新的问题\image-20210815195945687.png" alt="image-20210815195945687"  />

## 然后按照图中做

![image-20210815200147681](关于8月13号Git不再支持密码验证导致hexo无法更新的问题\image-20210815200147681.png)

<img src="关于8月13号Git不再支持密码验证导致hexo无法更新的问题\image-20210815200633002.png" alt="image-20210815200633002" style="zoom: 80%;" />

## 最后复制token并记录在你信任的地方

![image-20210815200814560](关于8月13号Git不再支持密码验证导致hexo无法更新的问题\image-20210815200814560.png)

然后我们开始设置Git

> 这里提供的是不输入token不连续登陆，也就是永久记住密码和账号

## Git的设置

首先重置密码和账号（对于已经保存过也就是永久登录的用户）

```bash
git config --system --unset credential.helper
```

然后我们执行

```bash
git config --global credential.helper store //记住账号密码
```

后面就是三大指令：`hexo clean` `hexo g` `hexo d`

这个时候会要求你输入账号和密码。

根据官方文档密码为你的`token`，账号是你的用户名。（由于我已经设置过，这里不贴图了）

贴个官方文档参考。

[Creating a personal access token - GitHub Docs](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)

接下来，你就可以正常提交了，除非超时。

# 完

