---
description: >-
  给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B 中的元素
  B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。
---

# 面试题66. 构建乘积数组

## 方法一：倒三角

1. 初始化：数组B，其中`B[0] = 1`，左上角。辅助变量`temp = 1`，右下角。
2. 计算`B[i]`的下三角各个元素乘积，直接乘入`B[i]`；
3. 计算`B[i]`的上三角各个元素乘积，记为temp，再将temp依次计入B。

![](../.gitbook/assets/image%20%2824%29.png)

```java
class Solution {
    public int[] constructArr(int[] a) {
       
        //1.特殊情况
        if(a == null || a.length == 0){
            return new int[0];
        }
        //2.设置数组b，辅助数组temp 
        int[] b = new int[a.length];
         b[0] = 1;
        int temp = 1;

        //3.计算下三角
        for(int i = 1; i < a.length; i++){
            b[i] = b[i - 1] * a[i - 1];
        }

        //4.计算上三角
        for(int i = a.length - 2; i >= 0; i--){
            temp *= a[i + 1]; //这里保证b[3]中乘的是a[4]
            b[i] *= temp; 
        }
        return b;
    }
}
```

