# 数组，链表，栈，队列
## 第一题：加一 https://leetcode.cn/problems/plus-one/
```java
class Solution {
    public int[] plusOne(int[] digits) {
        int n = digits.length;
        /**
        1.当最高位!=9的时候
        2.逆序遍历找到!=9的第一个数字加1
        3.将其后续全置为0
         */
        for (int i = n - 1; i >= 0; --i) {
            if (digits[i] != 9) {
                ++digits[i];
                for (int j = i + 1; j < n; ++j) {
                    digits[j] = 0;
                }
                return digits;
            }
        }

        /**
        1.当digits 中所有的元素均为9时
        2.创建新数组，长度为digits+1
        3.直接最高为置1
         */
        int[] ans = new int[n + 1];
        ans[0] = 1;
        return ans;
    }
}
```

## 第二题：合并两个有序链表 https://leetcode.cn/problems/merge-two-sorted-lists/
```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        /**
        1.当l1或l2为空，直接返回
        2.否则，比较l1和l2值，小的指向大的
        3.当一方遍历为空后，递归结束
         */
         if(list1 == null){
             return list2;
         }else if(list2 == null){
             return list1;
         }else if(list1.val <= list2.val){
             list1.next = mergeTwoLists(list1.next, list2);
             return list1;
         }else{
             list2.next = mergeTwoLists(list1, list2.next);
             return list2;
         }

    }
}
```

## TODO: 将后续题刷完
