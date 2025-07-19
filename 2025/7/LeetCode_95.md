## LeetCode [95 不同的二叉搜索树 II](https://leetcode.cn/problems/unique-binary-search-trees-ii/description/)
### 中文版本
根据数据范围，按照题意递归即可完成。

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
    vector<TreeNode*> buildTree(int l,int r){
        if(l>r)return {nullptr};

        vector<TreeNode*> lsons;
        vector<TreeNode*> rsons;
        vector<TreeNode*> ans;
        for(int i=l;i<=r;i++){
            lsons=buildTree(l,i-1);
            rsons=buildTree(i+1,r);
            for(auto lson:lsons){
                for(auto rson:rsons){
                    ans.push_back(new TreeNode(i,lson,rson));
                }
            }
        }
        return ans;
    }
    vector<TreeNode*> generateTrees(int n) {
        return buildTree(1,n);
    }
};
```
---
### English Version
Simply perform recursion according to the problem's requirements and within the given data range.