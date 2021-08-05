---
title: 关于hexo yun主题(本主题)代码高亮问题的解决
comments: true
categories: hexo
tags: hexo
abbrlink: cbd6015b
date: 2021-08-05 13:35:11
---

# 关于hexo yun主题(本主题)代码高亮问题的解决

> 实际上也不能称作(`yun`主题)是本主题，只是利用了`yun`主题的模板，在这还是要感谢[云游君](https://www.yunyoujun.cn/about/)(`yun`主题的作者)给我们提供了这么漂亮的主题
>
> 另外提一下，这里用的是prism，用highlight的可以关闭这个无用网页了。

## 1. 禁用highlight

打开根目录下的`_config.yml`文件，修改配置

```bash
highlight:
  enable: false
···········
```

## 2. 获取prism

下载页面：[https://prismjs.com/download.html](https://links.jianshu.com/go?to=https%3A%2F%2Fprismjs.com%2Fdownload.html)；选择你喜欢的 theme 主题、（想要支持的）language 支持的语言（不要选太多，够用就好）、plugin 插件（可以选Line Numbers、Copyto Clipboard Button，其他的看自己需求）；然后点击下载按钮就行了；下载到本地之后，将它们重命名为 `prism.js`、`prism.css`，然后将它们放置到 `/themes/next/source/js/prism/` 目录下（prism 文件夹需要自己新建），即它们的路径是：

```bash
/themes/yun/source/js/prism/
```

## 3. 配置 prism

- 修改 `themes/next/layout/_partials/head.pug`，在尾部添加以下代码：

```js
<link rel="stylesheet" href="/js/prism/prism.css">
```

- 修改 `themes/next/layout/_partials/footer.pug`，在尾部添加以下代码

```js
<script src="/js/prism/prism.js" async></script>
```

## 4. 修改博客配置

打开根目录下的`_config.yml`文件，添加下面代码

```yml
marked:
  langPrefix: line-numbers language-
```

## 4. 测试prism

清理后，重新运行直接测试

```undefined
hexo clean
hexo g
hexo s
```

