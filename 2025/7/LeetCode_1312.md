## LeetCode [1312 让字符串成为回文串的最少插入次数](https://leetcode.cn/problems/minimum-insertion-steps-to-make-a-string-palindrome/description/)
### 中文版本
题目可以转换为求最长回文子序列。因为对于非该序列的字符只能添加字符处理。

#### 完整代码
```cpp
class Solution {
public:
    int minInsertions(string s) {
        int n=s.size();
        vector<vector<int>>dp(n,vector<int>(n));
        for(int l=n-1;l>=0;l--)
        {
            dp[l][l]=1;
            for(int r=l+1;r<n;r++){
                if(s[l]==s[r]){
                    dp[l][r]=dp[l+1][r-1]+2;
                }else{
                    dp[l][r]=max(dp[l+1][r],dp[l][r-1]);
                }
            }
        }

        return n-dp[0][n-1];
        
    }
};
```
---
### English Version
The problem can be transformed into finding the longest palindromic subsequence. This is because characters not in this subsequence can only be handled by adding characters.