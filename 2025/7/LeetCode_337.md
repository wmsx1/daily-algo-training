## LeetCode [337 打家劫舍 III](https://leetcode.cn/problems/house-robber-iii/description/)
### 中文版本
模拟即可。从数据估计直接递归会导致爆栈，所以使用了记忆化。

#### 完整代码
```cpp
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
    unordered_map<TreeNode*,pair<int,int>>mem;
    int robSuper(TreeNode* root,bool isVisit) {//当前节点的父节点是否被访问
        if(!root)return 0;
        if(mem.count(root)){
            if(isVisit){
                return mem[root].first;
            }else{
                return mem[root].second;
            }
        }

        int ans=robSuper(root->left,false)+robSuper(root->right,false);
        mem[root].first=ans;
        if(!isVisit){
            ans=max(ans,
            root->val+robSuper(root->left,true)+robSuper(root->right,true));
            mem[root].second=ans;
        }
        return ans;
    }
    int rob(TreeNode* root) {
        return robSuper(root,false);
    }
};
```
---
### English Version
Simulation is sufficient. From the data, it can be seen that direct recursion would lead to a stack overflow, so memoization is used.