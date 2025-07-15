## LeetCode [983 最低票价](https://leetcode.cn/problems/minimum-cost-for-tickets/description/)
### 中文版本
对于这样的动态规划题目，首先需要定义状态。

在一开始，想当然地把日期 `i` 和使用的通行证种类 `j` 作为状态 `dp[i][j]`。但稍加思考后发现，这种定义无法表达通行证的起始使用时间。因此，我重新设计了状态如下：
```cpp
dp[n] 第i天，花费的价格
if(第i天需要旅游)
    dp[i]=dp[i-1]+costs[0] or dp[i-7]+costs[1] or dp[i-30]+costs[2];
else dp[i] = dp[i - 1];  //继承上一天
```
通过这种方式，我们能够正确地完成状态转移。值得一提的是，通行证是可以从“负数”天开始买的，即长期通行证（如7天或30天）可能在旅行开始前几天就已经购买，就像购买短期通行证一样。在状态转移时，我们需要使用 `max(i - 7, 0)` 或 `max(i - 30, 0)` 来避免数组越界。

#### 完整代码
```cpp
class Solution {
public:
    int mincostTickets(vector<int>& days, vector<int>& costs) {
        int n=days[days.size()-1];
        vector<int>dp(n+1);
        int cur=0;
        for(int i=1;i<=n;i++){
            if(i==days[cur]){
                cur++;
                dp[i]=dp[i-1]+costs[0];
                dp[i]=min(dp[i],dp[max(i-7,0)]+costs[1]);
                dp[i]=min(dp[i],dp[max(i-30,0)]+costs[2]);
            }else{
                dp[i]=dp[i-1];
            }
        }
        return dp[n];
    }
};
```
---
### English Version
For this type of dynamic programming problem, the first step is to define the state clearly.

Initially, the state `dp[i][j]` represents the cost on day `i`  using pass type `j`.However, this definition does not capture when the pass was originally purchased.Therefore, new state is redesigned as follows:
```cpp
dp[i] represents the minimum cost up to day i.
If day i is a travel day:
    dp[i] = min(dp[i - 1] + costs[0], dp[i - 7] + costs[1], dp[i - 30] + costs[2]);
Else:
    dp[i] = dp[i - 1];  // Same as the previous day
```

This way, we can perform the correct state transition. It's also worth noting that passes can be "bought in advance". Since longer-term passes might be more cost-effective, we can buy a 7-day pass even if we only start using it a few days later. Thus, we use `max(i - 7, 0)` or `max(i - 30, 0)` to avoid index out of bounds.