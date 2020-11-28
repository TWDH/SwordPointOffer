---
description: >-
  给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1]
  。请问 k[0]*k[1]*...*k[m-1]
  可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。
---

# 面试题14：剪绳子

## 方法一：动态规划

1. 定义 dp\[i\] 表示长度i的绳子能得到的最大乘积
2. 边界条件：`dp[1] = dp[2] = 1`，表示长度为 `2` 的绳子最大乘积为 `1`；
3. 状态转移方程：`dp[i] = max(dp[i], max((i - j) * j, j * dp[i - j]))`，可以这样理解：

![](../.gitbook/assets/image%20%2821%29.png)

```java
class Solution {
    public int cuttingRope(int n) {
        int[] dp = new int[n+1];
        dp[0] = 0; //没用
        dp[1] = 1; //没用
        dp[2] = 1;

        for(int i=3; i<=n; i++){
            for(int j=2; j<=i-1; j++){
                dp[i] = Math.max(dp[i], Math.max((i-j) * j, j * dp[i-j]));
            }
        }
        return dp[n];
    }
}
```

## 方法二：贪心算法

1. 当绳长`L<=3`时，易得最优解为 1 \* \(L-1\)
2. 当 `L > 3`时，
   1. 如果 L % 3的值为 1，则分解为两个2，剩下的分解为3 。
      * 只剩余一个1时，先从绳子中取下4（2 \* 2），再将其余的绳子都分成3。因为 2\*2 &gt; 1\*3 
   2. 如果 L % 3的值为 2，则分解为1个2，剩下的分解为3 
      * 只剩余一个2时，先取下一个2，再将其余绳子都分成3。 
   3. 如果 L % 3的值为 0，全部分解为3

```java
class Solution {
    public int cuttingRope(int n) {
        if(n <= 3){
            return 1 * (n-1);
        }
        int res = 1;
        if(n % 3 == 1){
            res = 4;
            n = n-4;
        }
        else if(n % 3 == 2){
            res = 2;
            n = n-2;
        }
        while(n != 0){
            res *= 3;
            n = n-3;
        }
        return res;
    }
}
```

