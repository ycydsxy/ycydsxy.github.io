---
title: 一份超详细的Hexo+NexT个人博客建站指南
date: 2021-03-17 16:08:37
tags: 
- 博客 
- Hexo
- NexT
categories: 教程
---

最近业务上节奏稍稍稍微放缓了一些，有了一些 ~~摸鱼~~ 学习的时间，俗话说的好：“饱暖思学习”，我也趁此机会进行了一次博客建站的尝试，并把整个的过程和其中的一些思考记录下来

这篇文章想尽量写的傻瓜式，即任何一个正常人看了本文都能够快速、完美地复制一遍，在最短的时间里搭建一个和[本站](https://ycydsxy.github.io)类似的博客站点；同时，我也会尽量对其中的一些步骤给出我的理解和解释，不正确的地方也请大家评论指正

{% asset_img example1.gif%}

<!-- more -->

# 写在前面

## 最终效果

最终你会得到一个个人博客站点（效果如上面动图所示），功能包括但不限于：

* 简约、美观的博客外观
* 支持标签、分类、归档、目录
* 支持内容全文搜索
* 支持在文章底部评论
* 支持阅读数量实时统计
* 全球可访问的域名
* 文章自动发布和更新

## Hexo 是什么 / 为什么要使用 Hexo

写博客（或者日记）是本质上是为了记录自己的生活和思考，并分享给别人。写博客的方式有很多种，其中比较常见的有：

* 在报纸或者书刊上发表文章（如 ~~意林~~、新青年、季羡林日记 等）
* 在公共互联网站点上发表文章（如 [古天乐博客](http://blog.sina.com.cn/louiskoo2008)、[码农桃花源](https://www.cnblogs.com/qcrao-2018)、微信公众号 等）
* 自己建设互联网站点发表文章（如 [wangyin](http://www.yinwang.org/) 、[draveness](https://draveness.me/)、[ouchangkun ](https://blog.changkun.de/)等）

其中，前两种可以理解为「打工人」模式，即用户输出内容发布到外部平台上，其优点是门槛较低、可专注于内容写作、平台自带功能（搜索、评论、点赞等），缺点是受制于平台、没有太多自定义的能力；后一种可以理解为「老板」模式，即用户自行负责平台和内容，优点是完全灵活、可以全部自定义、拥有“造世”的权力，缺点是门槛较高、需要自行搭建站点、需要做较多的和内容写作无关的工作

我们能否同时享受「老板」模式下的**自由**和「打工人」模式下的**轻松**呢？这是一个 ~~偷懒~~ 智慧的人显而易见会思考的事情，我理解 Hexo 就是为了解决这个问题而生的

[Hexo](https://hexo.io/zh-cn/) 是“一个快速、简洁且高效的博客框架”（官方说法），可以理解为一个站点生成器或者一个[脚手架](https://stackoverflow.com/questions/235018/what-is-scaffolding-is-it-a-term-for-a-particular-platform)，你只需要按照它的规则去写文章就好了，完全不用操心站点的事情，它会根据你写的文章去生成一个博客站点。

> Hexo 生成的站点其实是全静态（html + js + css）的页面，对于博客这种只需要展示内容、没有业务逻辑的场景是非常合适的，而且静态页面的部署也非常简单和轻量。当然，没有后端也就意味着有些动态功能（如评论等）很难实现，目前常见的做法是利用各种扩展插件去访问第三方服务的 API 

所以，使用 Hexo 后我们可以方便的拥有自己的博客站点，同时只用关注内容写作本身。另外，它提供了很多配置项来最大化站点的自由度，以确保大家在其规则下可以充分自定义自己的博客站点，使得大家的站点不是千篇一律的（否则费这老劲干嘛呢...）

## NexT 是什么 / 为什么要使用 NexT

Hexo 给了我们很多自由度，其中最重要的一部分就是[主题](https://hexo.io/themes/)，也就是你站点的外观和风格。在 Hexo 的设计中，内容和外观是分离的，所以可以比较方便的在不改内容的条件下改变站点的外观，也就是“换皮”。当然，你也可以使用默认的外观，但那必然是非常丑的，具体有多丑我们在下文中会提到

Hexo 的主题数量目前已经有 300+ 了，[NexT](https://theme-next.js.org/) 是众多 Hexo 主题中的比较优秀的一个，也是本人比较喜欢的一个，原因大致有三点：

1. 外观简约而不简单，好看但不喧宾夺主，让人阅读时能更关注内容
2. 在 ~~全球最大同性交友网站~~ GitHub 上的 star 数很非常高，属于绝对头部的主题之一，拥有良好的社区基础
3. 原作者是国人，有比较完善的中文支持和中文使用文档

>  NexT 社区官网和仓库目前有多个版本（有些还挂了...），也挺迷的，这里我找到了官方的一些[解释](https://theme-next.js.org/docs/getting-started/upgrade.html#NexT-Repositories)

当然，如果你不喜欢这个主题，也可以很方便地切换到其他主题上，知乎上总结过一些比较优秀的主题：[有哪些好看的 Hexo 主题？](https://www.zhihu.com/question/24422335)

# 建站指南

废话不多说了，我们赶紧开始实战和演示环节，演示用操作系统为 `Debian GNU/Linux 10`（ `mac`、`windows` 下方法相似，只是部分基础命令有差异）

在以下每一个步骤中，我会先给出一些需要用到的基本工具，工具的下载、安装、使用方法均不在本文的讨论范围内

## Hexo 建站

> 前置条件为已经安装 [Git](https://git-scm.com/) 和 [Node.js](https://nodejs.org/en/)

在本小节里，我会演示从「一无所有」到拥有一个「样例小站」的全过程

### 安装 Hexo

``` plain
root@hexo_test:~# npm install -g hexo-cli

changed 65 packages, and audited 66 packages in 6s

11 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

### 初始化博客源码

```plain
root@hexo_test:~# hexo init blog_test
INFO  Cloning hexo-starter https://github.com/hexojs/hexo-starter.git
INFO  Install dependencies
INFO  Start blogging with Hexo!
```

至此，Hexo 自动帮你建了一个存放博客的文件夹，在其中生成了五脏俱全的源代码，并且附赠一篇 Hello World 的样例文章

所谓源码，也就是 Hexo 规则下的一些路径和文件，其含义可以看[这里](https://hexo.io/docs/setup)。对于初级建站来说，比较重要的是其配置文件 `_config.yml` ，里面包含了 Hexo 的各种基础配置，本文中不会全部涉及，想了解更多可以看[这里](https://hexo.io/docs/configuration)；对于写博客而言，比较重要的是  `source` 路径，这是你将来所有文章的存放的地方，此时这个路径下只有刚才提到的 Hello World 文件（路径为 `source/_posts/hello-world.md`）

Hexo 默认你会使用 [Markdown](https://guides.github.com/features/mastering-markdown/) 语法进行写作，其后缀名为 `.md`，当然 Hexo 也支持其他的语法（比如 ejs、~~word~~、~~powerpoint~~），但需要安装对应的渲染组件

### 生成站点文件

> 本步骤及之后的步骤，若无特殊说明，当前路径均为 `~/blog_test`

```plain
root@hexo_test:~/blog_test# hexo generate
INFO  Validating config
INFO  Start processing
INFO  Files loaded in 165 ms
(node:1439) Warning: Accessing non-existent property 'lineno' of module exports inside circular dependency
(Use `node --trace-warnings ...` to show where the warning was created)
(node:1439) Warning: Accessing non-existent property 'column' of module exports inside circular dependency
(node:1439) Warning: Accessing non-existent property 'filename' of module exports inside circular dependency
(node:1439) Warning: Accessing non-existent property 'lineno' of module exports inside circular dependency
(node:1439) Warning: Accessing non-existent property 'column' of module exports inside circular dependency
(node:1439) Warning: Accessing non-existent property 'filename' of module exports inside circular dependency
INFO  Generated: archives/index.html
INFO  Generated: archives/2021/03/index.html
INFO  Generated: archives/2021/index.html
INFO  Generated: index.html
INFO  Generated: fancybox/jquery.fancybox.min.css
INFO  Generated: js/script.js
INFO  Generated: css/style.css
INFO  Generated: css/fonts/fontawesome-webfont.woff
INFO  Generated: css/fonts/fontawesome-webfont.woff2
INFO  Generated: css/fonts/FontAwesome.otf
INFO  Generated: css/fonts/fontawesome-webfont.eot
INFO  Generated: js/jquery-3.4.1.min.js
INFO  Generated: fancybox/jquery.fancybox.min.js
INFO  Generated: css/fonts/fontawesome-webfont.ttf
INFO  Generated: 2021/03/18/hello-world/index.html
INFO  Generated: css/images/banner.jpg
INFO  Generated: css/fonts/fontawesome-webfont.svg
INFO  17 files generated in 450 ms
```

`hexo generate` 用于将源码和文章“编译”成站点文件，生成的产物默认会放在 `public` 路径下，也就是说该路径下的内容已经是一个可以部署的站点了

> 生成产物只是用于部署，使用版本管理工具时可以将其忽略，以 git 为例，推荐将 `public` 路径整体加入 `.gitignore` 文件；另外，在生成有问题时可以尝试运行 `hexo clean` 命令后重新生成

### 本地部署和调试

Hexo 自带了一个简易的服务器，我们将刚才生成的产物部署到本地服务器上，进行查看和调试，运行 `hexo server` 命令

```plain
root@hexo_test:~/blog_test# hexo server
INFO  Validating config
INFO  Start processing
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```

在浏览器访问 [http://localhost:4000](http://localhost:4000) ，你就可以看到这个最原始的博客站点了（丑哭了...）

{% asset_img hexo_1.png%}

## 使用 NexT 主题

> 前置条件为已经安装 Hexo 及相关依赖

在本小节里，我会演示如何使用 NexT 主题来达到博客站点的“换皮”效果，简单来说，就是在 Hexo 中安装你喜欢的主题，并更改 Hexo 配置启用它

Hexo 的主题路径是 `themes` ，对于大多数主题来说，安装就是将主题文件下载到该路径的操作，以另外一个我比较喜欢的主题 yilia 为例，安装好的主题文件会在 `themes/yilia` 路径下。主题的默认配置文件一般会和主题文件在一起，如 yilia 主题的配置文件路径为 `themes/yilia/_config.yml`（文件名和 Hexo 配置文件文件名完全相同，所以多数教程里会提到需要区分 **Hexo 配置文件** 和 **主题配置文件**）

NexT 主题的 v8 版本提供了包安装的方式，其使用方法和文件组织结构和上面提到的普通方式有一定的不同，下面会详细介绍

### 安装 NexT

使用 `npm install hexo-theme-next` 命令拉包即可完成安装，这种方式会更加简洁方便，主题文件会在 `node_modules/hexo-theme-next` 路径下

```plain
root@hexo_test:~/blog_test# npm install hexo-theme-next

added 6 packages, and audited 187 packages in 3s

15 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

NexT 主题默认配置文件的路径为 `node_modules/hexo-theme-next/_config.yml`。Hexo 对于主题配置文件的读取有一套自己的[优先级](https://hexo.io/docs/configuration#Alternate-Theme-Config)，为了方便之后自定义主题配置，我们需要将配置文件从包内拷贝出来并重命名为 `_config.next.yml`：

```plain
root@hexo_test:~/blog_test# cp node_modules/hexo-theme-next/_config.yml _config.next.yml
```

###  替换默认主题

我们可以更改 Hexo 配置文件 `_config.yml` 中的 `theme` 配置项来使用不同的主题，这里将 `theme` 配置项更改为 `next` ：

```yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
```

### 查看效果

查看效果时需要按之前的[生成站点文件](#生成站点文件)和[本地部署调试](#本地部署和调试)步骤重新来一遍，最终效果如下：

{% asset_img next_1.png%}

> 和 Word 这种“所见即所得”的编辑工具不同，所有需要查看效果的地方均需要重新将生成和部署站点才能看到最新的效果（如果你使用过 Latex，你应该有所体会），下文中不再赘述，快速生成和部署可以使用 `hexo g && hexo s` 命令

## 自定义博客站点

> 前置条件为已经安装 Hexo、NexT 及相关依赖

上面我们已经生成了一个初始的博客站点，接下来就是自定义的过程了，这里我们先通过修改一些简单的配置来自定义部分内容。从本节开始，`Hexo 配置文件` 特指 `_config.yml`，`NexT 配置文件` 特指 `_config.next.yml`

### 基本信息配置

修改 ` Hexo 配置文件` 设置基本信息，如站点的标题、描述、关键字、作者、语言、时区、站点地址等，其他的配置项本文不一一列举了，配置项基本能够“望文生义”，有不清楚的地方可以参考[官方文档](https://hexo.io/docs/configuration)

```yaml
# Site	
title: Hexo	# 标题
subtitle: ''	# 子标题
description: ''	# 一句话描述
keywords:	# 关键字
author: John Doe # 作者	
language: en # 语言，中文为 zh-CN
timezone: ''	# 时区，中国为 Asia/Shanghai
# URL	
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'	
url: http://example.com # 站点地址
```

> 站点地址 是指你之后需要将此站点发布到互联网上的 URL，如果你已经有相应 URL 则可以直接替换，如果没有可以先不管，在后面的[发布博客站点](#发布博客站点)小节会让你拥有一个免费的站点地址

修改  `NexT 配置文件` 设置网站风格、头像等，其他的配置项本文不一一列举了，配置项上面都有详细的注释，有不清楚的地方可以参考[官方文档](https://theme-next.js.org/docs/theme-settings/)

```yaml
# ---------------------------------------------------------------	
# Scheme Settings	
# ---------------------------------------------------------------	
# Schemes	# 下面是四种不同的风格，可以按需打开相应的注释：Muse、Mist、Pisces、Gemini
scheme: Muse	
#scheme: Mist	
#scheme: Pisces	
#scheme: Gemini	
# Dark Mode
darkmode: false

# Sidebar Avatar # 下面是头像的配置
avatar:	
  # Replace the default image and set the url here.	
  url: #/images/avatar.gif	# 头像的路径，这个例子里你的头像文件应该放置在 source/images/avatar.gif
  # If true, the avatar will be dispalyed in circle.	
  rounded: false # 是否裁剪成圆形
  # If true, the avatar will be rotated with the cursor.	
  rotated: false # 是否在鼠标悬停时展示头像旋转动画
```

{% asset_img settings_1.png 四种不同的 NexT 风格%}

### 首页 / 标签 / 分类 / 归档配置

对一个博客站点来说，首页（home）、标签（tags）、分类（categories）和归档（archives）都是很常用和必要的功能：

* 首页：能够按时间顺序展示最近几篇文章的摘要，而非整篇文章
* 标签：为每篇文章打一个或多个 Tag，可以展示某 Tag 下的所有文章
* 分类：为每篇文章分类，将所有文章组织起来，可以展示某类别下的所有文章
* 归档：按时间线罗列出所有的文章

{% asset_img settings_2.png%}

修改  `NexT 配置文件`  ，将菜单栏里的 home、tags、categories、archives 注释打开，就可以在菜单里看到相应入口了

```yaml
# External url should start with http:// or https://	
menu: # 菜单栏
  home: / || fa fa-home	
  #about: /about/ || fa fa-user	
  tags: /tags/ || fa fa-tags	
  categories: /categories/ || fa fa-th	
  archives: /archives/ || fa fa-archive	
  #schedule: /schedule/ || fa fa-calendar	
  #sitemap: /sitemap.xml || fa fa-sitemap	
  #commonweal: /404/ || fa fa-heartbeat
```

归档功能是直接就能使用的，不需要额外其他配置和动作

首页功能需要提取文章的前面部分形成短小精悍的摘要，这里的方式有手动指定、自动截取等。Hexo 和 NexT 建议使用手动指定的方式，即在文章中插入 `<!-- more -->` 标记来手动切割，该标记前面的文字会形成摘要

标签和分类功能的完善需要额外的步骤，这里用标签功能进行演示。首先先创建相应的 `page`，直接使运行 `hexo new page tags` 命令：

``` plain
root@hexo_test:~/blog_test# hexo new page tags
INFO  Validating config
INFO  ==================================
  ███╗   ██╗███████╗██╗  ██╗████████╗
  ████╗  ██║██╔════╝╚██╗██╔╝╚══██╔══╝
  ██╔██╗ ██║█████╗   ╚███╔╝    ██║
  ██║╚██╗██║██╔══╝   ██╔██╗    ██║
  ██║ ╚████║███████╗██╔╝ ██╗   ██║
  ╚═╝  ╚═══╝╚══════╝╚═╝  ╚═╝   ╚═╝
========================================
NexT version 8.2.2
Documentation: https://theme-next.js.org
========================================
INFO  Created: ~/blog_test/source/tags/index.md
```

其次，更改刚生成的 `page` 的 `type` 属性，需要编辑 `source/tags/index.md` 文件，指定 `type` 为 `tags`：

``` markdown
---
title: tags
date: 2021-03-19 08:24:03
type: tags
---
```

> 分类的创建和更改流程和标签几乎一样，只需要把所有地方的 `tags` 替换成 `categories` 即可

另外，我们需要在每篇文章的[元信息](https://hexo.io/docs/front-matter)中指定该文章对应的标签和类别，以上面提到的 Hello World 文章为例，编辑 `source/_posts/hello-world.md` ，加入相应的标签和分类信息：

``` markdown
---
title: Hello World
tag: 
- hello
- world
categories: test
---
```

查看效果，已经可以看到有 hello 和 world 两个标签了：

{% asset_img settings_3.png%}

## 发布博客站点

之前我们都是在本地进行站点的部署和调试，这一节我们会把站点发布到互联网上，以供其他读者来访问和浏览。和本地部署过程类似，我们首先要进行站点的生成，然后需要将生成产物打包上传到服务器上。如果你不关心发布和部署的细节，你可以直接跳过这一节

### 站点文件的管理

在当前路径下主要有两类文件：一类是“源码”，也就是非 Hexo 生成的文件；一种是“产物”，也就是源码经过 Hexo 生成的产物（`public` 路径下的文件）

对于源码来说，我们可能会频繁新增、修改、删除文章或者更改配置，如果需要将这些历史记录保留下来，那么可以使用版本管理的工具，比如 Git；另外，如果希望随时随地地写博客文章，而不被设备限制，那么可以使用一些云服务，比如 GitHub

而对于产物来说，本质上是不需要存储和管理的，我们也不在意其历史，因为产物总可以由对应版本的源码生成出来，而使用 Git + GitHub 后，我们已经可以随时随地查看不同版本的源码了。但是，由于本节后面讨论的部署方式需要产物也上传到 GitHub，所以我们这里也将产物存放在源码的仓库中一并管理起来，使用不同的分支以和源码区分，如源码使用 `main` 分支，产物使用 `publish` 分支

### 快速发布配置

我们将使用 [GitHub Pages](https://docs.github.com/en/github/working-with-github-pages) 以及 [Travis CI](https://docs.travis-ci.com/user/for-beginners/) 来快速的进行站点发布，Github Pages 可以理解为一个免费的和 Github 打通的云服务器，可以直接部署 Github 上的指定仓库指定分支的静态资源，并分配一个免费的同仓库名的域名；Travis CI 是一个免费的持续集成（Continuous Integration，CI）的平台，可以和 Github 打通去监听仓库的更改并执行相应的流水线。最终，我们的发布方式会从 *提交博客源码 -> 生成产物 -> 执行其他命令 -> 部署到服务器*，变成只用 *提交博客源码*

#### 使用 GitHub Pages

这一部分网上有比较多的资料可以参考，这里就不再赘述了，更多细节可以参考[这里](https://docs.github.com/cn/github/working-with-github-pages/creating-a-github-pages-site)。这里只强调下几个原则：

* 仓库名必须为 `<username>.github.io` ，其中 `<username>` 为你的 GitHub 用户名，为了下面展示方便，这里假设你的仓库名和我的仓库名相同，为 `ycydsxy.github.io`
* GitHub Pages 配置好后，可以通过 `https://<username>.github.io` 来访问，如果你不喜欢这个域名，你也可以换成你自己拥有的其他域名，更多细节可以参考[这里](https://docs.github.com/en/github/working-with-github-pages/configuring-a-custom-domain-for-your-github-pages-site)
* 在 `Hexo 配置文件` 中，将你的域名配置到对应的 `url` 配置项中（参见 [基本信息配置](#基本信息配置) 小节）
* 在该仓库的 Settings 里面，可以设置部署的分支，这里将其换成我们产物使用的 `publish` 分支

{% asset_img publish_1.png%}

至此，我们就已经可以发布我们的站点到互联网了。但是，由于我们将源码和产物放到同一个仓库里的不同分支里了，发布时既需要提交产物又需要提交源码，使得目前的发布过程比较繁琐。这里可以使用 Hexo 自带的[一键部署](https://hexo.io/docs/github-pages#One-command-deployment)命令简化操作，**当然你也可以完全不用管**，因为下面配置好 Travis CI 后，这些操作将会对你完全透明

#### 使用 Travis CI

这一部分网上的教程大多整的比较复杂和繁琐，可能是之前 Travis CI 功能上没有较好的支持，现在 Travis CI 已经和 GitHub Pages 深度打通了，直接可以配置式地进行 GitHub Pages 的部署

首先需要在 GitHub 中安装 Travis CI 应用，这样每次 GitHub 仓库有提交时都会通知 Travis CI。在 [Travis CI](https://travis-ci.com/getting_started) 使用 GitHub 账号登陆，登陆后直接会进新手引导页（不得不说新手引导做的真好），点击  *Activate all repositories using GitHub Apps* 申请并通过即可，更多细节可以参考[这里](https://docs.travis-ci.com/user/tutorial/#to-get-started-with-travis-ci-using-github)

{% asset_img publish_2.png%}

其次，在博客站点源码里增加 Travis CI 的配置文件 `.travis.yml `，该配置文件控制了 Travis CI 运行的流水线内容：

```yaml
sudo: false
language: node_js
node_js:
  - 10 # use nodejs v10 LTS
cache: npm
branches: main # 只监听哪个分支执行流水线，这里我们选择源码所在的 main 分支
script:
  - hexo generate # 生成
deploy:
  provider: pages # 使用 GitHub Pages 对应的部署方式，更多细节请戳 https://docs.travis-ci.com/user/deployment/pages/
  skip-cleanup: true # 一定要是 true，否则生成的产物会被清理掉，然后就部署了个寂寞
  github-token: $GH_TOKEN
  on:
    branch: main # 只监听 main 分支执行部署
  target_branch: publish # 部署到仓库的哪个分支里，我们这里是 publish 分支
  local-dir: public # 生成产物在哪个路径，我们这里是 public 路径
```



流水线运行过程中需要对 GitHub 相应仓库有写权限，这里使用 GitHub 提供的 Personal access token 来鉴权，也就是 `github-token` 这个配置项。该 token 泄漏也就意味着仓库权限的泄漏，所以这里不推荐将其直接写到配置文件中，而是只写一个环境变量名 `GH_TOKEN`，我们生成这个 token 后将其并配置到流水线对应的环境变量中即可。在 GitHub [Settings](https://github.com/settings/tokens/new) 页面进行 token 申请，勾选 repo 权限并提交之后，就会得到一个 token

{% asset_img publish_3.png%}

在 Travis CI 相关仓库 Settings 页面进行 `GH_TOKEN` 环境变量的配置

{% asset_img publish_4.png%}

{% asset_img publish_5.png%}

### 第一次自动发布

配置好后，我们可以向 `main` 分支进行一次提交（比如新增一篇文章），推到 GitHub 上以触发 Travis CI 的流水线，过几秒后就能在 Travis CI 中看到流水线执行了

{% asset_img publish_6.png%}

关注控制台的输出，如果成功运行结束且没有报错，则自动发布成功，可以访问 `https://<username>.github.io` 看是否已经发布了最新的站点（比如是否看得到你新增的那篇文章）

至此，自动发布博客站点的功能就配置完毕了，之后每次将最新的 `main` 分支推到远端都会触发流水线的自动执行。当然，这个流水线除了自动发布之外也可以有其他的用途，比如更新全文搜索的索引等，这个会在下文中进行讨论

## 使用插件

上文提到，我们的站点是全静态的资源，所以如果需要动态的功能，就需要涉及一些第三方的服务。NexT 提供了一些插件封装了与第三方服务交互的行为，简单配置一下就能使用，非常方便。使用插件的套路一般是，先在 `NexT 配置文件` 中找到某个插件的说明，然后去对应第三方服务里注册进行注册并获得 appID 和 token，然后将其配置到 `NexT 配置文件` 对应的配置项里即可

静态资源 + 第三方 API 实现动态功能的做法其实是有一定风险，主要的问题就是第三方 API 的权限泄漏问题。一般来说，“动态”的能力是通过插件调用第三方 API 写入或者读取数据而获得的，调用期间会传 appID 和 token 进行鉴权。但是，由于我们的站点中，所有对第三方 API 的请求是前端直接发出的，所以 token 其实是裸奔的，故需要特别关注该 token 在第三方服务中的 [ACL](https://en.wikipedia.org/wiki/Access-control_list)（如该 token 只允许读操作等）

在本节里，我们讨论三个比较常用的插件：**全文搜索**、**实时评论**和**阅读统计**

### 全文搜索：Algolia

[Algolia](https://www.algolia.com/) 是一个全文搜索服务，我们可以将博客的内容全部存储到该服务上并建立索引，然后调用该服务的 API 进行全文检索

在[官网](https://www.algolia.com/users/sign_in)使用 GitHub 账号注册和登录，然后在 Indice 配置中点击 `Create Index` 为你的站点新建一个索引

{% asset_img plugin_1.png%}

新建一个用于写入的 API Key，在 API Key 配置中点击 `New API Key`  并设置 ACL：

{% asset_img plugin_2.png%}

这两步完成后我们在 Algolia 中的操作就完成了，此时需要记录 `Application ID` 、`Search-only API Key` 和刚才创建的用于写入的 API Key。站点中的全文搜索的请求都会带上  `Search-only API Key` ，所以必须只能有读权限；而刚才生成的写入的 API Key，会在向 Algolia 写入数据的时候用到

更改 `NexT 配置文件` 中 Algolia 相关的配置：

```yaml
# Algolia Search
# For more information: https://www.algolia.com
algolia_search:
  enable: true # 打开 algolia 搜索
  hits:
    per_page: 10
  labels: # 自定义搜索展示文案
    input_placeholder: "你要搜点什么呢..."
    hits_empty: "未找到结果: ${query}"
    hits_stats: "共找到 ${hits} 条结果，耗时 ${time} ms"
```

更改 `Hexo 配置文件` 并向其新增有关 Algolia 的配置：

``` yaml
	algolia:
  applicationID: # 上面记录的 Application ID
  indexName: # 你新建的索引名称
  apiKey: # 上面记录的 Search-only API Key
  chunkSize: 5000
```

安装 `hexo-algolia` 包

``` plain
root@hexo_test:~/blog_test# npm install hexo-algolia --save 

added 20 packages, and audited 207 packages in 5s

15 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

在本地新增 `HEXO_ALGOLIA_INDEXING_KEY` 这个环境变量，值为之前生成的写入 API Key，然后运行 `hexo algolia` 命令即可将所有站点内容索引至 Algolia

本地调试好后我们将其配置进 Travis CI 的流水线，这样之后每次变更都能够及时索引到 Algolia：在 Travis CI 中同样增加环境变量 `HEXO_ALGOLIA_INDEXING_KEY` ，值为之前生成的写入 API Key，然后修改 `.travis.yml` 文件加入 `hexo algolia` 命令即可

```yaml
script:
  - hexo generate
  - hexo algolia # 将站点内容索引至 Algolia
```

最后，将这些更改提交并推到 GitHub 上，并查看效果，可以看到菜单栏上已经有搜索入口并且能够进行搜索了

{% asset_img plugin_3.png%}

### 实时评论：Utterances

 [Utterances](https://utteranc.es/) 是一个实时评论的插件，其原理是使用 GitHub 仓库的 Issue 来进行评论的存储，每个话题都会新建一个 Issue

在 GitHub 里进行 Utterances App 的安装，可以点击[这里](https://github.com/apps/utterances)进行安装

{% asset_img plugin_4.png%}

在 `NexT 配置文件` 中修改 Utterances 相关配置：

```yaml
# Utterances
# For more information: https://utteranc.es
utterances:
  enable: true
  repo: ycydsxy/ycydsxy.github.io # 存储 Issue 的仓库名，可以和博客站点仓库一致
  # Available values: pathname | url | title | og:title
  issue_term: pathname
  # Available values: github-light | github-dark | preferred-color-scheme | github-dark-orange | icy-dark | dark-blue | photon-dark | boxy-light
  theme: github-light
```

最后，将这些更改提交并推到 GitHub 上，并查看效果，可以看到文章底部已经可以看到评论插件了

{% asset_img plugin_5.png%}

> 这里着重强调一下，一些其他相同原理的评论插件（如 Gitalk 等）使用的是 OAuth APP，但 OAuth APP 鉴权粒度较大，Gitalk 实际上能获得你所有共有仓库的读取和写入权限，且相关密钥完全暴露在前端，故有较高的安全风险，更多细节可以参考[这里](https://github.com/gitalk/gitalk/issues/95)

### 阅读统计：LeanCloud

阅读次数统计其实就是每次访问将文章的点击量自增的操作，这里使用 LeanCloud 来进行数据的存储，网上已经有非常详细的[教程](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/LEANCLOUD-COUNTER-SECURITY.md)，这里不再赘述

# 结语

本文从 Hexo 和 NexT 的介绍开始说起，讨论了静态博客站点建设的基本流程和实施细节。文章写的比较冗长，一来是因为几乎所有的细节我都没有落下，二来是因为其中还杂糅了一些我的 ~~思考~~ 废话，请允许我为读到这里的朋友点个赞：

* 如果你是一个小白，读完本文后你应该习得了使用 Hexo 和 NexT 搭建自己博客站点的基础技能；
* 如果你是一个新手，读完本文后你应该了解了自动部署、插件安全相关的概念和实践；
* 如果你是一个老手，读完本文后你应该一无所获却为本文的阅读量贡献了一份自己的力量；

大家都有光明的前途！



