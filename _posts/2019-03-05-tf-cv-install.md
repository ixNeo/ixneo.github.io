---
layout:     post   				    # 使用的布局（不需要改）
title:      环境搭建			# 标题 
subtitle:  	 
date:       2019-03-04				# 时间
author:     jktian 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - python
    - tools
---
# conda
1. conda install <url/package_name>	# 可能需要事先切换到python36，代替py37
2. conda info <package_name>	# 打印关于包的信息，有不同版本的tar.gz下载url

# tensorflow
1. 根据conda info, 得到依赖项。不仅要安装tensorflow本身，同时也要conda info 依赖项，来安装依赖的包
2. 和tensorboard
   1. 可能会有版本问题
   2. 重新安装大法好。pip upgrade不靠谱，直接uninstall再install即可
   3. 命令：tensorboard --logdir <log_path>
> 调试技巧：
> 	判断大概位置，逐步调试，验证假设，模块化问题点

# opencv
1. import cv2

# python包的安装方式
1. pip install
2. conda info, 然后conda install <url>
3. setup.py, 安装.whl