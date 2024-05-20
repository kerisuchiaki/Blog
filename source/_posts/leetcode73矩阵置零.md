---
title: leetcode73矩阵置零
date: 2024-03-15 22:51:47
tags: leetcode题解
---

## [73. 矩阵置零](https://leetcode.cn/problems/set-matrix-zeroes/)



给定一个矩阵，若其中一个元素为零，则将其余行和列的元素都置为零





 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

```
输入：matrix = [[1,1,1],[1,0,1],[1,1,1]]
输出：[[1,0,1],[0,0,0],[1,0,1]]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

```
输入：matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
输出：[[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```

 

**提示：**

- `m == matrix.length`
- `n == matrix[0].length`
- `1 <= m, n <= 200`
- `-231 <= matrix[i][j] <= 231 - 1`

## 题解代码

时间复杂度，显然必须要遍历每一个元素，那么复杂度就是O(m*n)了；

空间复杂度一定是矩阵的大小了,可以优化的也就只有额外的空间，显然的思路就是使用一个标记矩阵记录，可以复制原先矩阵元素的大小，显示遍历一次当我们的举证元素为零时，记为零，但我们第二次遍历时，直接和这个标记矩阵做对比，或者做异或运算就可以将原先举证置为零，空间是就是两倍的矩阵大小

```c++
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        int m=matrix.size();
        int n=matrix[0].size();
        vector<int> a(m),b(n);
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==0){
                    a[i]=1;b[j]=1;                    
                }
            }
        }
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(a[i]!=0||b[j]!=0)matrix[i][j]=0;
            }
        }
    }
};
```

