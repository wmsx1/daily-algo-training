## LeetCode [714 买卖股票的最佳时机含手续费](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/description/)
### 中文版本
因为数据限制只能把复杂度降为$O(n)$，为此需要额外添加状态表示买入情况，剩余的根据题意描述即可。

#### 完整代码
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n=prices.size();
        vector<vector<int>>dp(n,vector<int>(2));
        dp[0][0]=0;
        dp[0][1]=-prices[0];
        for(int i=1;i<n;i++){
            dp[i][0]=max(dp[i-1][0],dp[i-1][1]+prices[i]-fee);
            dp[i][1]=max(dp[i-1][1],dp[i-1][0]-prices[i]);
        }

        return dp[n-1][0];
    }
};

// dp[i][state] 第i天的最大利润，state为1表示持有
```
---
### English Version
Because of data constraints, we can only reduce the time complexity to $O(n)$. To achieve this, we need to introduce an additional state to represent the situation where we have bought the stock. The rest follows directly from the problem description.