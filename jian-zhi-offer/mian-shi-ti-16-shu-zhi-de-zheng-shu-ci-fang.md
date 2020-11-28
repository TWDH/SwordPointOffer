---
description: >-
  实现函数double Power(double base, int
  exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题
---

# 面试题16：数值的整数次方

## 方法一：

* 当exponent是0的时候，直接返回1即可，
* 当exponent小于0的时候，需要把它转化为正数才能更方便计算，同时base要变为1/base。
* 当exponent大于0的时候要分为两种情况，一种是偶数，一种是奇数。

1. 如果exponent是偶数我们只需要计算
   * `Power(base*base, exponent/2)`_。_举个例子，比如我们要计算`Power（3，8）`_，_我们可以改为 Power`（3*3，8/2`），也就是`Power（9，4）`。
2. 如果exponent是奇数，我们只需要计算
   * `basePower(base*base, exponent/2)`，比如`Power（3，9）`，我们只需要计算`3*Power（3*3，9/2）`，也就是`3*Power（9，4）`

```java
class Solution {
    public double myPow(double x, int n) {
        double result = 1.0;
        for(int i = n; i != 0; i /= 2, x *= x){
            if(i % 2 != 0){
                result *= x;
            }
        }
        if(n < 0){
            result = 1.0 / result;
        }
        return result;
    }
}
```



