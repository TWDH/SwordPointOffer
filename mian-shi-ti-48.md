---
description: 请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。
---

# 面试题48：最长不含重复字符的子字符串

![](.gitbook/assets/image%20%2838%29.png)

## 方法一：动态规划+HashMap

1. 创建HashMap存储，与字符`s[j]`相同的最近字符`s[i]`。`s[i]=s[j]` 
2. 创建**res**存储最终答案，创建**temp**表示`dp[j-1]`。
3. 循环遍历字符串中的字符
   1. 记录`i`：表示与当前字符`s[j]`相同的字符的位置。如果没有则`i=-1`，因为如果该字符没出现过，不返回**-1**会使后面计算距离`d=j-i`时少算一位数。
   2. 更新哈希表：把当前字符以`字符(key)~位置(value)`的形式存入HashMap，这里以字符为key，这样就不会出现重复的现象，一个字符只能有一个对应的位置。
   3. 计算temp\(dp\[j-1\]\)：
      1. `dp[j-1] < j - i`：距离`d = j - i`，表示本字符上次出现在`dp[j-1]`之前，所以`dp[j-1]`中不包含次字符。因此`dp[j] = dp[j-1] + 1`。
      2. `dp[j-1] > j - i`：此时表示s\[j\]的字符在`dp[j-1]`中已经出现过了，那么此字符的最长子字符就不能从`dp[j-1]`开始算了，而是应该计算`s[i]~s[j]`之间的距离。
   4. 更新res：使其一直保持temp的最大值。
   5. 返回res

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character, Integer> map = new HashMap<>();
        int res = 0;
        int temp = 0;
        for(int j = 0; j < s.length(); j++){
            int i = map.getOrDefault(s.charAt(j), -1);
            map.put(s.charAt(j), j);
            temp = temp < (j - i) ? temp + 1 : (j - i);
            res = Math.max(res, temp);
        }
        return res;
    }
}
```

