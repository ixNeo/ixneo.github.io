---
layout:     post   				    # 使用的布局（不需要改）
title:      python多进程			# 标题 
subtitle:  	 #副标题
date:       2019-02-26 				# 时间
author:     jktian 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - python
---
# python多进程
利用multiprocessing库，使用多进程，而不是多线程，充分利用多核cpu资源
举例：生产者和消费者问题
 ## Process
 - 创建进程，传入参数为要执行的函数。一个进程就是一个Proccess类的实例
 - 自定义类，继承Process类，重载run函数
 - 进程的deamon属性。若为true, 表示父进程结束，则子进程自动终止
 - 子进程的join函数。表示父进程等待子进程执行完毕
 ## Lock
 - 避免并行导致输出错位。让同一时间只有一个进程操作临时资源
 - Lock类的实例。有acquire()和release()方法
 ## Semaphore　信号量
- 控制临界资源的数量，保证进程之间的互斥和同步
- semaphore和mutex结合使用。mutex是互斥锁
 ## Queue　共享队列
 - 用于进程间通信，不同与普通的队列。
 - 有空异常和满异常
 ## Pipe
- 一端的进程发，一端的进程收
- 单向或双向
 ## Pool　进程池
 - 不再手动创建进程。用pool指定数量，如果没满，创建新的；如果满的，等待
 - 阻塞式和非阻塞式
 - map函数，
