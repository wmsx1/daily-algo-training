## LeetCode [123. 买卖股票的最佳时机 III](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/description/)
### 中文版本
一开始当然会使用完整的数组保存状态用于转移，但参考之前的思路，每一天都是从前一天转移的，所以可以简化为几个状态转移即可。

#### 完整代码
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n=prices.size();
        int buy1=-prices[0],buy2=-prices[0];
        int sell1=0,sell2=0;
        for(int i=1;i<n;i++){
            int& val=prices[i];
            buy1=max(buy1,-val);
            sell1=max(sell1,buy1+val);
            buy2=max(buy2,sell1-val);
            sell2=max(sell2,buy2+val);

        }
        return sell2;
    }
};
```
---
### English Version
Of course, initially the entire array is used to store the state for transitions. However, referring to the previous idea, since each day's state is derived from the previous day, it can be simplified to just a few state transitions.