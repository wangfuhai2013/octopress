---
layout: post
title: "第一次在github上搭建博客"
date: 2013-05-17 17:34
comments: true
categories: 
---
决定开始写博客，好好整理一下技术经验。现在大家都用github的Pages服务部署静态页面做博客，第一篇博客就记录一下搭建的过程。

### 注册github账号，并建立博客网站的仓库
在(https://github.com/signup/free)申请好github账号后，建一个名为 USERNAME.github.com 的代码仓库.USERNAME即账号名，实际操作即进行相应替换，如wangfuhai2013(下同)。

我是通过github的官方的客户端程序建立的代码仓库(repository)，本地代码仓库存放目录为/opt/data/github

### 在本地安装Jekyll，并推送到github

    $ cd /opt/data/github 
    $ git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com 
    $ cd USERNAME.github.com 
    $ git remote set-url origin git@github.com:USERNAME/USERNAME.github.com.git 
    $ git push origin master

push前，可先删除jekyll-bootstrap中的示例内容

    $ rm -rf _posts/core-samples

### 配置Jekyll
在`_config.yml`中修改博客名称、作者名、email地址信息

    $ cd USERNAME.github.com 
    $ vi _config.yml 

### 创建文章，修改文章内容

    $ rake post title="first install blog"
    $ vi _posts/2013-05-14-first-install-blog.md

修改后，生成实际页面，看一下有没有什么错误

    $ jekyll build

### 修改首页及其他页面
首页是一个页面，直接修改相应的md文件

    $ vi index.md

jekyll中创建页面的命令跟文章不一样

    $rake page name="about.md"

### 发布博客
先在本地运行jekyll，通过localhost:4000地址预览一下效果

    $ jekyll serve

再push到github上

    $ git add -u
    $ git commit -m 'create a new post'
    $ git push origin master

### 使用自己的域名
1. 在自己的域名解析中加一条CNAME记录，指向github的域名(USERNAME.github.com)
2. 在网站根目录下加一个文件CNAME,写入自己的域名，如:blog.chinaework.com
3. 修改`_config.yml`中的production_url设置，设为自己的域名地址

###更换markdown解释器
jekyll默认是用Maruku做markdown的解释器，但Maruku是ruby写的，效率较低，可以换成用c写的RDiscount，效率更好
先安装RDiscount

    $ gem install rdiscount

再修改`_config.yml`文件，增加一行地：
    markdown: rdiscount

但RDiscount在build过程中，不会报告markdown的语法错误，而Maruku会清楚文件内容中的语言错误。

### 配置评论功能
在[disqus](https://disqus.com/admin/signup/)注册账号后，修改`_config.yml`中的short_name设置

### 配置google analytics
在[googel analytics](https://www.google.com/analytics)中增加媒体资源后，修改`_config.yml`中的tracking_id设置

--------------------------

# 换用octopress


### 参考资料
* [jekyllbootstrap](http://jekyllbootstrap.com/) 
* [jekyll官网](http://jekyllrb.com/) 
* [octopress-is-pretty-sweet](http://joelmccracken.github.io/entries/octopress-is-pretty-sweet/) 
* [告别wordpress，拥抱jekyll](http://www.yangzhiping.com/tech/wordpress-to-jekyll.html) 
* [octopress安装](http://blog.devtang.com/blog/2012/02/10/setup-blog-based-on-github/) 
* [jekyll与octopress的比较](http://www.multunus.com/2012/10/our-experience-with-jekyll-and-octopress) 
* [jekll网站例子](http://https://github.com/mojombo/jekyll/wiki/sites)
* [markdown语法](http://daringfireball.net/projects/markdown/syntax) 


