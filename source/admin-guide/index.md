---
title: 网站维护指南
date: 2023-06-10 00:00:00
---

# 站点介绍

本站点为纯静态站点，由[Hexo框架](https://hexo.io/zh-cn/)和[Butterfly主题](https://butterfly.js.org/)搭建，部署于[GitHub Page](https://pages.github.com/)。

> 也有部署至服务器的方案，但是因为社团现阶段没有服务器所以使用免费方案。

# 网站维护工作

- 初级：文章（通知、教程）、页面撰写
- 中级：功能维护、站点美化
- 高级：网站部署

> 级别高的维护工作包括级别低的内容。同时级别高的工作需要题会低级别要求掌握的内容。

# 网站分级维护指南

## 初级

### 需要先掌握的东西

1. 终端的使用
2. git的下载和使用，有github账号
3. npm和nodejs的下载和使用
4. 能够访问github
5. Markdown语法

> 以上内容请自行上网学习

### 拉取站点源码至本地

首先获得[站点源码远程仓库](https://github.com/qzqzcsclub/csclubweb)的访问和提交代码的权限，这个需要找管理社团github账号的人员。

然后在你要放置源码的地方打开终端，将[远程仓库](https://github.com/qzqzcsclub/csclubweb)克隆到本地（在这之前请确保你的本地git的用户名、邮箱、密钥和公钥已设置完毕）。

```bash
git clone git@github.com:qzqzcsclub/csclubweb.git
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

### 新建文章和页面

#### 新建文章

在项目根目录的终端输入

```bash
hexo new "<文章名>"
```

例如：

```bash
hexo new "网安社yyds"
```

然后在相应目录就会自动生成新文章对应的md文件

#### 新建页面

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

```
|Front-matter|解释|
|-|-|
|title|【必需】文章标题|
|date|【必需】文章创建日期|
|categories|【必需】文章分类（只能填“内部通知”、“对外通知”、“教程”|
|description|【必需】文章描述|
|tags|【必需】教程分类（教程才要设置）|
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
```

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

### 提交修改至远程仓库并实现站点自动部署

在项目根目录的终端使用git提交修改至远程仓库

```bash
git add .
git commit -m"<在这里描述你修改的内容>"
git push origin main
```

代码提交成功后，远程仓库的GitHub Actions就会自动部署站点，可以在 https://github.com/qzqzcsclub/csclubweb/actions 看到正在运行的工作流，状态显示橙色就是工作流正在运行，绿色就是成功，红色就是失败。一般绿色就是部署成功了，不过具体还得点进工作流查看具体日志。如果部署失败了就需要查看具体日志排查错误，实在不行就求助高级网站维护人员。

## 中级

功能维护和站点优化要求基本掌握Hexo和Butterfly的使用方法。具体内容请查看相应文档进行学习：

Hexo: https://hexo.io/zh-cn/docs/

Butterfly: https://butterfly.js.org/

## 高级

### 现阶段站点部署方案

现阶段本站点的部署方案是先将项目源码提交到[csclubweb](https://github.com/qzqzcsclub/csclubweb)，然后由工作流自动对项目进行渲染，并将渲染后的站点源码提交到已开启GitHub Page的[qzcsclub.github.io](https://github.com/qzcsclub/qzcsclub.github.io),提交后站点就会被GitHub Page自动上传到 https://qzcsclub.github.io/ 。

### 其他站点部署方案

还有将站点同时部署到服务器的方案，该方案的代码已经在`./.github/workflows/autodeploy.yml`和`./.github/workflows/handdeploy.yml`实现，具体请见这两个文件的代码注释。

### GitHub Actions 说明

具体请见[GitHub Actions 中文文档](https://docs.github.com/zh/actions/learn-github-actions/understanding-github-actions)

# 留言

该站点应该在每一届都要安排相应的不同级别的维护人员，高级维护人员至少要有一个，初级和中级的维护人员数量按实际情况决定。站点维护人员应该定期维护网站（修改页面至最新，发布文章等）。