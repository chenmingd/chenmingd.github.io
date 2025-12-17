---
title: 零成本打造个人博客：用 Hexo + GitHub 全自动部署，轻松拥有专属网站
date: 2025-12-16 16:24:42
tags:
---
前言
==========
你是否也想拥有一个风格独特、加载迅速的个人博客或作品集网站，却又被服务器费用和复杂的部署流程劝退？这篇教程将为你提供一个完美解决方案。

本文详细介绍了如何利用 Hexo 这一高效的静态博客框架，结合 GitHub Pages 的免费托管服务与 GitHub Actions 的自动化工作流，从零开始搭建并全自动部署你的个人网站。你将学到：

* 环境搭建：如何快速安装 Node.js、Git 和 Hexo。

* 本地建站：初始化博客项目，并选用流行的 Butterfly 主题美化你的网站。

* 自动化部署核心：将代码托管至 GitHub，并通过配置简单的自动化脚本，实现“一次推送，自动发布”。从此，你只需专注写作，更新博客只需一个 git push 命令。

* 即刻测试：提供简单的测试步骤，让你立即验证自动化部署的成功。

整个过程完全免费，无需任何服务器预算，并能享受 GitHub 带来的稳定访问与版本管理优势。跟随本指南，只需不到一小时，即可让你的个人博客在互联网上优雅亮相。

第一、安装Hexo
==========================

