## LeetCode [91 解码方法](https://leetcode.cn/problems/decode-ways/description/)
### 中文版本
对于这样的动态规划题目，首先需要定义状态。

自然地，状态只需要包含已经完成解码的方案数即可，对于当前的字符可以考虑单独解码，也可以考虑和上一个字符组合解码。但需要注意的是，如果上一个字符也是和上一个字符组合解码，则只能选择单独解码，为此还需要保留一个状态表示当前字符是单独解码的结果还是组合解码的结果：
```cpp
str->dp
dp[i][st] 长度为i的字符串解码结果,st为1表示组合
dp[i][0]=dp[i-1][0]+dp[i-1][1] //i 单独解码
dp[i][1]=dp[i-1][0] //i-1 和 i 解码，条件是合法
```

#### 完整代码
```cpp
class Solution {
public:
    bool isInRange(char a,char b){
        int num=(a-'0')*10+(b-'0');
        return num>0 && num<=26;
    }
    int numDecodings(string s) {
        int n=s.size();
        vector<vector<int>>dp(n,vector<int>(2));
        if(s[0]=='0')return 0;
        dp[0][0]=1;//第二个参数表示组合，0 表示否
        for(int i=1;i<n;i++){
            if(s[i]=='0'){
                if(s[i-1]!='1' && s[i-1]!='2'){
                    return 0;
                }else{
                    dp[i][1]=dp[i-1][0];
                }
            }else{
                dp[i][0]=dp[i-1][0]+dp[i-1][1];
                if(isInRange(s[i-1],s[i])){
                    dp[i][1]=dp[i-1][0];
                }
            }
        }
        return dp[n-1][0]+dp[n-1][1];
    }
};
```
---
### English Version
State definition is a crucial part of dynamic programming problems.

Naturally, the state should represent the number of ways to decode the string up to a certain position.At each position, we can consider the current character individually, or combining it with the previous character as a two-digit number.However, note that if the previous character was already used in a combination, we cannot reuse it. Therefore, we need to maintain two states: one representing the number of ways where the current character is decoded individually, and another where it is part of a combined decoding with the previous character:
```cpp
str->dp
dp[i][p] represents the number of decoding ways for a string of length i, where p=1 means the i-th character is part of a combination.
dp[i][0] = dp[i-1][0] + dp[i-1][1] // decode current character individually
dp[i][1] = dp[i-1][0] // combine current character with previous one, only if the combination is valid
```
