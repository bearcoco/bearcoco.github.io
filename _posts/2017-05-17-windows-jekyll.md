---
layout:     post
title:      "在windows上安装Jekyll"
subtitle:   "使用Jekyll本地搭建开发环境"
date:       2017-05-17
author:     "zgx"
header-img: "img/post-bg-js-version.jpg"
catalog: true
tags:
    - 前端开发
    - 博客
    - jekyll
---
前面安装jekyll是在公司的mac上进行安装的，而家里的是windows系统的笔记本，所以要发表博客的话肯定要安装好环境了，但windows的安装又跟mac的不一样。折腾了一下，感觉是比在mac上安装来得麻烦。以下呢？就是在windows上安装jekyll的步骤以及一些可能遇到的问题。

首先呢在这里就不再介绍jekyll是什么了，可以访问前面写的[在mac上安装Jekyll](http://bearcoco.com/2017/05/15/mac-jekyll/)

搭建jekyll基本都满足如下步骤:
- 安装ruby(2.0.0以上)，并且安装DevKit。
- 切换ruby的source来源
- 通过gem命令安装jekyll
- github上fork心仪的jekyll模板，本地jekyll serve运行相应的博客

### 安装ruby
**下载ruby**
在windows上它不像mac有自带ruby，所有首先安装ruby，到[ruby下载地址](http://rubyinstaller.org/downloads/)下载对应的ruby版本。推荐下载2.0.0，其他的版本没实践过。然后根据自己电脑的系统选择对应的ruby，当然还有对应DEVELOPMENT KIT的下载。
**安装ruby2.0.0**
下载完安装包后，先安装rubyinstaller, 记得尽量以**管理员的权限**安装 安装时会有三个选项。
![环境变量](http://function.bypanda.cn/ruby.jpg)
请全部选上。全部选上在安装完毕后，环境变量也会自动配置。安装完之后win+R进入控制台输入命令**ruby -v**，如果显示版本号则表示安装成功。
### 安装EVELOPMENT
安装完ruby后，接着安装DevKit(请确保管理员权限安装) 点击安装，选择完对应的目标（默认地址就行了）后，点击确认即会自动提取。
在windows的命令行cd到安装的目录下，输入
```
ruby dk.rb init
```
待运行完毕后，该目录中会自动生成一个config.yml文件。将文件的内容修改成以下：
![config](http://function.bypanda.cn/ruby2.png)
也就是在文件内容的后面加上：**- C:\Ruby200-x64** ，这个表示的是刚才安装ruby的路径地址。修改完之后，继续在控制台输入命令：
```
ruby dk.rb install
```
至此，代表Development Kit已经正确安装并成功配置。

### 更改默认的source源
鉴于官方源无法访问，所以我们得更换为可以使用的源，这里推荐使用[ruby china源](https://gems.ruby-china.org/)，大致步骤如下:

- 先键入命令**gem sources -l**查看当前已经添加的源(默认应该是同时有官方源和淘宝源)
- 然后通过 **gem sources -r https://rubygems.org/ 和 gem sources -r https://ruby.taobao.org/** 分别移除官方源和淘宝源 (注意，请对比实际，移除自己已经添加的源即可，可以改为自己上一步中查询出来的地址)
- 通过 **gem sources -a http://gems.ruby-china.org** 添加了ruby china的可用源
- 修改来源后可以通过**gem sources -l**查看是否正确修改

### 安装jekyll
安装jekyll前先按照依赖包bundler，输入命令：
```
gem install bundler
```
按照依赖包bundler之后，直接安装jekyll，输入命令：
```
gem install jekyll
```
安装需要一定的时间，过一段时间正常安装后即代表jekyll可以开始使用了。

### 使用jekyll
这个步骤跟前面在mac上安装使用jekyll是差不多的。

首先，你可以到[http://jekyllthemes.org/](http://jekyllthemes.org/)上面找一个自己喜欢的jekyll模板，然后将对应的项目git clone到自己本地的目录下，同样用cmd命令进入对应的目录。

输入以下命令生成博客，默认生成再_site目录下：
```
jekyll build
```
开启jekyll本地预览服务：
```
jekyll serve
```
在浏览器中输入 http://localhost:4000 即可访问博客站点。
如果出现Error：jekyll-paginate
![error](http://function.bypanda.cn/jekyll.jpg)
输入命令：
```
gem install jekyll-paginate
```
再不能访问请检查_config.yml配置文件是否需要修改。

部署到Github pages请移驾到[在mac上安装Jekyll](http://www.bearcoco.com/2017/05/15/mac-jekyll/)