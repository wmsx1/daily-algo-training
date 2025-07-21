## LeetCode [124 二叉树中的最大路径和](https://leetcode.cn/problems/binary-tree-maximum-path-sum/description/)
### 中文版本
放弃思考，模拟了各类情况，实际就是根节点，左右字节点的抉择问题。

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
    int ans=-1001;
    unordered_map<TreeNode*,int>mem;

    int maxPathSumSuper(TreeNode* root) {
        if(!root)return -1001;
        if(mem.count(root))return mem[root];

        int val_left=maxPathSumSuper(root->left);
        int val_right=maxPathSumSuper(root->right);
        ans=max(ans,root->val+val_left+val_right);
        ans=max(ans,max(val_left,val_right));
        
        mem[root]=max(root->val,root->val+max(val_left,val_right));
        return mem[root];
    }
    int maxPathSum(TreeNode* root) {
        return max(ans,maxPathSumSuper(root));
    }
};
// ans->left+root+right
// return root+max(left,right)
```
---
### English Version
Give up thinking, simulated various situations, in fact, it's just a problem of choosing the root node, left and right child nodes.