---
title: dfs求全排列
date: 2024-08-24 22:55:05
tags: 算法
---

# 全排列

记录一下求全排列的算法，有三种，交换，插空，枚举

## 第一种 交换

<!-- more -->

这是常见的一种求全排列的dfs算法,经常在各种算法书籍上看到，简单的描述下就是假如n个元素的排列就是一种排列方式的话，那么将第一个元素和其它元素交换得到也是新的排列，即只要第一个元素不一样那么剩下的怎么排列都是不一样的，然后递归求剩下的元素的全排列即可

```c++
// 代码还挺简洁的
void permute(vector<int> nums,int start,vector<vector<int>> res){
    if(start==nums.end()){
      res.push_back(nums);
        return;
    };
    for(int i=start;i<nums.size();++){
        swap(nums[i],nums[start]);
        permute(nums,start+1,res);
        swap(nums[i],nums[start]);
    };
}
```

## 第二种 高中的插空法

在高中，我们都学过怎么求全排列，其中一种方法就是插空法，即把一个元素插入到已将排列好的序列的中间，那么每一种插入的位置都会形成一个新的排列，只要求出剩下元素的所有全排列然后再将第一个元素插入得到所有全排列中的位置就行

### 思路来源

这个想法我是怎么得到的呢，我并不是直接从高中数学中得到的，而是用递归的想法想到的，怎么求一个序列的全排列，直接想有点难度，使用分治的思想进行递归，长度为n的序列全排列可以先求出长度为n-1的序列的全排列，即先不考虑第一个元素，把剩下的元素全排列求出来后，再把第一个元素插入到这个n-1个元素形成的全排列的位置中，那么就可以得到长度为n的全排列，很符合递归分治的思想，分而治之，将问题规模逐渐减少到最小的维度，然后只需要具体思考这个最小的问题即可，思维难度小，妙啊，后来想想这不就是高中的插空法嘛

```c++
// 定义permute求nums数组的start到end的元素的全排列并返回
vector<vector<int>> permute(vector<int> & nums,int begin,int end){
    vector<vector<int>> res,ans;
    if(end-begin==1){
        vector<int> tmp;
        tmp.push_back(nums[begin]);
        ans.push_back(tmp);
        return ans;
    }
    /*
    求begin到end的全排列等价于求begin+1到end的全排列然后让索引begin处的元素插入begin+1到end元素之间的位置，
    那么每个这样的排列都是一个新的全排列,
    也就是高中数学求排列的的插空法
    */
    res=permute(nums,begin+1,end);
    for(int i=0;i<res.size();i++){
        for(int j=0;j<=res[i].size();j++){
            vector<int> tmp;
            for(int k=0;k<res[i].size();k++){
                tmp.push_back(res[i][k]);
            };
            tmp.insert(tmp.begin()+j,nums[begin]);
            ans.push_back(tmp);
        };
    };
    return ans;
};
```

## 第三种 普通人能想到的枚举

为什么这是普通人想到的算法，应为我从之前接触到的求全排列算法中打印它们的全排列序列总是和我想得到不一样，我一直以为交换得到全排列的序列是

```
1 2 3 4
1 2 4 3
1 3 2 4
1 3 4 2
1 4 2 3
1 4 3 2
2 1 3 4
2 1 4 3
....
```

然而他的结果是

```
1 2 3 4 
1 2 4 3
1 3 2 4
1 3 4 2
1 4 3 2 // 奇怪的地方没按字典序  //原因在于1 2 3 4中 2与4交换 形成 1 4 3 2
1 4 2 3 // 与上逆序
2 1 3 4
2 1 4 3
2 3 1 4
2 3 4 1
2 4 3 1 //
2 4 1 3 //与上逆序            //原因在于2   1 3 4中 1与4交换形成 2 4 3 1
3 2 1 4  //
3 2 4 1 //
3 1 2 4
3 1 4 2// 第二个元素就逆序了			//原因在于 1 2 3 4中 1 3交换使得形成 3 2 1 4
3 4 1 2
3 4 2 1
4 2 3 1 //							//原因在于1 2 3 4 1 和 4交换出现 4 2 3 1
4 2 1 3 //与上逆序					//
4 3 2 1 //
4 3 1 2 //与上逆序
4 1 3 2 //
4 1 2 3 //与上逆序
```

这个序列不是很符合第一个普通人想的，普通人就是从所有元素中选则来生成序列，比如第一个元素的选择可以有4中。然后第二个元素的选择就只能有剩下的三种，第三个元素就只能有两种选择，最后一个就只能有一种选择了，那么基于这个想法就可以得到新的生成全排列算法而且序列就是符合正常人想的

```c++
//这里原始序列也充当可选元素集合
vector<vertoc<int>> permute(vector<int> nums){
    if(nums.size()==0){
        vector<vector<int>> res(1);
        return res;
    }
    vector<vector<int>> res;
    for(int i=0;i<nums.size();i++){
    	//选择一个元素，减少可选元素集合，然后递归剩下的元素集合
        int selectNum=nums[i];
        nums.erase(nums.begin()+i);
        vector<vector<int>> ans=permute(nums);
        for(int j=0;j<ans.size();j++){
            // 添加回到递归的集合
				ans[j].insert(ans[j].begin(),selectNum);
            res.push_back(ans[j]);
        };
        //回溯
        nums.insert(nums.begin()+i,selecrNum);
    };
    return res;
}
```



会这么想只要还是傻逼老师出在pta的题目中使用dfs求全排列的题目只有一个测试点并且答案还是只能是使用交换的这种，这使得有多个符合条件的答案只能其中一个序列，那么我是用其它的求全排列的算法得到的排列恰好不是和答案一样的（测试样例通过但是后台不是测试样样例，问老师老师也是直接说这个测试用例就是后台样例，那么为什么直接输出结果相同都错误，我怀疑是老师根本不知道，题目都不知道从哪个学校弄来的），但是题目要求的结果即输出的结果是一样的，然而提交总是不通过，后来研究网上的通过代码才发现这个问题
