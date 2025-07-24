## LeetCode [673 最长递增子序列的个数](https://leetcode.cn/problems/number-of-longest-increasing-subsequence/description/)
### 中文版本
模拟即可。

#### 完整代码
```cpp
class Solution 
{
public:
    int findNumberOfLIS(vector<int>& nums) 
    {
        int n=nums.size();
        vector<vector<int>>dp(n,vector<int>(2,1));//以i结尾的最长递增子序列个数
        //参数1为长度，2为个数
        //dp[i][0]=max(dp[i][0],dp[j][0]+1);
        // if update:
        //     dp[i][1]=1;
        // else equal:
        //     dp[i][1]+=dp[j][1]

        dp[0][0]=1;
        dp[0][1]=1;

        int len=1;
        for(int i=1;i<n;i++)
        {
            for(int j=i-1;j>=0;j--)
            {
                if(nums[j]<nums[i])
                {
                    if(dp[i][0]<dp[j][0]+1){
                        dp[i][0]=dp[j][0]+1;
                        len=max(len,dp[i][0]);
                        dp[i][1]=dp[j][1];
                    }else{
                        if(dp[i][0]==dp[j][0]+1){
                            dp[i][1]+=dp[j][1];
                        }
                    }
                }
            }
        }


        int ans=0;
        for(int i=0;i<n;i++){
            if(dp[i][0]==len){
                ans+=dp[i][1];
            }
        }
        return ans;
    }
};
```
---
### English Version
Simulation is sufficient.