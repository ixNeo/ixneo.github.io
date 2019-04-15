---
layout:     post   				    # 使用的布局（不需要改）
title:      linux-manjaro			# 标题 
subtitle:  　
date:       2019-03-20 				# 时间
author:     jktian 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
category: 攀天索--工具
tags:							#标签
    - linux
---
* content
{:toc}

常用命令
---

- 查找端口并删除进程:
  - $ lsof -i:<post>
  - $ kill -9 <pid>

# 文件
- touch 更新文件的访问／修改时间；创建文件
# 系统工具
# 命令工具
- which 显示命令的路径名和别名
- tar -zxvf file # 解压缩
- tar -zcvf file # 压缩




# 文件系统
- du
- df 显示文件系统已使用／可使用的磁盘空间
- mount 挂载文件系统
- umount 卸载文件系统
- fdisk 磁盘分区工具，可以扩展分区


# 比较文件
- cmp
- diff
- sdiff(推荐)　比较两个文件，显示区别


# 登录和注销
- login 终止登录shell并初始化一个新登录
- loginout 终止登录shell
- passwd 改变登录口令



# 目录
- cd 改变工作目录
- chmod 改变文件或目录的文件权限
- chown 改变文件属组
- du 显示文件使用的磁盘空间量
- file 分析文件类型
- ls 显示文件的各种类型信息
- dirs 显示目录列表
- mkdir 创建目录
- mv 移动或重命名文件或目录
- pwd 显示工作目录的路径名
- rm 删除文件或目录
- rmdir 删除空目录
- tree 显示目录树的图表


# 进程和作业控制
- & 在后台挂起程序
- fg 将作业移到前台
- bg 将作业移至后台
- suspend 挂起（暂停）shell
- jobs 显示作业信息
- ps 显示显示进程信息
- top 显示使用最多CPU的进程的数据
- pstree 显示进程树图表
- kill 终止进程；给进程发送信号
- kill -9 pid # 只杀进程本身
- kill pid 杀本身和子进程
- nice 使用指定的调度优先级运行程序



# 系统工具
- dmesg 显示启动信息
- reboot
- shutdown
- su 改变到超级用户
- sudo
- uname
- uptime
- free 查看内存使用情况
- service 服务相关
- crontab -l　查看定时任务
- crontab -e 新增


# 工具
- cal 显示一个日历


# 显示数据
- cat 组合文件，将标准输入复制到标准输出
- echo 将参数写到标准输出
- less 分页程序
- more
- head 从数据的开头选择行
- tail 在数据的末尾选择行


# shell
- exit 退出shell
- history 显示历史命令


# 用户和用户标识
- group 显示用户标识所属的组
- id　显示当前用户标识和组标识
- last　查看用户标识上一次登录时间
- w　显示用户标识和活动进程的信息
- who
- whoami

# 文档资料
- info 从info参考系统中显示文件
- man 显示Unix联机参考手册的页面
- help


# 选择数据
- grep 正则表达式 file #  选择包含指定模式的行
- cut
- head
- look
- tail
- find /path/to -name ""


# 变量
- env 显示环境变量
- set 设置／显示shell选项和shell变量

# 编辑
- vi vi文本编辑器
- vim vim文本编辑器

# 用户管理
- su USER 切换用户
- useradd USER 添加用户 -u 指定uid，-g指定gid
- userdel USER 删除用户 -r删除家目录和mail账户
- groupadd  GROUP 添加组
- groupdel GROUP 删除组
- passwd [USER] 默认修改自身密码（普通用户可以），加用户名修改某用户密码（root）

