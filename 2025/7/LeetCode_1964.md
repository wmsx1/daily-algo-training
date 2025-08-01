## LeetCode [1964 找出到每个位置为止最长的有效障碍赛跑路线](https://leetcode.cn/problems/find-the-longest-valid-obstacle-course-at-each-position/description/)
### 中文版本
根据题目数据范围，需要使用二分。为此维护一个有序数组，即以`dp[i]`为结尾的最长递增子序列。对于每一个插入的数，尝试查找可能最长子序列，即第一个大于当前值的`cur=dp[j]`，这样就可以更新其为当前值以维护最长的递增子序列。

#### 完整代码
```cpp
class Solution {
public:
    vector<int> longestObstacleCourseAtEachPosition(vector<int>& obstacles) {
        int n=obstacles.size();
        vector<int>ans;
        vector<int>dp;
        for(auto it:obstacles){
            if(dp.empty() || it>=dp.back()){
                dp.push_back(it);
                ans.push_back(dp.size());
                continue;
            }
            int cur=upper_bound(dp.begin(),dp.end(),it)-dp.begin();
            dp[cur]=it;
            ans.push_back(cur+1);
        }
        return ans;
    }
};
//二分
//已经处理过的数，排序
//待处理的数，查找插入位置
```
---
### English Version
According to the data range specified in the problem, binary search is required. To achieve this, maintain a sorted array, dp, where `dp[i]` represents the smallest ending element of all increasing subsequences of length `i+1`. For each new number to be inserted, use binary search to find the leftmost position `j` such that `dp[j]` is greater than or equal to the current value. If such a position exists, replace `dp[j]` with the current value; otherwise, append the current value to the end of dp. This way, dp always maintains the smallest possible tail values for increasing subsequences of various lengths, ensuring the longest possible increasing subsequence can be constructed.