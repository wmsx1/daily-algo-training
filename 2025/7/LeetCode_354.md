## LeetCode [354 俄罗斯套娃信封问题](https://leetcode.cn/problems/russian-doll-envelopes/description/)
### 中文版本
两个维度的`LIS`问题。通过排序可以减少一个维度，然后为了降低时间复杂度，考虑使用二分查找。为此，有方法耐心排序可以使用二分查找的方式，快速插入构建出最长递增子序列。
#### 完整代码
```cpp
class Solution {
public:
    int getLIS(vector<int>& nums){
        vector<int> top;

        for(auto val:nums){
            auto cur=lower_bound(top.begin(),top.end(),val);
            if(cur==top.end()){
                top.push_back(val);
            }else{
                *cur=val;
            }
        }
        return top.size();
    }
    int maxEnvelopes(vector<vector<int>>& envelopes) {
        int n=envelopes.size();
        sort(envelopes.begin(),envelopes.end(),[](const auto& A,const auto& B){
            if(A[0]==B[0]){
                return A[1]>B[1];
            }return A[0]<B[0];
        });

        vector<int>nums;
        for(int i=0;i<n;i++){
            nums.push_back(envelopes[i][1]);
        }
        
        return getLIS(nums);
    }
};
```
---
### English Version
A two-dimensional Longest Increasing Subsequence (LIS) problem. By sorting, one dimension can be eliminated, and then, to reduce time complexity, binary search is considered. For this purpose, the "Patience Sorting" method can be used, which leverages binary search to efficiently insert elements and construct the longest increasing subsequence.