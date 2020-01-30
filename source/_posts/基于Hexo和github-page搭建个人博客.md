---
title: 基于Hexo和github page搭建个人博客
date: 2020-01-29 19:46:47
tags: 小白
---

倒腾过好几次个人主页，但个人原创文章并不多，总是要么在换模板的路上，要不就是在换框架的路上，终于乐此而疲了。这次换个人主页之后还是要静下心来多写文章才是。这篇文章用于答谢Hexo和Archer主题的作者，hexo是到目前为止用过的最好用的博客框架，archer主题模板是目前个人比较喜欢的一款模版。

废话不多说，按照个人习惯，分四段简单介绍下如何基于Hexo和Github Page搭建个人主页。

> 本文不严格区分*nix系统和windows系统，所有命令均可在terminal或者gitbash中执行。

## 0x00 准备

hexo是一个静态站点生成工具，集创建（初始化站点）、开发（指的是写博客）、发布博客文章功能于一体，十分方便。

搭建博客站点先准备以下平台的账号和开发环境：

- 注册github账户，[链接](https://github.com/)

- 安装git，并在github账户中配置sshkey：*nix系统一般自带git，windows系统安装gitbash，[下载地址](https://gitforwindows.org/)

- 配置sshkey：

  - 生成sshkey：*nix系统中打开terminal，windows系统中打开gitbash，参考[教程](https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)，执行以下命令，

    ```bash
    cd ~ && ssh-keygen -t rsa -b 4096 -C "your_email@example.com" # your_email@example.com替换为你注册github的邮箱，可以一直按回车生成默认的文件名，方便阅读后续的步骤
    ```

  - 执行以下命令，拷贝出你的public key，将屏幕中输出的公钥内容`ctrl+c`进行拷贝：

    ```bash
    cd ~/.ssh/ && cat id_rsa.pub # 这里的id_rsa.pub为上一步生成的密钥对中的公钥
    ```

  - 打开github中配置sshkey的界面，[链接](https://github.com/settings/keys)，选择`New SSH key`，把拷贝的公钥配置上去即可。

- 安装Nodejs，[下载地址](https://nodejs.org/zh-cn/)，安装成功后会同时安装好node和npm两个工具，并为npm配置国内源，例如配置淘宝源可以执行下述命令：

  ```bash
  npm config set registry https://registry.npm.taobao.org
  ```

- 安装hexo，执行下述命令

  ```bash
  npm install hexo-cli -g # install hexo
  hexo -v # check whether successfully installed
  ```

## 0x01 初始化站点

执行以下命令来初始化博客站点，会创建一个新的目录，以blog-dev为例，执行：

```bash
hexo init blog-dev
```

待命令执行完毕，会新建一个blog-dev目录，进入该目录中，我们可以看到以下目录树：

```bash
blog-dev
├── _config.yml        #---------------- 站点配置文件
├── node_modules       #---------------- npm安装包本地保存目录
├── package-lock.json
├── package.json       #---------------- 依赖包配置文件
├── scaffolds
├── source             #---------------- 博客文章保存目录
└── themes             #---------------- 博客主题保存目录
```

此时，进入到blog-dev目录，可以执行hexo的相关参数及命令，可以进行站点的管理，简单介绍如下：

```bash
hexo clean # 清除缓存
hexo generate # 生成网站静态文件
hexo server # 启动本地调试模式，默认可以打开localhost:4000查看网站效果
hexo deploy # 发布到GitHub Page，第0x11节会具体介绍
```

hexo还有一个非常方便的点是主题套用十分方便，将想要的模板下载下来，放到themes目录下，然后修改_config.yml文件中的theme字段，改为下载下来的主题目录名即可。主题可以在[官方网站下载](https://hexo.io/themes/)，也可以自行从各种渠道获取。

## 0x10 创建github page

本节内容大家应该都比较熟悉，创建作为个人主页用的github page，必须将仓名命名为username.github.com，经过测试，仓名中的username与你的github账号名可以不区分大小写。

这部分教程我想偷懒跳过了，可以自行查看[官方教程](https://pages.github.com/)。

## 0x11 预览和发布

在blog-dev目录下执行`hexo new '博客标题'`即可创建一篇新的博客，使用markdown语法进行编辑。

编辑完毕之后，执行下述命令，可以启动一个本地的临时服务器进行预览：

```bash
hexo server # 启动本地预览服务
```

在浏览器中打开`localhost:4000`，即可预览你的博客。

配置blog-dev的发布路径，编辑blog-dev/_config.yml文件，一般在文件末尾，有一个deploy字段，把第三节创建的github page仓库路径配置上去即可，如果deploy字段下只有一个type，则手动添加其他字段（注意yml文件遵从yaml格式缩紧）。例如我的配置就是：

```yaml
deploy:                                                                                                          
  type: git
  repo: https://github.com/ChinoMars/chinomars.github.io.git
  branch: master
```

依次执行下述命令，即可发布你的静态站点：

```bash
hexo clean # 清除缓存
hexo generate # 生成站点的静态文件
hexo deploy # 自动push到github page所在的master分支，进行发布
```

最后，可以打开网址：`https://username.github.io`即可查看个人的站点。