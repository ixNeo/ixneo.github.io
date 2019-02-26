---
layout:     post   				    # 使用的布局（不需要改）
title:      博客搭建			# 标题 
subtitle:  　#副标题
date:       2019-02-26 				# 时间
author:     jktian 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:							#标签
    - 工具
    - 博客搭建
---


# 博客迭代

1. 第一次，用腾讯云主机作为后台，买了域名，用wordpress，mysql, apache, linux搭建。
	- 由于域名需要备案，且云主机第二年优惠消失，所以开始迁移计划
	- 本次学到
		- 服务器的配置过程，linux的基本操作
		- 在别人以及文档的帮助下，能少走很多弯路
2. 第二次，用gitbook搭建。无需后台，像写书一样，但是自由度有限。
	- 由于作为一本书，博客所能写的内容和跨度不能太大，且访问速度慢，所以继续迁移
	- 本次学到
		- markdown写法的熟练操作
		- github不仅能用于资源存储和版本管理，更是社交的地方
3. 第三次，即本次，用github作后台，jekyll辅助搭建
	- 用tag来取代具体的类别，让不同的文章自由组成类别，而不是在固定类别下写文章
	- 用了百度统计，监督网站动态
	- 评论功能开发中


# jekyll命令行

    gem install jekyll bundler
    
    jekyll new my-awesome-site
    
    cd my-awesome-site
    
    bundle install
    
    bundle exec jekyll serve
    
    blog目录下：　jekyll s # 本地运行，端口4000


# problem
1. gem的安装。如遇问题，删除之后重新安装.
	- 即使有复杂的依赖项关系，也不要慌
2. 缓存问题。浏览器会有网页的缓存，记得修改之后，要删除缓存再查看
	- 适合情况：使用jekyll本地开启端口查看网页


