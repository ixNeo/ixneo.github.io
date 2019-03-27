---

layout:     post   				    # 使用的布局（不需要改）
title:      微信小程序开发			# 标题 
subtitle:  	 
date:       2019-03-25				# 时间
author:     jktian 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
category: 历劫桥--项目实战
tags:								#标签
    - log
    - web

---
* content
{:toc}

# 环境搭建
微信小程序开发工具: 只支持windows/macos
本机的win7无法正常显示
linux下:
1. wine	# windows虚拟模拟程序,可以选择windows版本

2. 安装nwjs-sdk
wget https://dl.nwjs.io/v0.25.4/nwjs-sdk-v0.25.4-linux-x64.tar.gz 
tar xvf  nwjs-sdk-v0.25.4-linux-x64.tar.gz

3. 获取微信开发工具包
git clone https://github.com/cytle/wechat_web_devtools.git

4. 结合nwjs和微信开发包
复制微信开发工具包（package.nw在wechat_web_devtools目录下）到nwjs-sdk目录下
5. 启动
./nw