## 什么是Hexo
Hexo 是一个快速、简洁且高效的博客框架。 Hexo 使用 [Markdown](https://daringfireball.net/projects/markdown/)（或其他标记语言）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

More info : [Hexo](https://hexo.io/zh-cn/)、[markdown](https://daringfireball.net/projects/markdown/)

## 安装环境要求

安装 Hexo 相当简单，只需要先安装下列应用程序即可：

- Node.js (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
- Git

### 安装Node.js
Node.js 为大多数平台提供了官方的[安装程序](https://nodejs.org/zh-cn/download/)。

其它的安装方法：

- Windows：通过 nvs（推荐）或者 nvm 安装。
- Mac：使用 Homebrew 或 MacPorts 安装。
- Linux（DEB/RPM-based）：从 NodeSource 安装。
- 其它：使用相应的软件包管理器进行安装。 可以参考由 Node.js 提供的[指导](https://nodejs.org/en/download)。

对于 Mac 和 Linux 同样建议使用 nvs 或者 nvm，以避免可能会出现的权限问题。
### 安装Git
- Windows：下载并安装[git](https://git-scm.com/install/windows)。
- Mac：使用 Homebrew, [MacPorts](https://www.macports.org/) 或者下载[安装程序](https://sourceforge.net/projects/git-osx-installer/)。
- Linux (Ubuntu, Debian)：`` sudo apt-get install git-core ``
- Linux (Fedora, Red Hat, CentOS)：`` sudo yum install git-core ``

## 安装Hexo
所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。
``` bash
$ npm install -g hexo-cli
```
执行`` hexo v `` 查看安装的hexo版本情况


第二、创建Hexo个人博客网站
==========================

## 创建博客网站

安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件
``` bash
$ hexo init <folder>
$ cd <folder>
$ npm install
```

初始化后，您的项目文件夹将如下所示：
<pre>
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
</pre>

More info : [Hexo建站](https://hexo.io/zh-cn/docs/setup)
## 选择主题配置博客网站

Hexo提供了很多[主题](https://hexo.io/themes/)，建站成功后可以选择喜欢的主题来装饰自己的网站

这里我选择[butterfly](https://butterfly.js.org/)作为网站的主题。它是一个基于[hexo-theme-melody](https://github.com/Molunerfinn/hexo-theme-melody)开发的主题，文档全面更新快。

> [!NOTE]
> **提示** 其他主题的安装方式与当前Butterfly安装方式是相同的

### 安装Butterfly主题

创建好Hexo个人博客网站后，就可以安装主题了

``` bash
$ cd <folder>
$ git clone -b dev https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
$ npm install hexo-renderer-pug hexo-renderer-stylus --save
```

### 应用Butterfly主题
修改 Hexo 根目錄下的 _config.yml，把主題改為 butterfly
``` yaml
theme: butterfly
```

More info : [Butterfly安装](https://butterfly.js.org/posts/21cfbf15/)

## 运行博客网站
``` bash
$ cd <folder>
$ hexo s
```
浏览器中输入 `` http://localhost:4000 ``

第三、发布博客网站至互联网
=======================
作为个人博客站的托管，这里将选择GitHub pages作为解决方案，并使用Github的workflow来自动发布Hexo网站变更，告别烦人的Hexo编译发布操作。

## 什么是GitHub 
GitHub 是一个基于 Git 的全球最大的在线代码托管平台和软件开发协作平台，它允许开发者存储、管理和共享代码，并提供版本控制、代码审查、项目管理、问题跟踪等功能，是开源社区和大型项目协作的首选地，也被视为开发者的社交和求职名片。

我们可以将自己Hexo站点的所有内容都托管到GitHub中,这样就可以在不同的设备，不同地点都能随时编写自己的博客，记录的生活。

More info : [GitHub](https://docs.github.com/zh)

## 什么是GitHub Pages
GitHub Pages 是一种免费的静态网站托管服务，它直接从你的 GitHub 仓库提取 HTML、CSS、JavaScript 文件，并为你发布一个公开的网站，非常适合托管个人博客、项目文档和组织官网。它支持自定义域名，并且能与 Jekyll 静态网站生成器集成，但不能运行服务器端语言如 PHP、Python.

More info : [GitHub Pages](https://docs.github.com/zh/pages)

## 托管Hexo博客站点内容至GitHub

### 创建GitHub仓库
创建GitHub仓库用于保存当前Hexo博客网站的所有信息，具体步骤如下

1. 在GitHub中注册一个账户。

2. 在任何页面的右上角，选择 ，然后单击“新建存储库”。
    ![](repo-create-global-nav-update.webp)
    
3. 使用“所有者”下拉菜单选择你想要拥有存储库的帐户。

4. 输入仓库的名称和说明（可选）。 如果要创建用户或组织站点，则存储库必须命名为 <user>.github.io 或 <organization>.github.io。 如果您的用户或组织名称包含大写字母，您必须小写字母。 
    ![](create-repository-name-pages.webp)
5. 选择仓库可见性 - 公共

6. 将README 切换为开启

7. 单击“创建存储库”。

在页面中找到类似 `` https://github.com/**.git ``的地址。并记住他。

### 上传Hexo博客站点信息到GitHub
需要将本地Hexo博客网站的所有内容都上传至`` https://github.com/**.git ``。具体操作
``` bash
$ cd <folder>
$ rm -rf .git
$ rm -rf themes/butterfly/.git
$ git init
$ git add *
$ git commit -m "first commit"
$ git branch -M main
$ git remote add origin https://github.com/**.git
$ git push -u origin main

```
> 注意：要将https://github.com/**.git换成自己的仓库地址。如果是第一次`` git remote add ``会让输入GitHub的验证信息，届时按照步骤操作就可以了

### 开启GitHub Pages功能
1. 在GitHub仓库名称下，单击 “Settings”****。 如果看不到“设置”选项卡，请选择“”下拉菜单，然后单击“设置”。
    ![](repo-actions-settings.webp)

2. 在边栏的“代码和自动化”部分中，单击“ Pages”****。

3. 在“生成和部署”的“源”下，选择“GitHub Actions”。

4. 在Hexo博客站点中创建一个``.github/workflows/pages.yml ``，并并填入以下内容
``` .github/workflows/pages.yml
name: Pages

on:
  push:
    branches:
      - main # default branch

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          # If your repository depends on submodule, please see: https://github.com/actions/checkout
          submodules: recursive
      - name: Use Node.js 20
        uses: actions/setup-node@v4
        with:
          # Examples: 20, 18.19, >=16.20.2, lts/Iron, lts/Hydrogen, *, latest, current, node
          # Ref: https://github.com/actions/setup-node#supported-version-syntax
          node-version: "20"
      - name: Cache NPM dependencies
        uses: actions/cache@v4
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Upload Pages artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./public
  deploy:
    needs: build
    permissions:
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
5. 将添加的文件保存至GitHub

``` bash
$ cd <folder>
$ git add .github
$ git commit -m 'add github workflow'
$ git push
``` 

6. 等几分钟，就能通过https://<user>.github.io 或 <organization>.github.io访问自己的博客了

> [!NOTE]
> **注意：** 这里的user、organization是自己GitHub账户名或者组织名

第四步 小试牛刀，测试自动部署网页的情况
=================================

1.在本地电脑使用命令创建一个文档，并添加自己的博客内容
2.使用git将刚刚新建的文档推送至github.等几分钟后就可以在网页中看到新建的页面了
3.修改刚刚的文档，然后再次推送至github.查看页面效果

参考
========
- [1] [Hexo安装指南](https://hexo.io/zh-cn/docs/)
- [2] [Butterfly安装配置指南](https://butterfly.js.org/posts/21cfbf15/)
- [3] [Hexo GitHub Pages配置指南](https://docs.github.com/zh/pages)
- [4] [GitHub创建仓库指南](https://docs.github.com/zh/get-started/start-your-journey/hello-world)
- [5] [Git基础用法](https://docs.github.com/zh/get-started/learning-to-code/getting-started-with-git)