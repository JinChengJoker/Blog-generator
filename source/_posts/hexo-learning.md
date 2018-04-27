---
title: GitHub Pages + Hexo 搭建博客
date: 2017-06-20 16:23:01
---
很久之前就准备自己搞一个博客，当时准备直接在博客网站上注册一个，但是总觉得不酷。后来发现了GitHub Pages，可以用Hexo在上面部署一个博客，于是几经折腾，终于搞出来了。

## Hexo 介绍

Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

- 速度超快
- 支持 Markdown
- 一键部署
- 丰富的插件

## 安装必要程序

[Git](https://git-scm.com/download/win) - 在官网下载安装包安装
[Node.js](https://nodejs.org) - 在官网下载安装包安装

验证安装成功：

```
$ node -v
```

## 创建 Github 仓库

由于需要部署到 Github，所以先在 Github 创建一个仓库，这个仓库用来存放 hexo 为我们生成的静态文件。这个仓库名需要与自己的 Github 账户名一致，比如我的账户名是 JinChengJoker，那么则需要创建一个名为 JinChengJoker.github.io 的仓库。
同时考虑到后面时间长了，可能会存在更换电脑的情况，所以再创建一个仓库 Hexo，这个仓库用来存放 hexo 的原始文件，便于管理。遇到更换电脑的情况，只需要克隆这个仓库到新电脑，npm install 之后就可以继续更新博客了。
ps：其实也可以[用 git 分支的方法实现](https://www.zhihu.com/question/21193762)，原理相同，但是我觉两个仓库更加清晰一些，所以采用此方法。

## 克隆 Github 仓库

我们只需要克隆 Hexo 仓库到本地，另一个仓库不需要管，后面 Hexo 会自动部署。

```
$ git clone git@github.com:JinChengJoker/Hexo.git
```

## Hexo 快速搭建博客

用 npm（随同Node.js一起安装的包管理工具）安装 Hexo。

```
$ cd Hexo
$ npm install -g hexo-cli
$ hexo init
$ npm install
```

生成静态页面：

```
$ hexo g
```

启动服务器：

```
$ hexo s
```

在浏览器访问 http://localhost:4000/ 就可以看到博客已经基本搭建完成。

新建一篇文章：

```
$ hexo new test
```

在 `source/_posts` 下会生成一个 test.md 的文件，在这个文件里写文章，写完之后保存。

```
$ hexo clean    // 清除缓存文件 (db.json) 和已生成的静态文件夹 (public)。
$ hexo g
$ hexo s
```

重新访问 http://localhost:4000/ ，就可以看到刚才新建的文章。

## 部署到 Github

安装 hexo-deployer-git，它会帮我们把博客部署到Github。

```
$ npm install hexo-deployer-git --save
```

修改 `_config.yml` 配置文件中的 deploy：

```
deploy:
  type: git
  repo: <repository url>
  branch: [branch]
```

repo 为之前创建的跟账户名相同的 Github 仓库地址，branch 为 master。配置完成之后保存。

自动部署：

```
$ hexo d
```

在浏览器访问 https://jinchengjoker.github.io/ ，就可以看到博客基本已经部署成功了。
