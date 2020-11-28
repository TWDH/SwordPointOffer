---
description: '求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。'
---

# 面试题64：求1+2+…+n

## 方法一：逻辑运算符的短路效应

* `if(A && B)`  //若A为**false**，则B的判断**不会执行**\(即短路\)，直接判定`A && B`为false。
* `if(A || B)`  //若A为**true**，则B的判断则**不会执行**\(即短路\)，直接判定`A || B`为true。
* 上述的不会执行，即为递归跳出循环的条件
* boolean Nothing：只为了能在java中构成语句，无实际作用。
* Java中，开启递归的函数`sumNums(n - 1) > 0`，整体作为boolean的输出，否则报错。

```java
// &&版
class Solution {
    //1.初始化res，作为最后的答案
    int res = 0;
    public int sumNums(int n) {
        
        //2.初始化Nothing，用于控制递归
        boolean Nothing = n > 1 && sumNums(n - 1) > 0;
        res += n;
        return res;
    }
}
```

```java
// ||版
class Solution {
    //1.初始化res，作为最后的答案
    int res = 0;
    public int sumNums(int n) {
        
        //2.初始化Nothing，用于控制递归
        boolean Nothing = n < 1 || sumNums(n - 1) > 0;
        res += n;
        return res;
    }
}
```

