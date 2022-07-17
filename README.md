# 动规（二）
## 第一题：跳跃游戏 https://leetcode.cn/problems/jump-game/
```java
class Solution {
    public boolean canJump(int[] nums) {
        //公示：y：数组下标，x：当前位置，nums[i]：跳跃距离
        //rightMost>=nums.length-1，return true
        int rightMost = 0;
        for(int i=0;i<nums.length; i++){
            if(i<=rightMost){
                rightMost = Math.max(rightMost, i+nums[i]);
                if(rightMost>=nums.length-1){
                    return true;
                }
            }
        }
        return false;
    }
}
```

## 第二题：跳跃游戏 II https://leetcode.cn/problems/jump-game-ii/
```java
class Solution {
    public int jump(int[] nums){
        //dp公式：f(n)=min{f(i),1+f(i+j)}
        int[] dp=new int[nums.length];
        //base case
        dp[dp.length-1]=0;
        for (int i=nums.length-2;i>=0;i--){
            dp[i] = 1 << 31 - 1;//代替Integer.MAX_VALUE,防止溢出
            for (int j=1;j <= nums[i];j++){
                if (i+j<nums.length){
                    dp[i]=Math.min(dp[i],1+dp[i+j]);
                }
            }
        }
        return dp[0];
    }
}
```

## TODO: 将后续题刷完
