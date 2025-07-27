## LeetCode [115 不同的子序列](https://leetcode.cn/problems/distinct-subsequences/description/)
### 中文版本
经典的背包模型，在选和不选中转移。解答中使用了加空前缀的技巧避免处理边界问题。
#### 完整代码
```cpp
class Solution {
public:
    int numDistinct(string s, string t) {
        int n=s.size(),m=t.size();
        s=" "+s;
        t=" "+t;
        vector<vector<unsigned long long>>dp(n+1,vector<unsigned long long>(m+1));
        for(int i=0;i<=n;i++){
            dp[i][0]=1;
        }

        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                dp[i][j]=dp[i-1][j];
                if(s[i]==t[j]){
                    dp[i][j]=dp[i][j]+dp[i-1][j-1];
                }
            }
        }
        return dp[n][m];
    }
};
//str1 str2
//匹配
//跳过当前字符
//或者加上匹配
```
---
### English Version
This is a classic knapsack dynamic programming model, where the transition is based on choosing or not choosing an item. The solution uses a technique of adding a virtual prefix to avoid handling edge cases.