---
description: "一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n\_级的台阶总共有多少种跳法。答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。来源：力扣（LeetCode）链接：https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof著作权归领扣网络所有。"
---

# 面试题10-2：青蛙跳台阶问题

## **方法一：**动态规划

* 此题与上一题相同，为斐波那契数列

```java
class Solution {
    public int numWays(int n) {
        //1.台阶为2以下的情况
        if(n<2){
            return 1;
        }
        //2.多于2个台阶，建立dp。dp[i]表示第i级的跳法
        int[] dp = new int[n+1];
        dp[1] = 1;
        dp[2] = 2;
        for(int i=3; i<=n; i++){
            dp[i] = (dp[i-1] + dp[i-2]) % 1000000007;
        }
        return dp[n];
    }
}
```

