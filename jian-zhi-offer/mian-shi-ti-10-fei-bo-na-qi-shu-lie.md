---
description: >-
  写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。斐波那契数列的定义如下：F(0) = 0,   F(1) = 1F(N) =
  F(N - 1) + F(N - 2), 其中 N > 1.斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。答案需要取模
  1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。
---

# 面试题10：斐波那契数列

## **方法一：**

* 从下向上计算：先根据f\(0\)和f\(1\)计算出f\(2\)，再计算f\(3\) ... ... 以此类推
* 时间复杂度O\(n\)

```java
class Solution {
    public int fib(int n) {
        if(n<2){
            return n;
        }
        long fibN=0;
        long fibNMinusone = 1;
        long fibNMinustwo = 0;
        int constant = 1000000007;
        

        for(int i=2; i<=n; i++){
            fibN = fibNMinusone + fibNMinustwo;
            fibNMinustwo = fibNMinusone % constant;
            fibNMinusone = fibN % constant;
        }
        return (int)fibN  % constant;
    }
}
```

