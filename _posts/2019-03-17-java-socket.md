---
layout:     post   				    # 使用的布局（不需要改）
title:      java模拟路由表构建			# 标题 
subtitle:  	 
date:       2019-03-15				# 时间
author:     jktian 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - java
    - project
    - 多进程
---

# 项目内容
java模拟路由表构建
socket
multi-thread
# properties文件读取
Java 开发中，需要将一些易变的配置参数放置再 XML 配置文件或者 properties 配置文件中。然而 XML 配置文件需要通过 DOM 或 SAX 方式解析，而读取 properties 配置文件就比较容易

```
         Properties prop = new Properties();
         String value = null;
         try {
             // 通过输入缓冲流进行读取配置文件
             InputStream InputStream = new BufferedInputStream(new FileInputStream(new File(filePath)));
             // 加载输入流
             prop.load(InputStream);
             // 根据关键字获取value值
		value = prop.getProperty(keyWord);
```
# 文件读写操作
inputstream是filestream的父类
BufferedInputStream和BufferedoutputStream是FilterInputStream和FilterOutputStream的子类，可以避免每次发送或者
写数据的时候，进行实际的写操作，使用的是缓冲区；

不应用缓冲区的时候，每次读取一个字节，写入一个字节，由于操作磁盘比内存慢的很多，所以不应用缓冲区效率很低；
应用缓冲区，可以一次读取多个字节，先不写入磁盘，而是放入内存之中，到了缓冲区大小的时候，在写入磁盘，减少了对磁盘的操作，效率高；
应用缓冲流，在结束的时候，调用flush和close方法，将缓冲区的数据都清理出来，，写入磁盘，否则可能无数据；
InputStreamReader类是从字节流到字符流的桥接器
InputStreamReader(InputStream in, String charsetName)
byteArrayInputStream(byte buf[])
objectStream

# java语言的特点
安全,虚拟机,规范/一板一眼
# hashmap & hashset
HashSet实现了Set接口，它不允许集合中出现重复元素。当我们提到HashSet时，第一件事就是在将对象存储在HashSet之前，要确保重写hashCode（）方法和equals（）方法，这样才能比较对象的值是否相等.HashSet使用成员对象来计算hashcode值对于两个对象来说hashcode可能相同，
所以equals()方法用来判断对象的相等性，如果两个对象不同的话，那么返回false

HashMap实现了Map接口，Map接口对键值对进行映射。Map中不允许出现重复的键（Key）。Map接口有两个基本的实现
TreeMap和HashMap。TreeMap保存了对象的排列次序，而HashMap不能。HashMap可以有空的键值对（Key（null）-Value（null））
HashMap是非线程安全的（非Synchronize），要想实现线程安全，那么需要调用collections类的静态方法synchronizeMap（）实现。
HashMap使用键（Key）计算Hashcode
# 实现serialable接口
实现serializabel接口的作用是就是可以把对象存到字节流，然后可以恢复，所以你想如果你的对象没实现序列化怎么才能进行持久化和网络传输呢，要持久化和网络传输就得转为字节流，所以在分布式应用中及设计数据持久化的场景中，你就得实现序列化
# == & equals() & hashcode()
==直接比较jvm中的内存地址
equals()默认调用==, 可以重载,如string中首先比较内存地址,其次比较字符本身
hashcode()返回32位的jvm内存地址

(1)绑定。当equals方法被重写时，通常有必要重写 hashCode 方法，以维护 hashCode 方法的常规协定，该协定声明相等对象必须具有相等的哈希码。

(2)绑定原因。Hashtable实现一个哈希表，为了成功地在哈希表中存储和检索对象，用作键的对象必须实现 hashCode 方法和 equals 方法。同(1)，必须保证equals相等的对象，hashCode 也相等。因为哈希表通过hashCode检索对象。

(3)默认。

　　==默认比较对象在JVM中的地址。

　　hashCode 默认返回对象在JVM中的存储地址。

　　equal比较对象，默认也是比较对象在JVM中的地址，同==
　　

# 包装类