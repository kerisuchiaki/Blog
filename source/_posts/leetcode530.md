---
title: leetcode530二叉搜索树的最小绝对值
date: 2024-04-14 20:08:19
tags: leetcode
---

## 题目

给你一个二叉搜索树的根节点 `root` ，返回 **树中任意两不同节点值之间的最小差值** 。

差值是一个正数，其数值等于两值之差的绝对值。

## 分析

做这种题，我们需要知道二叉搜索树的一个特性，即中序遍历的结果是有序升序的数组，那么求书中最小的两个节点的差值最小显然是中序遍历的数组的相邻的两个元素，毕竟在树中就是一个节点的左子树最右边和右子树最左边是和节点差值最小的，而中序遍历的特点就是先处理左子树，再梳理节点，最后在处理右子树，当处理完左子树时，除了最左边元素没有上一个元素，其它元素都有，用一个变量pre记录处理左子树后上一个处理元素，即可计算上一个元素与当前节点的差值，每次计算完差值就更新pre，重复上述步骤即可

<!-- more -->

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int pre=-1,minx=10000000;
    int getMinimumDifference(TreeNode* root) {
       dfs(root);
       return minx;
    };
    void dfs(TreeNode* root){
        if(root==nullptr)return ;
        dfs(root->left);
        if(pre!=-1){
            int dis=root->val-pre;
            minx=minx<dis?minx:dis;
        };
        pre=root->val;
        dfs(root->right);
    }
};
```

