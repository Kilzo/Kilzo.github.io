---
title: 使用hexo-abbrlink解决版权本文链接有中文乱码问题
comments: true
categories: hexo
tags: hexo
abbrlink: 3185eecb
date: 2021-08-04 16:26:59
---

# 使用hexo-abbrlink解决版权本文链接有中文乱码问题

## 安装插件

```C++
npm install hexo-abbrlink --save
```

## 配置站点配置文件`_config.yml`

```C++
permalink: post/:abbrlink.html   #若是按照上一篇中搭建的图片显示功能，请将html去掉即可正常显示图片
abbrlink:
  alg: crc32  # 算法：crc16(default) and crc32
  rep: hex    # 进制：dec(default) and hex
```

