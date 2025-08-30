## LeetCode [102 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/description/)
### 中文版本
层序遍历有多种方法，这里使用了直接的方法，即递归合并。另外，在编写时，遇到了`size_t`负溢出的问题。

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
    void merge(vector<int>& ans,vector<int>& nums){
        for(auto it:nums){
            ans.push_back(it);
        }
    }
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>>ans;
        if(!root)return ans;
        ans.push_back({root->val});
        vector<vector<int>> ans_left=levelOrder(root->left);
        vector<vector<int>> ans_right=levelOrder(root->right);

        for(int i=1;i<=max(ans_right.size(),ans_left.size());i++){
            ans.push_back({});
        }

        for(int i=0;i<ans_left.size();i++){
            merge(ans[i+1],ans_left[i]);
        }
        
        for(int i=0;i<ans_right.size();i++){
            merge(ans[i+1],ans_right[i]);
        }

        return ans;
    }
};
```
---
### English Version
Level-order traversal can be implemented in various ways. Here, we use a direct approach, namely recursive merging. Additionally, during implementation, we encountered the issue of `size_t` underflow when dealing with negative values.