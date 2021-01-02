---
title: "使用Hugo和GitHub搭建免费静态Blog"
date: 2021-01-01T21:53:35+08:00
summary: "搭建一个属于自己的Blog，快来行动吧！"
tag: "website"
---
2021年的第一天，在xdm的帮助下完成了静态blog的搭建。话不多说，教程奉上。

### 安装Hugo

首先介绍一下Hugo，Hugo是由Go语言实现的静态网站生成器。简单、易用、高效、易扩展、快速部署。

搭建静态blog的第一步就是在本地安装Hugo，安装流程请移步[官方文档](https://gohugo.io/getting-started/installing/)。安装过程中如遇需要使用Homebrew及Linuxbrew镜像，请移步[镜像使用帮助](https://mirrors.tuna.tsinghua.edu.cn/help/homebrew/)。

安装完成使用 `hugo version` 命令来检查是否安装成功。

### 生成站点

使用Hugo快速生成站点，比如希望生成到`/workspace/website/path`路径:

``` $ hugo new site /workspace/website/path ```

这样就在/workspace/website/path下生成了站点。
