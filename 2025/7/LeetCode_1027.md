## LeetCode [1027 最长等差数列](https://leetcode.cn/problems/longest-arithmetic-subsequence/description/)
### 中文版本
基本可以直接按照题意完成编写。但值得注意的是，如果不想使用`map`而是数组存储的话，考虑到`diff`可能为负数，需要加上一个足够大的偏移值。
#### 完整代码
```cpp
class Solution {
public:
    int longestArithSeqLength(vector<int>& nums) {
        int n = nums.size();
        if (n <= 2) return n;

        vector<unordered_map<int, int>> dp(n);
        int ans = 2;

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < i; j++) {
                int diff = nums[i] - nums[j];
                if(dp[j].count(diff)){
                    dp[i][diff] = dp[j][diff] + 1;
                }else{
                    dp[i][diff]=2;
                }
                
                ans = max(ans, dp[i][diff]);
            }
        }

        return ans;
    }
};
// 每个数都有集中选择：
// 1.尝试加入之前的序列
// 2.加入失败则单独创建序列
// 以val结尾，差是diff的序列
```
---
### English Version
The code can basically be written directly according to the problem description. However, it's worth noting that if you choose to use an array instead of a `map` to store the differences, you should add a sufficiently large offset to the `diff` value, since it could be negative.