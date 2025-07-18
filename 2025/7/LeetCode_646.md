## LeetCode [646 最长数对链](https://leetcode.cn/problems/maximum-length-of-pair-chain/description/)
### 中文版本
对于这样的动态规划题目，首先需要定义状态。

状态定义为以`i`为结尾的最长序列，然后后继状态直接从可扩展的状态中挑选最大的扩展。需要注意的是，这个序列并不受制于原有序列的顺序，所以应当先进行排序。


#### 完整代码
```cpp
class Solution {
public:
    int findLongestChain(vector<vector<int>>& pairs) {
        int n=pairs.size();
        vector<int>dp(n);

        sort(pairs.begin(),pairs.end(),
        [](const vector<int>& A,const vector<int>& B){
            return A[1]<B[1];
        });

        int ans=1;
        dp[0]=1;
        for(int i=1;i<n;i++){
            for(int j=0;j<i;j++){
                if(pairs[j][1]<pairs[i][0]){
                    dp[i]=max(dp[i],dp[j]+1);
                    ans=max(ans,dp[i]);
                }
            }
        }
        return ans;
    }
};
```
---
### English Version
For such a dynamic programming problem, the first step is to define the state.

The state can be defined as the longest sequence ending at index `i`. Then, the subsequent state can be directly selected by extending from the available states. It is important to note that the sequence is not constrained by the original order of the elements, so the array should be sorted first.
