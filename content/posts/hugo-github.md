---
title: "hugo和github搭建静态博客"
date: 2021-08-25T16:40:11+08:00
draft: false 
---


## 用hugo和github搭建静态博客

### 前言
想搭建一个简单的博客，主要用来渲染md静态文档，上网搜了一下，发现很多网友用hugo、github pages来搭建，于是自己搜了一些相关博客，尝试搭建成功，就记录一下搭建步骤。

### 安装hugo

用的是mac操作系统，直接在命令行中输入命令安装：
``` bash
brew install hugo
```

安装成功后，习惯运行hugo -v 命令，如果有输出，说明安装成功

### 生成站点
选择一个路径，比如 `/path/to/myblog`, 使用hugo快速生成站点:
```bash
hugo new site /path/to/myblog
```
这样就在路径`path/to/myblog`的目录生成了一下文件：
```
├── archetypes
│   └── default.md
├── config.toml
├── content
├── data
├── layouts
├── static
└── themes
```

简单介绍一下常用目录功能
| 子目录名称 | 功能 |
| :------------ | :---------------------------------------------------------------------- |
| archetypes | 新文章默认模板 |
| config.toml | Hugo配置文档 |
| content | 存放所有Markdown格式的文章 |
| layouts | 存放自定义的view，可为空 |
| static | 存放图像、CNAME、css、js等资源，发布后该目录下所有资源将处于网页根目录 |
| themes | 存放下载的主题 |

然后我们在content目录下生成hello world文章：
```bash
hugo new posts/hello-world
```
此命令在会自动`content/posts`目录生成一个篇名为hello-world.md文章，文章内容为：
```bash
---
title: "Hello World"
date: 2021-08-25T18:37:57+08:00
draft: true
---
```
draft为true表示这是篇草稿文章，真正发布的时候，要设置为false，或者直接删除。
### 添加主题
给站点添加主题，主要是渲染页面的格式，分两个步骤

第一步：
下载一个主题到themes文件夹
```bash
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```
第二步：
把主题添加到config.toml中
```bash
echo 'theme = "ananke"' >> config.toml
```
然后启动服务：
```bash
hugo server
```
在浏览器中输入网址http://localhost:1313/就可以在浏览器中查看网页效果了：
todo 插入图片
### 发布并托管到github
本文介绍受用/docs发布到master，还有使用/public发布的方法，请自行搜索。

具体步骤如下

步骤1：
我们需要在github创建一个repository，命名为：username.github.io，username替换成你的github用户名

初始化本地文档根目录的git：
```bash
git init
git add .
git commit -m "first commit"
git remote add origin https://github.com/username/username.github.io.git
git push -u origin master
```

步骤2：
在config.toml添加一行配置：
``` bash
publishDir = "docs"
```
这样，运行hugo命令以后，生成的网页文件都会保存到/docs子目录下
```bash
hugo
```

步骤3：
进入刚创建username.github.io的repository的settings标签菜单，在github pages选项的sources选择master branch /docs，点击保存,
然后提交 /docs目录下所有的文件
```bash
git add docs
git commit -m "提交docs静态网易文件"
git push
```

步骤4：
在网页中输入:https://username.github.io就能访问你所有的文章了

todo 添加图片









