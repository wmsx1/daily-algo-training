## LeetCode [1218 最长定差子序列](https://leetcode.cn/problems/longest-arithmetic-subsequence-of-given-difference/description/)
### 中文版本
模拟即可。另外根据数据范围限制使用 `map` 记录之前的值。
#### 完整代码
```cpp
class Solution {
public:
    int longestSubsequence(vector<int>& arr, int difference) {
        int ans=1;
        int n=arr.size();
        unordered_map<int,int>mem;

        for(int i=0;i<n;i++){
            int val=arr[i]-difference;
            if(!mem.count(val)){
                mem[arr[i]]=1;
                continue;
            }
            // mem[arr[i]]=max(mem[arr[i]],mem[val]+1);
            mem[arr[i]]=mem[val]+1;
            ans=max(ans,mem[arr[i]]);
        }
        
        return ans;
    }
};
```
---
### English Version
Simulate as needed. Additionally, use a map to record previous values based on the data range constraints.