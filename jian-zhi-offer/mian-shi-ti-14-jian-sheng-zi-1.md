---
description: "给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m\_段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m - 1] 。请问 k[0]*k[1]*...*k[m - 1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。答案需要取模 1e9+7（1000000007），如计算初始结果为：1"
---

# 面试题14：剪绳子

## 方法一：贪心算法+快速幂求余

![](../.gitbook/assets/image%20%2823%29.png)

![](../.gitbook/assets/image%20%2813%29.png)

```java
class Solution {
    public int cuttingRope(int n) {
        if(n <= 3) return n - 1;
        int a = n / 3; 
        int b = n % 3;
        if(b == 2){
            return (int)(quickpow(3,a) * b % 1000000007);
        }
        else{
            return (int)(quickpow(3,a-1) * (3 + b) % 1000000007);
        }
    }

    public long quickpow(int x, int n){
        long res = 1;
        long tt = x;
        while(n != 0){
            if((n & 1) == 1){
                res *= tt;
                res = res % 1000000007;
            }
            tt *= tt;
            tt %= 1000000007;
            n /= 2;
        }
        return res;
    }
}
```

