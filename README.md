# 贪心，动规（一）
## 第一题：爬楼梯 https://leetcode.cn/problems/climbing-stairs/
```java
class Solution {
    public int climbStairs(int n) {
        //状态转移方程：f(n) = f(n-1) + f(n-2)
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1; 
        for(int i=2;i<=n;i++){
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```

## 第二题：最长递增子序列的个数 https://leetcode.cn/problems/number-of-longest-increasing-subsequence/
```java
class Solution {
    public int findNumberOfLIS(int[] nums) {
        //状态转移方程：dp[i]=max(dp[j])+1,其中0≤j<i且num[j]<num[i]
        int n = nums.length, maxLen = 0, ans = 0;
        int[] dp = new int[n];
        int[] cnt = new int[n];
        for (int i = 0; i < n; ++i) {
            dp[i] = 1;
            cnt[i] = 1;
            for (int j = 0; j < i; ++j) {
                if (nums[i] > nums[j]) {
                    if (dp[j] + 1 > dp[i]) {
                        dp[i] = dp[j] + 1;
                        cnt[i] = cnt[j]; // 重置计数
                    } else if (dp[j] + 1 == dp[i]) {
                        cnt[i] += cnt[j];
                    }
                }
            }
            if (dp[i] > maxLen) {
                maxLen = dp[i];
                ans = cnt[i]; // 重置计数
            } else if (dp[i] == maxLen) {
                ans += cnt[i];
            }
        }
        return ans;
    }
}
```

## TODO: 将后续题刷完
