## LeetCode [188 买卖股票的最佳时机 IV](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/description/)
### 中文版本
相较于仅允许一次交易的情况，本题将交易次数上限扩展为 k 次，但问题本质不变。需要维护的状态包括：天数、交易次数和当前持股状态。

        int n=prices.size();
        int ans=0;
        vector<vector<vector<int>>>dp(n,vector<vector<int>>(k+1,vector<int>(2)));
天数维度可以通过动态规划的逐日递推自然处理，且由于状态仅依赖前一天，因此可以简单转移即可，甚至压缩该维度。

持股状态与交易次数紧密关联。状态转移时，卖出不增加交易计数，买入则需从前一次交易完成后的空仓状态转移，确保每次买入都对应一次有效的交易启动。

交易次数的处理依赖于正确的初始化。由于状态是从 `j-1` 转移而来，而非自动选择最优路径，若不显式初始化，持股状态可能继承默认值 0，导致“免费持股”的逻辑错误。因此，必须在第 0 天将所有 `dp[j][1]` 初始化为 `-prices[0]`，以体现买入成本，保证状态转移的语义正确。

```cpp
dp[i][j][st]=max(dp[i-1][j][st],dp[i-1][_k][st^1]+val);
```

#### 完整代码
```cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        for (int j = 0; j <= k; j++) {
            dp[0][j][0] = 0;
            dp[0][j][1] = -prices[0];
        }

        for(int i=1;i<n;i++){
            for(int j=1;j<=k;j++){
                dp[i][j][0]=max(dp[i-1][j][0],dp[i-1][j][1]+prices[i]);
                dp[i][j][1]=max(dp[i-1][j][1],dp[i-1][j-1][0]-prices[i]);
                ans=max(ans,dp[i][j][0]);
            }
        }

        return ans;
    }
};
```
---
### English Version
Compared to the case with only one allowed transaction, this problem extends the limit to k transactions, but the core idea remains the same. The state to maintain includes: day, number of transactions, and current holding status.

The day dimension can be naturally handled through daily DP recurrence. Since each state depends only on the previous day, it can be simply updated day by day, and this dimension can even be compressed to optimize space.

The holding status is closely tied to the number of transactions. During state transitions, selling does not increase the transaction count, while buying must come from the "not holding" state after completing the (j-1)-th transaction, ensuring each buy starts a valid new transaction.

Proper initialization is crucial for handling transaction counts. Since the state transfers from `j-1` rather than automatically selecting the best path, failing to initialize explicitly may cause the holding state to inherit a default value of 0, leading to the logical error of "getting stock for free." Therefore, on day 0, all `dp[j][1]` values must be initialized to `-prices[0]` to reflect the actual purchase cost and ensure semantic correctness in state transitions.
