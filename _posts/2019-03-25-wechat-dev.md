---

layout:     post   				    # 使用的布局（不需要改）
title:      微信小程序开发			# 标题 
subtitle:  	 
date:       2019-04-15				# 时间
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
[项目地址](https://github.com/ixneo/kaoyanshuo)
[后端详细文档](https://github.com/ixneo/kaoyanshuo/doc/back-front-introduce)

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


# LOG
20190409
---
### 知识点
1. input标签可以指定类型，有默认类型
2. 逐步排除错误
3. 区分
	- this.data.value_name
	- e.details.value
4. 多线程模型
	在访问数据库时，success之后的操作，要写在**回调函数**中，避免操作顺序不一致，出现玄学错误

### 初步设计
##### 前端
- [ ] 首页的论坛
	- [ ] 列表项展示条目．条目包含：头像昵称，摘要，点赞数
	- [ ] 滚动加载 
	- [ ] 搜索：根据标签，内容．高亮符合数据．**查询帖子表**
	- [ ] 发帖：**更新帖子表，更新个人信息表**
	- [ ] 点赞等对帖子的操作．**更新个人信息表**
- [ ]  资源仓库
	- [ ]  直接写死
	- [ ]  提供下载和上传服务
- [ ]  我的
	- [ ] 反馈信息，收集个人信息，上传头像图片等．**更新个人信息表**
##### 后端

- [ ]  collections
	- [ ] 帖子表(posts):: 帖子id(post_id), 发帖人的id(id_user),　帖子摘要，帖子内容，tag, 赞同数，评论数，发帖时间
	- [ ] 个人信息表．用户id, 性别，昵称，头像，学校，专业，发过的帖子id, 跟过的帖子id, 点赞过的帖子id(用于推荐), 收藏的帖子id
	- [ ] 反馈信息表．反馈id, 用户id, 反馈内容，反馈时间
	- [ ] 资源表．资源id,　资源文件（pdf/xlsx等）
	- [ ] 跟帖表．跟帖id, 主帖id, 跟帖时间，跟帖人，跟帖内容．
- 实际设计
1. posts表：包含帖子内容，每个帖子中包含follow_posts数组（显示跟帖信息）
2. person表：我点赞过的帖子
```
 // posts表
{
    "user_id": 2,
    "user_name": "jk.tian",
    "user_head": "../../images/icon1.jpeg",
    "post_brief": "考研的时候怎么查找资料",
    "post_content": "给学姐学长发红包",
    "post_tags": ["红包","资料","方法"],
    "like_count": 3,
    "follow_count": 2,
    "follow_posts": [
        {"user_id": 1,"user_name": "wangZY","user_head": "../../images/icon1.jpeg","follow_content": "+1"},
        {"user_id": 2,"user_name": "wangZY","user_head": "../../images/icon1.jpeg","follow_content": "朱门酒肉臭路有冻死骨"}
    ]
}

// person表
相当于posts表中某一行，加上了owner字段（标识点赞人）
```

20190411
---
### DONE
1. 查询循环展示：（跟帖写循环，**跳转页面传数据**）
	1. post
	2. follow-posts
	3. tags
```
// 跟帖. 传一个item, 找到跳转按钮
// page_from
  buttonListener:function(){
    var that = this
    wx.navigateTo({
      url: '/pages/test2/test2?nameData=' + that.data.name + '&ageData=' + that.data.age
    })
  }
  let str=JSON.stringify(e.currentTarget.dataset.item);
wx.navigateTo({
url: '../toMybaby/babyDetail/babyDetail?jsonStr='+str,

// page_to  
      onLoad:function(options){
    // 生命周期函数--监听页面加载
    let item=JSON.parse(options.jsonStr);
    this.setData({ward:item});
  },
```
2. 点赞/关注／跟帖
```
// 更新posts
// 存储当前post
  update_post: function (e) {
    var id = post._id;
    var cfollow_posts = post.follow_posts;
    cfollow_posts.push({,});
    const db = wx.cloud.database();

    db.collection(posts').where({
      "_id": id,
    })
    .update({
        data: {
          follow_posts: cfollow_posts;
          like_count: post.like_count+1,
          
        },
      });

// 在查询我点赞过的文章时，
// 方案一：　直接遍历post
// 方案二：　冗余存储我的表中，点赞过的文章
```
> 由于云数据库的权限问题，决定全部迁移到云函数
2. 搜索（只提供文本搜索）
```
// 一个新的，但是类似论坛的页面，目的：存储不同的帖子列表数据
```

6. 个人信息更改：更改
> 注意数据库的权限，否则会访问成功但无返回数据
> 微信云开发用的是NoSQL. 所以图片要么云端存路径，要么本地随机抽取

### TODO
1. 个人信息表，存openid, 点赞过的文章列表，和我的点赞(页面类似论坛)对接，
    1. 头像，昵称存**本地**，更改也在本地。每次开启读本地数据
2. 资源tab
##### 妥协
 采用很多冗余page的原因，每一个page有自己专属的json-data
##### 待解决
- 帖子头像存在哪里。利用云函数，存储路径
- 权限管理
- 数据都要存到云端。因为代码有大小限制
##### 进步空间
改用jsp, 解决高并发，数据一致性问题


 ### FINAL
 1. 数据库权限问题：从云数据库迁移到云函数
 2. 云函数对日期类型的支持问题：在前端将json-date变为string, 在后端将string变为json-date. 放弃时间的存储
 3. 每个用户对某个特定帖子的点赞和跟帖是有限制的
 4. 很多用户的异常操作没有考虑
 5. 函数式编程语言，就是无法确定执行顺序，只是映射，所以很少考虑异步问题，但对于机器来说，顺序问题又是真实存在的，所以函数式语言适合人写
 6. 高亮搜索词
 7. 针对广大用户的产品：就是一点一点打磨出来的
 	1. 做最小可行性产品，逐段debug

20190412
---
### DONE
- 论坛界面和后端的连接
　　　　- 直接编写json文件，然后上传到云开发中即可
- 某一帖子的界面．和后端的连接
　　　　- 此界面下，关注代表点赞，跟帖代表新回答．点击后对应数字会变，和后端连接
- 搜索界面和后端的连接．
　　　　- 支持搜索内容，摘要，标签，发帖人姓名．未区分，未排名

### TODO
1. 发帖和跟帖
1. 我的点赞，我的回答
2. 资源界面．下载上传
3. 个人信息反馈界面
4. 论坛界面的更新问题
> - 页面之间要少耦合．耦合应该在单个页面和数据库后端之间
> - 明确page和app的生命周期，栈
> - 按钮点击: 先捕获，再冒泡
>   -由于js中作用域的问题，this指针记得改名，以区分作用域．　var that=this;
> - 点赞后返回慢，是因为建立了多次网络连接，是代码的问题
> - 要学会利用缓存，加快加载速度，提高用户体验

###### 我的收藏
```
    wx.getUserInfo({
      success(res) {
        const userInfo = res.userInfo
        const nickName = userInfo.nickName

        db.collection('person').where({
          owner: nickName,
        })
          .get({
            success(res) {
            // res.data 是包含以上定义的两条记录的数组
              console.log(res.data)
            }
          });

      }
    });
```

20190413
---
### DONE
1. 发帖和跟帖．和后端的连接
2. 我的点赞，我的回答中可看见历史记录
3. 资源界面


20190414
---
### DONE
1. 解决刷新问题．去除刷新特效
2. 解决具体帖子的标签显示问题．将text标签换为label
3. 在同一时刻，同一主帖下，点赞／关注的变灰效果，以及加减1
1. 发帖／跟帖后自动返回页面
2. 加入新帖子之后的搜索正常，关注新帖子后，也可在我的收藏中看到
	1. 解决办法：person数据库的插入问题．在调用云函数之前，删除json的_id和_openid字段
3. 对同一个帖子，在不同时刻，多次点赞，会当成对多个帖子的第一次点赞处理
	1. 相当于快照，因为我的收藏中保存的是点赞当时的状态（包括当时的点赞数）
4. 添加邀请功能
5. 搜索：点击右上角的搜索图标／输入搜索词后直接回车
6. 每个主帖下边的跟帖，按照时间顺序，最新的在最下边

### FINAL
1. 出现了posts和person两个表的不一致性．
	1. person表会冻结当时的点赞数．但是通过此途径进入具体的帖子，仍然会显示当前点赞数
2. 重新进入某个帖子时，关注按钮又变得可点击了．
	1. 解决：让点击次数成为page的变量，而不是全局变量（每次show都会刷新）
1. 发帖后自动返回页面
2. 加入新帖子之后的搜索正常，关注后无法在我的中显示
	1. person数据库的插入问题．在调用云函数之前，删除json的_id和_openid字段
3. 对同一个帖子，在不同时刻，多次点赞，会当成对多个帖子的第一次点赞处理
	1. 相当于快照，因为我的收藏中保存的是点赞当时的状态（包括当时的点赞数）