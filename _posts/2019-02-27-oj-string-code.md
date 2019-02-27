---
layout:     post   				    # 使用的布局（不需要改）
title:      oj-行程长度编码			# 标题 
subtitle:  	 
date:       2019-02-27				# 时间
author:     jktian 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - oj
---
# 题目描述
总时间限制:  1000ms  内存限制:  65536kB
描述
在数据压缩中，一个常用的方法是行程长度编码压缩。对于一个待压缩的字符串，我们可以依次记录每个字符及重复的次数。例如，待压缩的字符串为"aaabbbbcbb"，压缩结果为(a,3)(b,4)(c,1)(b,2)。这种压缩对于相邻数据重复较多的情况有效，如果重复状况较少，则压缩的效率较低。
现要求根据输入的字符串，首先将字符串中所有大写字母转化为小写字母，然后将字符串进行压缩。
输入
一个字符串，长度大于0，且不超过1000，全部由大写或小写字母组成。
输出
输出为编码之后的字符串，形式为：(a,3)(b,4)(c,1)(d,2)，即每对括号内分别为小写字符及重复的次数，不含任何空格。
样例输入
aAABBbBCCCaaaaa
样例输出
(a,3)(b,4)(c,3)(a,5)

# 题解
    #include<iostream>
    #include<cmath>
    #include<string>
    #include<iterator>
    
    // 行程长度编码
    using namespace std;
    
    string l2g(string s){
        for(auto it=s.begin();it!=s.end();it++){
            if(*it>='a' && *it<='z'){
                *it -= 32;
            }
        }
        return s;
    }
    
    string showLenCode(string s){
        int len = 1,i=0;
        string res;
        for(i=0;i<s.size();i++){
            if(s[i+1]==s[i]){
                len++;
            }else{
                // 重点关注，不能是: res+＝...
                res = res + '('+s[i]+','+(char)(len+'0')+')';
                len = 1;
            }
        }
        return res;
    }
    
    int main(){
        // get input
        string s;
        cin >> s;
    
        // low-letter to high-letter
        s = l2g(s);
    
        // statics
        string res;
        res = showLenCode(s);
        cout << res << endl;
        return 0;
    }

#　重难点
1. 先写注释，搭建基本框架，然后写对应的函数。控制复杂度
2. 小写字母的ascii的编码比大写字母大32
3. 字符串的拼接和格式化。<str> = <str> +... , 不能是<str>+=...
