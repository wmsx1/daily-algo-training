## LeetCode [55 跳跃游戏](https://leetcode.cn/problems/jump-game/description/)
### 中文版本
模拟即可。

#### 完整代码
```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int flag=0;
        int cur=0;
        int n=nums.size();
        while(flag<n-1 && cur<=flag){
            int _flag=cur+nums[cur++];
            flag=max(flag,_flag);
        }
        return flag>=n-1;
    }
};
```
---
### English Version
Simulation is sufficient.
