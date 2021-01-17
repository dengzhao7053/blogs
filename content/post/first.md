---
truncated: true
title: "使用Hugo和GitHub搭建免费静态Blog"
date: 2020-01-01T21:53:35+08:00
categories: ["website"]
tags: ["hugo","website"]
series: ["Go Web Dev"]
---

"搭建一个属于自己的Blog，快来行动吧！"
<!--more-->

2021年的第一天，在xdm的帮助下完成了静态blog的搭建。话不多说，教程奉上。

### 安装Hugo

首先介绍一下Hugo，Hugo是由Go语言实现的静态网站生成器。简单、易用、高效、易扩展、快速部署。

搭建静态blog的第一步就是在本地安装Hugo，安装流程请移步[官方文档](https://gohugo.io/getting-started/installing/)。安装过程中如遇需要使用Homebrew及Linuxbrew镜像，请移步[镜像使用帮助](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)。

安装完成使用 `hugo version` 命令来检查是否安装成功。

### 生成站点

使用Hugo快速生成站点，比如希望生成到`/workspace/website/path`路径:

``` $ hugo new site /workspace/website/path ```

这样就在/workspace/website/path下生成了站点。

### 创建文章
创建一个`about`页面：

``` $ hugo new about.md```

`about.md`自动生成在`content/about.md`。内容如下：

```
---
title: "About"
date: 2021-01-01T21:49:06+08:00
---
正文内容
```

内容是`Markdown`格式，`---`之间的内容是YAML格式，根据你的喜好可以换成TOML格式（使用`++++`标记）或者`JSON`格式。

创建第一篇文章，放到`post`目录下，方便之后生成聚合页面。

``` $ hugo new post/first.md```

使用编辑器打开`post/first.md`，即可编辑内容。

### 安装皮肤

到[皮肤列表](https://themes.gohugo.io/)挑选一个心仪的皮肤，找到相关的`GitHub`地址，在站点根目录下创建`themes`目录，在`themes`中把皮肤`git clone`下来，这里以Hyde皮肤为例：

```
$ mkdir themes
$ cd themes
$ git clone https://github.com/spf13/hyde.git
```

### 运行Hugo

在你的站点根目录执行`Hugo`命令行进行调试：

``` $ hugo server --theme=hyde --buildDrafts```

在浏览器中打开：`http://localhost:1313`，即可浏览效果。

### 部署到GitHub Pages

部署到`GitHub Pages`也比较简单。大致可分为以下几步：

1. `GitHub`上创建仓库
2. 站点根目录执行`hugo`命令生成最终页面
3. 使用`git init`将站点初始化为一个`git`仓库
4. 修改`config`文件
5. 将本地代码`push`到刚创建的仓库的`master`分支
6. 指定`GitHub`上仓库`github pages`设置项的source
7. 浏览器里访问

因为有不同的部署方式，所以不仔细展开。具体流程请参考[github部署官方文档](https://gohugo.io/hosting-and-deployment/hosting-on-github/)。

到此，一个简单的静态站点就搭建完毕了。