---
layout:     post   				    # 使用的布局（不需要改）
title:      python黑魔法			# 标题 
subtitle:  	 #副标题
date:       2019-03-16				# 时间
author:     jktian 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - python
---
# with
with只适用于上下文管理器的调用，除了文件外，with还支持 threading、decimal等模块，当然我们也可以自己定义可以给with调用的上下文管理器
使用类定义上下文管理器。
``` python
    class A():
        def __enter__(self):
            self.a=1
            return self
        def f(self):
            print 'f'
        def __exit__(self,a,b,c):
            print 'exit'
    def func():
        return A()

    with A() as a:
        1/0
        a.f()
        print a.a
```

# time

time.sleep()模拟时间延迟/读写数据延迟/网络延迟
计算耗时：time.time()用于记录起始和结束时间