# 二分
## 第一题：在 D 天内送达包裹的能力 https://leetcode.cn/problems/capacity-to-ship-packages-within-d-days/submissions/
```java
class Solution {
    /**
    典型二分答案题：找子数组各自和的最大值最小
     */
    public int shipWithinDays(int[] weights, int days) {
        int right = 0;
        int left = 0;
        //初始化左右边界
        for(int weight: weights){
            left = Math.max(left, weight);
            right += weight;
        }
        //二分查找
        while(left < right){
           int mid = (left + right) / 2;
           if(validate(weights, days, mid)){
               right = mid;
           }else{
               left = mid + 1;
           }
        }
        return right;

    }

    private boolean validate(int[] weights, int days, int vol){
        int pack = 0;
        int count = 1;
        for(int weight: weights){
            //如果没有大于vol，就继续往当前package塞
            if(pack + weight <= vol){
                pack+=weight;
            }else{
                //否则新建一个package
                count++;
                pack=weight;
            }
        }
        //没有超过规定天数返回true
        return count<=days;
    }
}
```

## 第二题：搜索二维矩阵 https://leetcode.cn/problems/search-a-2d-matrix/submissions/
```java
class Solution {
    /**
    两次二分查找即可
     */
    public boolean searchMatrix(int[][] matrix, int target) {
        //前驱型：找到target可能所在行下标
        int rowIndex = binarySearchFirstColumn(matrix, target);
        if (rowIndex < 0) {
            return false;
        }
        //前驱型：target是否在该行
        return binarySearchRow(matrix[rowIndex], target);
    }

    private int binarySearchFirstColumn(int[][] matrix, int target){
        int left = -1, right = matrix.length - 1;
        while (left < right) {
            int mid = (left + right + 1) / 2;
            if (matrix[mid][0] <= target) {
                left = mid;
            } else {
                right = mid - 1;
            }
        }
        return right;
    }

    private boolean binarySearchRow(int[] matrix, int target){
        int left = -1, right = matrix.length - 1;
        while (left < right) {
            int mid = (left + right + 1) / 2;
            if (matrix[mid] <= target) {
                left = mid;
            } else {
                right = mid - 1;
            }
        }
        return matrix[right] == target;
    }
}
```

## TODO: 将后续题刷完
