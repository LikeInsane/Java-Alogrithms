# 哈希，集合，映射，递归，分治
## 第一题：子域名访问计数 https://leetcode.cn/problems/subdomain-visit-count/solution/zi-yu-ming-fang-wen-ji-shu-by-leetcode/
```java
class Solution {
    public List<String> subdomainVisits(String[] cpdomains) {
        /**
        1.构建hash表,格式<String, Integer>，存域名和计数
        2.先按照正则切割\s+(空格、换行符、回车为分隔线)
        3.从尾部遍历域名，放到hash表中
         */
         Map<String, Integer> domainCounts = new HashMap<>();
         for(String cpdomain: cpdomains){
             String[] cp = cpdomain.split("\\s+");
             String[] domains = cp[1].split("\\.");
             int count = Integer.valueOf(cp[0]);
             String cur="";
             for(int i=domains.length-1; i>=0; i--){
                 cur = domains[i] + (i < domains.length - 1 ? "." : "") + cur;
                 domainCounts.put(cur, domainCounts.getOrDefault(cur, 0) + count);
             }
         }
         
        /**
        遍历hash输出结果
         */
         List<String> res = new ArrayList();
         for(String dom: domainCounts.keySet()){
             res.add(domainCounts.get(dom) + " " + dom);
         }
         return res;
    }
}
```

## 第二题：数组的度 https://leetcode.cn/problems/degree-of-an-array/
```java
class Solution {
    public int findShortestSubArray(int[] nums) {
        /** 
        1.构建一个hash表，value存(出现次数,第一次出现位置，最后一次出现位置)
        2.如果已存在，则次数+1和更新最后出现位置
        3.否则新建数组
        */
        Map<Integer, int[]> res = new HashMap<>();
        for(int i=0; i<nums.length; i++){
            if(res.containsKey(nums[i])){
                res.get(nums[i])[0]++;
                res.get(nums[i])[2]=i;
            }else{
                res.put(nums[i], new int[]{1, i, i});
            }
        }
        /** 
        1.遍历hash表
        2.如果最大度小于当前度，更新度和最小子数组长度
        3.如果相等，再判断最小长度是否大于当前子数组长度，是则更新
        */
        int maxNums=0;
        int minLen=0;
        for(Map.Entry<Integer, int[]> entry : res.entrySet()){
            int[] arr = entry.getValue();
            if(maxNums<arr[0]){
                maxNums=arr[0];
                minLen=arr[2]-arr[1]+1;
            }else if (maxNums==arr[0]){
                if(minLen>arr[2]-arr[1]+1){
                    minLen=arr[2]-arr[1]+1;
                }
            }
        }
        return minLen;
    }
}
```

## TODO: 将后续题刷完
