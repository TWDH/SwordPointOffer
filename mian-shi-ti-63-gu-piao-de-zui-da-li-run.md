---
description: 假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？
---

# 面试题63：股票的最大利润

## 方法一：动态规划

1. 定义`diff[i]`为: 当卖出价为数组中第i个数字时，可能获得的最大利润。
2. 在扫描到数组中第i个数字时，记住前面`i - 1`个数字的最小值，则可算出当前价位卖出时可能得到的最大利润。

```java
class Solution {
    public int maxProfit(int[] prices) {
        //0.特殊情况，只有一个点的时候无法计算收益
        if(prices == null || prices.length < 2){
            return 0;
        }
        //1.选定最小值
        int min = prices[0];
        int maxDiff = prices[1] - min;
        //2.遍历数组，找到与当前值最大的diffPrice。以此类推，直到找到最大值
        for(int i = 2; i < prices.length; i++){
            //3.记录前i - 1个点的最小值，以便计算收益
            if(prices[i - 1] < min){
                min = prices[i - 1];
            }
            int curDiff = prices[i] - min;
            if(curDiff > maxDiff){
                maxDiff = curDiff;
            }
        }
        //4.如果一直跌，没有正收益，则返回0
        if(maxDiff < 0){
            return 0;
        }

        return maxDiff;
    }
}
```

### 简洁写法

* 状态定义：dp\[i\]，以prices\[i\]为结尾的数值的最大利润（前i日最大利润）。
* 转移方程：前i日最大利润等于前`i - 1`日最大利润`dp[i - 1]` 与 第`i`日卖出最大利润中的**最大值**。
  * `min = Math.min(min, prices[i])`。
  * `dp[i] = Math.max(dp[i - 1], prices[i] - min)`。
  * min：记录更新每日最低价格
  * profit：因为`dp[i]`只与`dp[i - 1]`, `prices[i]`, `min`相关，因此可以使用一个便利profit代替**dp列表**。

```java
class Solution {
    public int maxProfit(int[] prices) {
        //1.选定最小值
        int min = Integer.MAX_VALUE;
        int profit = 0;
        //2.遍历数组，找到与当前值最大的profit。
        for(int i = 0; i < prices.length; i++){
            min = Math.min(min, prices[i]);
            //相当于profit[i-1]与当前profit[i]-之前最小值，作比较
            profit = Math.max(profit, prices[i] - min);
        }
        return profit;
    }
}
```

