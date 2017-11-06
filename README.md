# ubuntu 部署 hexo 博客  

## hexo 简介  

Hexo 是一个快速、简洁且高效的博客框架。Hexo 基于 Node.js，可以方便的生成静态网页托管在 github 上。  
Hexo 使用 Markdown（或其他渲染引擎）解析文章，页面风格多变，适合于搭建个人博客。在几秒内，即可利用靓丽的主题生成静态网页。

## 准备工作  

> 1. github 帐号  
> 2. PC 已经安装 git  

> 本文环境： ubuntu 16.04  

## 安装 Node & npm  

Nodejs 是一个 js 框架，用于静态博客托管，因此，首先需要安装 Node.    
npm 是 node 的包管理工具，因此需要安装 npm.  
可以采取命令行直接安装：  

    $ sudo apt-get install nodejs
    $  sudo apt-get install npm  

注：  使用apt-get 安装的nodejs版本过老，会导致安装hexo的时候出问题。  
官方推荐的安装方法：

    curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
    sudo apt-get install -y nodejs  

## 安装 hexo  

我们使用 npm 安装 hexo:  

    $ sudo npm install hexo-cli -g
    $ sudo npm install -g hexo  
安装完成后进行初始化：  
初始化时需要添加以后存放博客以及配置文件的文件夹  

    $ hexo init <your folder>  
    $ cd <folder>
    $ npm install  //安装依赖
至此，hexo 已经安装完毕，可以进行本地测试。  

## hexo 命令 和本地测试

- 常用命令  

|命令|释义| 
|:---:|:---:| 
|hexo g|generate ,编译成静态文件|  
|hexo d|deploy, 部署网站|
|hexo s|server, 本地运行|
|hexo c|clean, 清空generate生成器的文件|  

- 本地测试  

        $ cd ~/<folder>
        $ hexo generate     #生成博客
        $ hexo server   #运行本地服务  

在浏览器输入 http://localhost:4000 就可以看到效果.  

- 目录结构  

当安装成功后，可以看到 hexo 的目录结构如下：  

```
├── _config.yml
├── db.json
├── node_modules
├── package.json
├── public
├── scaffolds
├── source
└── themes
```

## 部署到 github  

#### github 创建仓库  

在 github 上创建一个与自己用户名对应的 github 仓库，仓库名如下：  

【your_user_name.github.io】

*注：务必对应自己的用户名，且建成后不要添加 README 等文件，只需要一个空仓库即可。*



#### 配置修改  

在 hexo 的配置目录下的 `_config.yml` 文件为博客的配置文件，可以对网页端的一些属性和内容进行修改。 
```
title: 这里填写博客的标题
subtitle: 这里填写博客的副标题
description: 这里填写博客的描述
author: 这里填写博客的作者
language: 这里填写博客的语言,如果是中文填写”zh”
url: 这里填写我们之前申请的博客网页存放空间的网址,例如我们的github用户名为”aaa”,这里就填写”http://aaa.github.io”
deploy:
type: 这里填写”git”
repo: 这里填写我们之前申请的git仓库的地址,例如我们的用户名为”aaa”,则此处填写”git@github.com:aaa/aaa.github.io.git”
```

注： url 可以选择为自己所申请的域名。如果没有申请，则使用 http://your_user_name.github.io  

#### 推送至远端  

推送至 github 还需要安装 hexo-git 插件：  

	npm install hexo-deployer-git --save  

这样，在调用 	`hexo d` 的时候就可以自动 push 到 github 上。

#### 建立 hexo 分支  

为了更好的保存自己 hexo 的配置和方便存档，可以建立一个 hexo 分支，用来存放现在 hexo 的所有配置文件。  
把生成的 public 目录下的文件放到 master 分支下即可。git commi后把这两个分支推送到你的 github 上。

![](https://i.imgur.com/c6feNZ1.png)

*----------------------------华丽的分割线----------------------------*

至此，github 的部署设置已经完成，执行

    hexo d

然后在浏览器中输入 http://your_user_name.github.io 就可以访问自己的博客啦！  

以后每次的部署步骤可以按照以下三步：  

    hexo clean

    hexo generate

    hexo deploy  
    
*注：部署出错 clean 一下一般都可以了~*

## 写一篇新博客  

使用如下命令即可新建一篇名为 test 的博客：  

	hexo new test  

test.md 存放于 `sources/_posts`. 博客的正文格式如下：  
```
title: test
tags:
  - Ubuntu
  - Hexo
categories:
  - Hexo
date: 2017-11-3 15:31:00
---

## 以下为 Markdown 文章正文。
```
当博客推送到远端后，即可在前面提到的网址进行访问查看。

## 常见问题  

- ERROR Deployer not found: git 或者 ERROR Deployer not found: github

 解决方法： npm install hexo-deployer-git --save


- ERROR Plugin load failed: hexo-server

 解决方法，执行命令：

 sudo npm install hexo-server  

## 总结

在部署安装时一定一步一步来，在出现各种莫名的问题时，首先看命名是否出错，然后建议去 hexo 的 github 主页的 issues 中查找对应的问题，一般都会有类似的问题和解答。



  







