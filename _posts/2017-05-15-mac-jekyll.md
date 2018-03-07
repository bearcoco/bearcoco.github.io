---
layout:     post
title:      "在mac上安装Jekyll"
subtitle:   "Jekyll本地搭建开发环境以及Github部署流程"
date:       2017-05-15
author:     "zgx"
header-img: "img/post-bg-js-version.jpg"
catalog: true
tags:
    - 前端开发
    - 博客
    - jekyll
---

作为一个程序员，特别是一个前端，将Blog挂在大众博客上面就太没意思了。当然并不是说把Blog挂在大众博客上面没意义，只是个人感觉现在的大众博客页面都太丑了，除了简书的页面好点，其他的更是广告横飞。于是这个基于GitHub Pages + Jekyll 的博客主题就这么被我折腾出来了。

### Jekyll是什么？

Jekyll是一个简单静态博客生成工具，为什么是静态，因为它是不需要数据库的，通过markdown编写静态文件，生成Html页面。它有什么优点呢？
- 流行又简洁的MarkDown写作语法
- 轻量级的网站结构，不再有动态网站的沉重
- 方便的和github pages结合，不仅免费，而且方便
- Jekyll 的自定制非常容易，基本就是个模版引擎

### 安装Homebrew

使用Mac的程序员必不可少的一步便是安装Homebrew, Homebrew是基于Ruby安装, Mac默认自带Ruby。
运行以下命令进行安装：

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### 安装最新版ruby

Mac上是有默认自带Ruby，我们要做的事将它更新为最新的版本。使用刚才安装好的Homebrew进行安装，输入命令行：
```
brew install ruby
```

安装完成之后，会提示安装好的ruby目录为**/usr/local/Cellar/ruby/2.4.1**,想要最新安装的ruby生效，需要将**~/.zshrc**配置文件中的环境变量PATH中添加上新版本ruby的目录，在PATH后添加上ruby安装目录的bin文件夹，如下：
```
export PATH="/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/Cellar/ruby/2.4.1/bin"
```
然后输入命令：

```
source ~/.zshrc
```
输入命令
```
ruby -v
```
查看ruby版本，显示的将是最新的版本

```
ruby 2.4.1p111 (2017-03-22 revision 58053) [x86_64-darwin15]
```
如果，版本不对，就使用命令**echo $PATH**查看最新版本的ruby目录是否在环境变量PATH中，如果不对，就按照上述过程修改环境变量PATH

###  安装jekyll
输入命令行：
```
gem install jekyll
```
因为我们将会使用Markdown语言作为标记语言，所以还需要安装kramdown，命令如下：
```
gem install kramdown
```
至此，jekyll已经安装成功了，可以在本地上运行环境了。

### 使用jekyll

首先，你可以到[http://jekyllthemes.org/](http://jekyllthemes.org/)上面找一个自己喜欢的jekyll模板，然后将对应的项目git clone到自己本地的目录下，同样用cmd命令进入对应的目录。

输入以下命令生成博客，默认生成再_site目录下：
```
jekyll build
```
开启jekyll本地预览服务：
```
jekyll serve
```
在浏览器中输入 http://localhost:4000 即可访问博客站点
不能访问请检查_config.yml配置文件是否需要修改

在本地上可以预览博客站点后就可以使用Jekyll写博文，进入博客目录的_post文件夹，撰写的markdown语法的博文都放在这里。如何撰写可以参考[jekyll中文网](http://jekyllcn.com/docs/posts/),这里就不写了。写完之后刷新一下浏览器、发现页面并没有变化.因为我们还没有通过Jekyll build去生成。
```
jekyll build
```
然后再输入命令**jekyll serve**进行本地预览。

jekyll目录结构
- 文件夹_layouts：用于存放模板的文件夹，里面有两个模板，default.html和post.html
- 文件夹_posts：用于存放博客文章的文件夹
- 文件夹css：存放博客所用css的文件夹
- _site：jekyll自动生成的目录，为静态的页面
- _coinfig.yml：jekyll的配置文件，里面可以定义相当多的配置参数，具体配置参数可以参照其官网

### 部署Github pages服务

部署到Github Page，首先肯定要有github账号，没有的话自己去注册一个。然后创建一个跟你账户名一样的仓库，如我的github账户名叫zgxpro， github仓库名就叫 zgxpro.github.io，创建好了之后，把刚才建立的 myBlog 项目 push 到username.github.io仓库里去（username指的是你的github用户名），检查你远端仓库已经跟你本地 myBlog 同步了，然后你在浏览器里输入username.github.io ，就可以访问你的博客了。 　
本地Jekyll站点部署到Github Pages的命令：
```
git add --all               #添加到暂存区    
git commit -m "提交jekyll默认页面" #提交到本地仓库
git push origin master           #线上的站点是部署在master下面的
```
稍等个几分钟左右，Github Pages有一定时间缓存,我们刷新username.github.io看看,已经ok了！

### 绑定个人域名
一般情况下，别人想访问的是咱们自己的个人网站，而不是去访问username.github.io。所以就要为username.github.io绑定个人域名。
我们要绑定的话需要在username.github.com目录下增加一个CNAME文件。
在里面添加你的域名，假设为example.com，然后推送CNAME文件到远程仓库:
```
git add CNAME
git push origin master
```
到域名服务商增加你的CNAME记录。
添加两条记录，@和www的主机记录，记录类型为CNAME类型，CNAME表示别名记录，该记录可以将多个名字映射到同一台计算机。
记录值请写username.github.io.,值得注意的是io后面还有一个圆点，切记。
![CNAME记录](http://upload-images.jianshu.io/upload_images/21868-188b926c62db15e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 后记
稍等几分钟，刷新自己的博客地址，我的博客域名是[bearcoco.com](http://bearcoco.com/)，就能直接访问了。
差不多就这样了，之后你可以在_posts文件夹里继续撰写博文，然后按照上面步骤上传到github即可。


















