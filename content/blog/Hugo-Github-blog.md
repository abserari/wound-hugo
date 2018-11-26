+++
author = "Abser"
categories = ["Hugo"]
date = "2018-11-25"
description = "Use Hugo and Github make a website for blog"
featured = "pic04.jpg"
featuredalt = "Pic 4"
featuredpath = "date"
linktitle = ""
title = "Hugo+Github搭建个人博客"
type = "post"

+++

## 前言介绍

- **Hugo是什么?**

  > **Hugo是一种通用的网站框架。严格来说，Hugo应该被称作静态页面生成引擎。**

  官网https://gohugo.io/

- **静态页面生成引擎又是什么?**

  > **静态页面生成引擎从字面上来理解，就是将你的内容生成静态网站。所谓“静态”的含义其实反映在网站页面的生成的时间。一般的web服务器（WordPress, Ghost, Drupal等等）在收到页面请求时，需要调用数据库生成页面（也就是HTML代码），再返回给用户请求。而静态网站则不需要在收到请求后生成页面，而是在整个网站建立起之前就将所有的页面全部生成完成，页面一经生成便称为静态文件，访问时直接返回现成的静态页面，不需要数据库的参与。**

- **那么我采用Hugo来搭建博客优点有哪些?**

  1. **访问快速.因为不需要每次访问生成页面当然，一旦网站有任何更改，静态网站生成器需要重新生成所有的与更改相关的页面。然后由于Hugo是用Go语言编写的在生成速度这方面做的非常好.5000篇文章的博客生成时间只需要6秒钟.对比其他的静态页面生成引擎动不动几分钟的时间优势非常明显**
  2. **采用静态页面搭建博客,维护起来非常简单.事实上根本不需要什么维护，完全不用考虑复杂的运行时间，依赖和数据库的问题。再有也不用担心安全性的问题，没有数据库，网站注入什么的也无从下手**
  3. **无依赖.低消耗资源.**
  4. **专注于写作.我认为对于个人博客来说，应该将时间花在内容上而不是各种折腾网站。Hugo会将Markdown格式的内容和设置好模版一起，生成漂亮干净的页面。你只需要把Markdown文件放在content文件夹下面.一切水到渠成**

- **听起来很棒的样子那搭建起来会不会非常复杂?**

  **不会.跟着教程走下来.只需要十分钟.**



# 开始



# 需求

```toml
1.Hugo工具
2.GitHub个人账号
3.Git工具
```

# 安装

如果说速度快是Hugo的第一大优点，那么安装简单应该就是Hugo的第二大优点。对于Mac用户，没有brew的话先安装brew，在命令行里敲：

```
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

然后再敲一行安装Hugo:

```
$ brew new Hugo
```

当然你也可以在[这里](https://github.com/spf13/hugo/releases)直接下载对应系统的binary文件，解压就行了。

#  生成 site 目录

```bash
hugo new site blog
cd blog
git init
#Congratulations! Your new Hugo site is created in /Users/steven/MyProjects/Demo/blog.

#Just a few more steps and you're ready to go:
#
#1. Download a theme into the same-named folder.
#   Choose a theme from https://themes.gohugo.io/, or
#   create your own with the "hugo new theme <THEMENAME>" command.
#2. Perhaps you want to add some content. You can add single files
#   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
#3. Start the built-in live server via "hugo server".
#
#Visit https://gohugo.io/ for quickstart guide and full documentation.


