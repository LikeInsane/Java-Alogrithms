# 字符串处理
## 第一题：字符串中的第一个唯一字符 https://leetcode.cn/problems/first-unique-character-in-a-string/
```java
class Solution {
    public int firstUniqChar(String s) {
        //找字符下标前后出现次数是否一样，相同返回下标值，否则-1
        for(char c: s.toCharArray()){
            if(s.indexOf(c) == s.lastIndexOf(c)){
                return s.indexOf(c);
            }
        }
        return -1;
    }
}
```

## 第二题：最长公共前缀 https://leetcode.cn/problems/longest-common-prefix/
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        //按列比较每个字符，当当前列不满足时，就返回之前的最长公共前缀
        if (strs == null || strs.length == 0) {
            return "";
        }
        int length = strs[0].length();
        int count = strs.length;
        for (int i = 0; i < length; i++) {
            char c = strs[0].charAt(i);
            for (int j = 1; j < count; j++) {
                if (i == strs[j].length() || strs[j].charAt(i) != c) {
                    return strs[0].substring(0, i);
                }
            }
        }
        return strs[0];
    }
}
```

## TODO: 将后续题刷完
