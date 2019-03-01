---
layout:     post   				    # 使用的布局（不需要改）
title:      oj-怪盗基德的滑翔翼			# 标题 
subtitle:  	 
date:       2019-03-01				# 时间
author:     jktian 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - oj
    - dp
    - dfs
---

# 问题描述
假设城市中一共有N幢建筑排成一条线，每幢建筑的高度各不相同。初始时，怪盗基德可以在任何一幢建筑的顶端。他可以选择一个方向逃跑，但是不能中途改变方向（因为中森警部会在后面追击）。因为滑翔翼动力装置受损，他只能往下滑行（即：只能从较高的建筑滑翔到较低的建筑）。他希望尽可能多地经过不同建筑的顶部，这样可以减缓下降时的冲击力，减少受伤的可能性。请问，他最多可以经过多少幢不同建筑的顶部（包含初始时的建筑）？


输入
输入数据第一行是一个整数K（K < 100），代表有K组测试数据。 
每组测试数据包含两行：第一行是一个整数N(N < 100)，代表有N幢建筑。第二行包含N个不同的整数，每一个对应一幢建筑的高度h（0 < h < 10000），按照建筑的排列顺序给出。
输出
对于每一组测试数据，输出一行，包含一个整数，代表怪盗基德最多可以经过的建筑数量。

# 解决方案

1. dfs

            #include<iostream>
            #include<cmath>
            #include<string>
            #include<iterator>
            #include<algorithm>
    
            using namespace std;
            /* test-input
                3
                8
                300 207 155 299 298 170 158 65
                8
                65 158 170 298 299 155 207 300
                10
                2 1 3 4 5 6 7 8 9 10
            */
            /* test-output
                6
                6
                9
            */
            int buildings[200][200] = {0};
            int buildTot[200] = {0};
    
            int dfs(int caseIndex, int curBuilding,int pVal, int tot, int inc){
            //    cout << curBuilding << endl;
                if(inc==1 && curBuilding>=buildTot[caseIndex]){
                    return tot;
                }
                if(inc==-1 && curBuilding<0){
                    return tot;
                }
                int curVal = buildings[caseIndex][curBuilding];
                if(curVal<pVal){
                    return max(dfs(caseIndex,curBuilding+inc,pVal, tot, inc),
                               dfs(caseIndex,curBuilding+inc,curVal, tot+1, inc));
                }else{
                    return dfs(caseIndex,curBuilding+inc,pVal, tot, inc);
                }
            }
            int main(){
                // get input
                int caseNum;
                cin >> caseNum;
                for(int i=0;i<caseNum;i++){
                    cin >> buildTot[i];
                    for(int j=0;j<buildTot[i];j++){
                        cin >> buildings[i][j];
                    }
                }
    
                // dfs, two-direction
                for(int i=0;i<caseNum;i++){
                    int res = 0;
                    int f2b=dfs(i,0,10000,0,1), 							b2f=dfs(i,buildTot[i]-1,10000,0,-1);
                //  cout << f2b << ": " << b2f << endl;
                    res = max(res,max(f2b,b2f));
                    cout << "Case" << i << ": " << res << endl;
                }
                return 0;
            }
    1. dp
    
            // i表示最大的建筑下标，用于限制子问题
            // j表示根据i得到的可能倒数第二个建筑下标
            for(i=0;i<n;i++){
            a[i]=1;
            }
            a[0]=1;
            for(i=1;i<n;i++){
            flag=0;
            for(j=0;j<i;j++){
            if(buf[j]>buf[i]&&a[i]<a[j]+1){
            a[i]=a[j]+1;
            if(!flag)
            flag=1;
            }
            }
            if(!flag){
            a[i]=1;
            }
            
            }
            int mx1=*max_element(a,a+n);

# 知识点

1. 可以用dfs做
  1. 确定函数参数，哪些是递归下来的，需要做出改变的，哪些是全局坐标等
  2. 确定递归的退出条件
  3. 确定递归过程/递推公式，一般是分支或max(dfs(),dfs())
2. dp做
3. 其他
> 1. 接受输入后
>    1. 可以动态分配内存
>    2. 或者初始化几个很大的全0数组, 然后按需置１
> 2. 整个流程
>    1. 可以全部接受输入并存储（很多测试案例）后，统一处理
>    2. 或者在循环中，每接受一个测试案例，处理一个