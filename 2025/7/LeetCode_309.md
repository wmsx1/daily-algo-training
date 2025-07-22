## LeetCode [309 买卖股票的最佳时机含冷冻期](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/)
### 中文版本
动态规划，定义状态即可。因为涉及到冷冻期，增加了附加状态描述在某一天的卖出情况。

#### 完整代码
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n=prices.size();
        vector<vector<int>>dp(n,vector<int>(2));
        for(int i=1;i<n;i++){
            for(int j=0;j<i;j++){//买入第j天,并在第i天卖出
                int val=dp[max(j-1,0)][0]+prices[i]-prices[j];
                dp[i][1]=max(dp[i][1],val);
            }
            dp[i][0]=max(dp[i-1][0],dp[i-1][1]);
        }
        return max(dp[n-1][0],dp[n-1][1]);
    }
};
// dp[i][state] 第i天的最大利润,state为1表示卖出
// dp[i]=dp[j]+delta(i,j)
```
---
### English Version
Dynamic Programming: Simply define the states. Since there is a "cooldown" period involved, we introduce additional state descriptions to track the selling status on a given day.