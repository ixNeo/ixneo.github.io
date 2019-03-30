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

[项目地址](https://github.com/ixneo/exam_tub)

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

# 开发工具／语言
标签，属性名（无引号），属性值（引号），　if/for可以作为wx:if，即标签的属性名存在
{{}}表示变量，中间可以有布尔判断
pages文件夹表示页面，每个页面有对应的三件套
app表示全局设置
data字段表示数据，以json格式
json中的key和value都要引号

ECMAScript是一种由Ecma国际通过ECMA-262标准化的脚本程序设计语言， JavaScript 是 ECMAScript 的一种实现

浏览器中的JavaScript 是由 ECMAScript 和 BOM（浏览器对象模型）以及 DOM（文档对象模型）组成的，Web前端开发者会很熟悉这两个对象模型，它使得开发者可以去操作浏览器的一些表现，比如修改URL、修改页面呈现、记录数据等等。

NodeJS中的JavaScript 是由 ECMAScript 和 NPM以及Native模块组成，NodeJS的开发者会非常熟悉 NPM 的包管理系统，通过各种拓展包来快速的实现一些功能，同时通过使用一些原生的模块例如 FS、HTTP、OS等等来拥有一些语言本身所不具有的能力。

小程序中的 JavaScript 是由ECMAScript 以及小程序框架和小程序 API 来实现的。同浏览器中的JavaScript 相比没有 BOM 以及 DOM 对象，所以类似 JQuery、Zepto这种浏览器类库是无法在小程序中运行起来的，同样的缺少 Native 模块和NPM包管理的机制，小程序中无法加载原生库，也无法直接使用大部分的 NPM 包。

引入模块
局部变量和全局变量

# 开发日志
20190330
---
- [ ] 搜索页面
	- [ ]　数据库保存结果
	- [x]　向数据库添加数据 
	- [ ]　向数据库查询数据 
	- [ ]　列表形式展示文章
	- [ ]　搜索算法
- [ ] 最新最热页面
- [ ] 具体文章页面
- [ ] 发帖页面
- [ ] 我的页面

# problem
### 宗旨
input要指定类型（不需要）
逐步排除错误

### 区分
this.data.value_name
e.details.value

### 多线程模型
在访问数据库时，success之后的操作，要写在**回调函数**中，避免操作顺序不一致，出现玄学错误