```

`config.toml` 是配置文件，在里面可以定义博客地址、构建配置、标题、导航栏等等。

`themes` 是主题目录，可以去 [themes.gohugo.io](http://themes.gohugo.io/) 下载喜欢的主题。

`content` 是博客文章的目录。

### 安装主题

```
mkdir themes
cd themes
git clone https://github.com/jpescador/hugo-future-imperfect.git
```

*安装的主题在这里 themes/hugo-future-imperfect* 

### exampleSite

主题目录下有一个示例网站文件夹，直接把文件夹内容全部复制到blog目录下覆盖替换即可

The structure of the folder will look like this:

```sql
exampleSite
├── config.toml
├── staticman.yml
├── content
|   ├── about
|   |   └── _index.md
|   ├── blog
|   │   ├── creating-a-new-theme.md
|   │   ├── goisforlovers.md
|   │   ├── hugoisforlovers.md
|   │   └── migrate-from-jekyll.md
|   ├── contact
|   │   └── _index.md
|   └── itemized
|       ├── item1.md
|       ├── item2.md
|       ├── item3.md
|       └── item4.md
├── data
│   └── comments
│       └── .gitkeep
└── static
    ├── css
    │   └── add-on.css
    ├── img
    |   ├── 2014
    |   |   ├── 04
    |   |   |   ├── pic02.jpg
    |   |   |   └── pic03.jpg
    |   |   └── 09
    |   |       └── pic01.jpg
    |   └── main
    |       └── logo.jpg
    └── js
        └── add-on.js
```

这几个文件的作用分别是：

- archetypes：包括内容类型，在创建新内容时自动生成内容的配置
- content：包括网站内容，全部使用markdown格式
- layouts：包括了网站的模版，决定内容如何呈现
- static：包括了css, js, fonts, media等，决定网站的外观
- config.toml: 包括主题生成网站的时候的配置

### 预览

执行命令，使用 Hugo 生成静态内容并在启动本地 HTTP Server。然后即可访问 [http://localhost](http://localhost/):1313/ 查看效果。

```bash
hugo server -t
#...
#Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
```

# 用Github Pages作为网站的Host



（注意，以下的<>包括的内容都是需要自行替换的)

Github pages分为两种：一种是项目主页，每个项目都可以有一个；另一种是用户主页，一个用户只能有一个。

因为用户主页只能有一个，所以建议使用项目主页托管，不过我这里采用了用户主页，反正我也只用一个博客，使用个人主页作为Host也相对更简单一点。

我们需要创建两个单独的repo，一个用于放Hugo的输入文件，即除了`public/`文件夹之外的所有文件，另一个放我们生成的静态网站，也就是`public/`的内容。

步骤如下：

1. 在Github上创建repo `<your-project>-hugo`，托管Hugo的输入文件。
2. 创建repo `<username>.github.io`，用于托管`public/`文件夹，注意这里的repo名字一定要用自己的用户名，才会被当作是个人主页。
3. clone your-project

```
$ git clone <<your-project>-hugo-url>
```

1. 进入your-project 目录

```
$ cd <your-project>-hugo
```

1. 删掉public目录（这个目录每次运行Hugo都会再次生成，不用担心）

```
$ rm -rf public
```

1. 把public/目录添加为submodule 与.github.io同步

```
$ git submodule add git@github.com:<username>/<username>.github.io.git public
```

1. 添加.gitignore文件，文件中写`public/`，在同步`<your-project>-hugo`时会忽略public文件夹
2. 下面是写好的一个script `deploy.sh`，拷贝过去直接就能用，记得chmod +x deploy.sh加上运行权限。

```bash
#!/bin/bash
echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi

# Push Hugo content 
git add -A
git commit -m "$msg"
git push origin master


# Build the project. 
hugo # if using a theme, replace by `hugo -t <yourtheme>`

# Go To Public folder
cd public
# Add changes to git.
git add -A

# Commit changes.

git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back
cd ..
```

等一小会儿（10分钟左右），你就能在<http://username.github.io/> 这个页面看到你的网站了！每次更新网站或者写了新文章，只需要运行./deploy.sh 发布就搞定了，简单吧？

Github pages还支持域名绑定，三个步骤：

1. 在`<username>.github.io` repo的跟目录下添加`CNAME`文件，文件里写上你的域名，不用加http://的开头。
2. 记下<http://username.github.io/> 的ip地址。

```
$ ping username.github.io
```

1. 在你的域名管理中加上两条A记录，分别是www和@，记录指向<http://username.github.io/> 的ip地址，也需要等一小会儿生效。

#  