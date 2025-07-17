## LeetCode [2466 统计构造好字符串的方案数](https://leetcode.cn/problems/count-ways-to-build-good-strings/description/)
### 中文版本
对于这样的动态规划题目，首先需要定义状态。

把字符串长度作为状态，根据添加的不同字符扩展当前状态：
```cpp
dp[i] 长度为 i 的字符串
dp[i]=dp[i-zero]+dp[i-one]
```
#### 完整代码
```cpp
class Solution {
public:
    int countGoodStrings(int low, int high, int zero, int one) {
        int n=high;
        const int MOD=1e9+7;
        vector<long long>dp(n+1);
        dp[0]=1;
        for(int i=1;i<=n;i++){
            if(i-zero>=0){
                dp[i]=(dp[i]+dp[i-zero])%MOD;
            }
            if(i-one>=0){
                dp[i]=(dp[i]+dp[i-one])%MOD;
            }
        }
        
        long long ans=0;
        for(int i=low;i<=high;i++){
            ans=(ans+dp[i])%MOD;
        }
        return ans;
    }
};
```
---
### English Version
For such a dynamic programming problem, the first step is to define the state.

Use the length of the string as the state, and extend the current state based on the addition of different characters:
```cpp
dp[i]  // the number of valid strings of length i
dp[i] = dp[i - zero] + dp[i - one]
```
Here, `zero` and `one` represent the lengths of the binary substrings (such as "0" or "1") being added, depending on the specific problem. This recurrence relation captures all valid ways to form a string of length `i` by appending these substrings.
