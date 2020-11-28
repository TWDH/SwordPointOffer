---
description: "请实现一个函数，输入一个整数，输出该数二进制表示中 1 的个数。例如，把 9\_表示成二进制是 1001，有 2 位是 1。因此，如果输入 9，则该函数输出 2。"
---

# 面试题15：二进制中1的个数

## 方法一：&gt;&gt;&gt;1右移

1. 创建result记录含有1的次数
2. 让待检测数n，与运算数字“1”
   1. 如果n&1 = 0，则说明最末尾是0
   2. 如果n&1 = 1，则说明最末尾是1
3. 让数字n右移，最末尾会自动消失，直到数字n变为0。

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int result = 0;
        while(n != 0){
            result = result + (n & 1);
            n = n >>> 1;
        }
        return result;
    }
}
```

## 方法二：n & \(n-1\)

* **\(n - 1\)\(n−1\) 解析：** 二进制数字 nn 最右边的 11 变成 00 ，此 11 右边的 00 都变成 11 。
*  **n&\(n−1\) 解析：** 二进制数字 nn 最右边的 1 变成 0 ，其余不变。

![](../.gitbook/assets/image%20%2828%29.png)

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int result = 0;
        while(n != 0){
            result++;
            n = n & (n-1);
        }
        return result;
    }
}
```

