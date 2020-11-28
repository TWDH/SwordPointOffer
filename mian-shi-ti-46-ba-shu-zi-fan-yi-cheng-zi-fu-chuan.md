---
description: >-
  给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成
  “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。
---

# 面试题46：把数字翻译成字符串

## 1.方法一：动态规划

![](.gitbook/assets/image%20%2836%29.png)

![](.gitbook/assets/image%20%2835%29.png)

* 此解法`dp[0]`为**“无数字”**的情况

```java
class Solution {
    public int translateNum(int num) {
        String str = String.valueOf(num);
        int len = str.length();
        if(len < 2){
            return len;
        }

        char[] charArray = str.toCharArray();
        int[] dp = new int[len + 1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i=1; i<len; i++){
            //dp[i]:字符串s[0..i)能翻译成小写字母的种类数，左闭右开
            dp[i+1] = dp[i];
            int currentNum = 10 * (charArray[i-1] - '0') + (charArray[i] - '0');
            if(currentNum > 9 && currentNum < 26){
                //当前字符与前两个有关
                dp[i+1] = dp[i] + dp[i-1];
            }
        }
        return dp[len];
    }
}
```

* 此方法`dp[0]`为**数组中的第一个数**

```java
class Solution {
    public int translateNum(int num) {
        String str = String.valueOf(num);
        int len = str.length();
        if(len < 2){
            return len;
        }

        char[] charArray = str.toCharArray();
        int[] dp = new int[len + 1];
        dp[0] = 1;
        for(int i=1; i<len; i++){
            //dp[i]:字符串s[0..i]能翻译成小写字母的种类数，左闭右闭
            dp[i] = dp[i-1];
            int currentNum = 10 * (charArray[i-1] - '0') + (charArray[i] - '0');
            if(currentNum > 9 && currentNum < 26){
                if(i == 1){
                    dp[i]++;
                }
                else{
                    //当前字符与前两个有关
                dp[i] += dp[i-2]; //dp[i] = dp[i-1]+dp[i-2];
                }
                
            }
        }
        return dp[len-1];
    }
}
```

