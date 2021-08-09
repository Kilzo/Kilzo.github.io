---
title: yun主题的页面背景透明和左侧菜单栏透明修改
comments: true
tags: hexo
abbrlink: cf1abab9
date: 2021-08-09 20:07:24
categories:
---

> 今天是本人少数肝博客更新肝一下午的一天，这个主题真的是简直毫无教程。全程自己摸索。不过也学到好多东西。
>
> 本文对所有主题（Hexo）生效的一点估计就在开头的控制台介绍了。

在开始之前，我bing查询了一些大伙怎么修改文章透明，发现没一个对的上的，（其实我也没一个个试），偶然间看到了网页F12进入开发者模式（也就是大家俗称的控制台），在元素中可以看到每一个模块在哪个文件。更加坚定了自己手动修改的目的。于是乎，下面开始了。（这里是全透明，不含透明百分数，想要百分比透明的可以跳过了。)

> 首先先说说像我这样的小白怎么整这个控制台。

# 首先打开你的博客/网站目录

在你的博客目录右键打开Git Bash Here,输入三连，`hexo clean` 、`hexo g`、 `hexo s`打开你的博客，然后键盘按F12进入控制台，当然你也可以在浏览器中找找控制台，具体打开方式可以百度，这里不多说。大概长这样：

<img src="yun主题的页面背景透明和左侧菜单栏透明修改\1.png" alt="1"  />

然后我们打开元素面板，如上图最上面菜单栏所示

# 接下来就可以根据这里面的代码定位你要修改的地方

<img src="yun主题的页面背景透明和左侧菜单栏透明修改\2.png" alt="2"  />

如图中高亮区域

接下来一步步细化你所需要修改的区域

<img src="yun主题的页面背景透明和左侧菜单栏透明修改\3.png" alt="3"  />

<img src="yun主题的页面背景透明和左侧菜单栏透明修改\4.png" alt="4"  />

一直到你想要的区域不能再细分为止。我直接贴最终结果了

<img src="yun主题的页面背景透明和左侧菜单栏透明修改\5.png" alt="5"  />

放大结果，得出如下结论

<img src="yun主题的页面背景透明和左侧菜单栏透明修改\6.png" alt="6"  />

在这个post.styl文件中的post-block函数中，以下开始正式修改

----

# 首先是文章页面的透明

打开你的博客目录中的`themes\yun\source\css\_layout`里面的post.styl文件，马上就能找到如下代码并修改：（按照下图修改）

```stylus
.post {
  &-block {
    color: var(--hty-text-color);
    //opacity: 0.4   //文章背景透明度（总的，大bug）一般不用这个，用下面那个（这个是我自己加的）
    margin: 0 1rem;
    padding: 1rem;
    //background-color: var(--post-block-bg-color);   //改这个透明
    background-color: "";//这样就表示透明了，至于透明度，我还没发现怎么改，因为上面那个一改就基本字也是透明的了

    +mobile() {
      margin: 0;
      padding-top: 2.5rem;
    }
  }
```

此时改完保存你可以三连看看本地效果如何。

# 然后是左边菜单栏的修改

重复上述控制台步骤步骤找到你需要的文件，我这里是`themes\yun\source\css\_components\sidebar`中的sidebar.styl，同样，找到下述代码并修改:

```stylus
.sidebar {
  position: fixed;
  overflow-y: auto;
  top: 0;
  bottom: 0;
  left: 0;
  width: 20rem;
  background-color: ''; //左边栏透明
  background-image: ''; //这个是你插入的图片取消，当然也可以不插入图片，在你插入图片的文件中取消而不是在这
//background-image: url($sidebar-bg-image);
  background-size: contain;
  background-repeat: no-repeat;
  background-position: convert($sidebar-bg-position);
  text-align: center;
  z-index: $sidebar-z-index;
  the-transition();
  the-box-shadow();

  +mobile() {
    left: -20rem;
    transform: translateX(0);
  }

```

到目前为止，这里只是亮色主题下的左边菜单栏修改。由于作者大大的骚操作，他把暗色主题在设置时候重写了这个函数，我们需要到暗色主题下修改。我们到

`\themes\yun\source\css\_global`下打开dark.styl。找到如下代码并修改：

```stylus
// sidebar
$sidebar-bg-image = hexo-config('sidebar.dark_bg_image');

.sidebar {
  //background-color: rgba($dark-primary-color, 0.95);   //这里是被重写的结果，亮色改变要在_components中的sidebar中sidebar.styl
  background-image:'';//同样的图片修改

  if ($sidebar-bg-image) {
    background-image: url($sidebar-bg-image);
  } else {
    background-image: none;
  }
}

```

# 然后就是评论板块

打开`themes\yun\source\css\_widget`中的comment.styl,找到并修改如下代码：

```stylus
#comment {
  margin: 0 1rem;
  padding: 1rem;
  //background-color: var(--post-block-bg-color);
  background-color: '';  //评论板块透明
  +mobile() {
    margin: 0;
  }
}

```

# OK,三连看你的修改效果，大功告成

