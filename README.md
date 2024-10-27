# 泉州七中网络安全社官网

欢迎访问：**[https://csc.iteacher.org.cn](https://csc.iteacher.org.cn)**

---

## 站点维护指南

### fork源码仓库并克隆至本地

首先在github上fork[站点源码远程仓库](https://github.com/qzqzcsclub/csclubweb)

然后在你要放置源码的地方打开终端，将你fork来的远程仓库克隆到本地（在这之前请确保你的本地git的用户名、邮箱、密钥和公钥已设置完毕）。

```bash
git clone git@github.com:<你的github地址>/csclubweb.git
```

### 安装Hexo和依赖包

在终端通过npm下载Hexo

```bash
npm install -g hexo-cli
```

在项目根目录的终端下载依赖包

```bash
npm install
```

### 修改文章和页面

在`./source/`中有所有页面和文章的md文件，例如文章“泉州七中网络安全社官网开始建设”的md文件就在`./source/_posts/泉州七中网络安全社官网开始建设.md`。打开相对应的md文件修改内容即可。

### 新建文章

在项目根目录的终端输入

```bash
hexo new "<文章名>"
```

例如：

```bash
hexo new "网安社yyds"
```

然后在相应目录就会自动生成新文章对应的md文件

### 新建页面

```bash
hexo new "<页面名>"
```

例如：

```bash
hexo new "一个不正经的页面"
```

然后在相应目录就会自动生成新页面对应的md文件

### 文章和页面的Front-matter

Front-matter是md文件最上方以 --- 分隔的区域，用于指定个别文件的变量，例如：

```
---
title: Hello World
date: 2023/6/10 00:00:00
---
```

本站点文章正常情况下统一要有的Front-matter：

|Front-matter|解释|
|-|-|
|title|文章标题|
|date|文章创建日期|
|categories|文章分类（只能填“内部通知”、“对外通知”、“教程”|
|description|文章描述|
|tags|教程分类（教程才要设置）|

例如：

```
---
title: 泉州七中网络安全社官网开始建设
categories: 
  - 对外通知
date: 2023-06-10 00:00:00
description: 泉州七中网络安全社官网新版本开始建设
---
```

所有文章的Front-matter：

|Front-matter|解释|
|-|-|
|title|【必需】文章标题|
|date|【必需】文章创建日期|
|categories|【必需】文章分类（只能填“内部通知”、“对外通知”、“教程”）|
|description|【必需】文章描述|
|tags|【必需】教程分类（教程才要设置）|
|top|【可选】文章置顶（填写true或者数字，数字越大越考前）
|updated|【可选】文章更新日期|
|keywords|【可选】文章关键字|
|top_img|【可选】文章顶部图片|
|cover|【可选】文章缩略图(如果没有设置top_img,文章页顶部将显示缩略图，可设为false/图片地址/留空)|
|comments|【可选】显示文章评论模块(默认 true)|
|toc|【可选】显示文章TOC(默认为设置中toc的enable配置)|
|toc_number|【可选】显示toc_number(默认为设置中toc的number配置)|
|toc_style_simple|【可选】显示 toc 简洁模式|
|copyright|【可选】显示文章版权模块(默认为设置中post_copyright的enable配置)|
|copyright_author|【可选】文章版权模块的文章作者|
|copyright_author_href|【可选】文章版权模块的文章作者链接|
|copyright_url|【可选】文章版权模块的文章连结链接|
|copyright_info|【可选】文章版权模块的版权声明文字|
|highlight_shrink|【可选】配置代码框是否展开(true/false)(默认为设置中highlight_shrink的配置)|
|aside|【可选】显示侧边栏 (默认 true)|

本站点页面正常情况下统一要有的Front-matter：

|Front-matter|解释|
|-|-|
|title|文章标题|
|date|文章创建日期|

例如：

```
---
title: 介绍
date: 2023-06-10 00:00:00
---
```

所有页面的Front-matter：

|Front-matter|解释|
|-|-|
|title|【必需】页面标题|
|date|【必需】页面创建日期|
|type|【必需】标籤、分类和友情链接三个页面需要配置|
|updated|【可选】页面更新日期|
|description|【可选】页面描述|
|keywords|【可选】页面关键字|
|comments|【可选】显示页面评论模块(默认 true)|
|top_img|【可选】页面顶部图片|
|aside|【可选】显示侧边栏 (默认 true)|
|highlight_shrink|【可选】配置代码框是否展开(true/false)(默认为设置中highlight_shrink的配置)|

### 通知和教程区分、教程分类说明

本站点使用了非常规的方法来区分通知和教程、分类教程（暂时没找到更好的方案）。通知和教程的区分是使用Hexo提供的分类功能实现的，所以文章分类只能填“内部通知”、“对外通知”、“教程”。教程的分类是使用Hexo提供的标签功能实现的，所以在教程文章的Front-matter中的`tag`中需要填写教程的分类，例如`python`。

### 在本地渲染Hexo源码

因为有一些修改如果不渲染就合并到远程仓库，就会产生一些我们不想看到的结果（比如一篇没在本地的文章每次都会在远程仓库重新渲染一遍，导致每次渲染出来的访问链接都不一样），所以在修改完源码后请先渲染再提交代码。渲染的方式就是在项目根目录的终端输入：

```bash
hexo g
```

### 提交代码至远程仓库

在项目根目录的终端使用git提交修改至你fork来的远程仓库的其他分支（不是main分支就行，这里以patch分支为例）

> 不要提交到main分支是因为如果你提交到了main分支，那么github工作流就会自动在你的仓库运行，虽然这不对我们的站点构成影响，但是这不是一个好的习惯，你也不希望你的提交记录旁边显示一个工作流运行失败的红点对吧。

```bash
git add .
git commit -m"<在这里描述你修改的内容>"
git push origin patch
```

### 提交pr

代码提交到你的远程仓库后，在浏览器打开你的远程仓库，打开patch分支后点击 compare & pull request ，然后选择从你的patch分支合并到原本的仓库的main分支，再描述你的修改并提交就可以了。

### 拉取远程仓库的更改

在你再维护站点可能会遇到一个问题，就是在你提交的代码合并到远程仓库后又有其他人合并了代码，这时候你的仓库的代码就不是最新的了，这个时候就需要你将你的仓库和远程仓库同步，同步方法就是在你的github仓库页面点击Sync fork，然后点击Update sync，如果是显示“This branch is not behind the upstream qzqzcsclub:main”的话就代表你的仓库已经是最新的了，就不用更新了。你的仓库更新到了最新，但是你电脑上的仓库还没有，你需要将你的仓库拉取到你的本地仓库，就是在你项目根目录的终端输入：

```bash
git pull origin main
```

拉取成功后就可以继续维护站点了。

---

## 站点部署方案

现阶段本站点的部署方案是先将项目源码pr或者直接提交到[csclubweb](https://github.com/qzqzcsclub/csclubweb)，然后由Netlify自动对项目进行渲染，并将渲染后的站点源码提交到[https://csc.iteacher.org.cn](https://csc.iteacher.org.cn)。

## 维护要求

高级维护工作需要修改和管理[csclubweb](https://github.com/qzqzcsclub/csclubweb)的直接权限，这个需要找管理社团github的人员获取

需要定期审核[csclubweb](https://github.com/qzqzcsclub/csclubweb)的pr，不然别人的维护工作就白费了。

## GitHub Actions 说明

具体请见[GitHub Actions 中文文档](https://docs.github.com/zh/actions/learn-github-actions/understanding-github-actions)
