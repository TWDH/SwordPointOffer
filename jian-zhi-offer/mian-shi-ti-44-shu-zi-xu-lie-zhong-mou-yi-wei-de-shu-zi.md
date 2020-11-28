---
description: >-
  数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。请写一个函数，求任意第n位对应的数字。
---

# 面试题44：数字序列中某一位的数字

## 方法一：找规律

![](../.gitbook/assets/image%20%2837%29.png)

缺点：无法解决long类型问题，数字过大

```java
class Solution {
    public int findNthDigit(int n) {
        int base = 9;
        int digits = 1; //几位数
        //1.算出有几位数
        while(n - base * digits > 0){
            n -= base * digits;
            base *= 10;
            digits++;
        }
        System.out.println("digits:"+digits);
        System.out.println("n:"+n);
        //2.余数，n：在digits位的第几个数
        int idx = n % digits;
        
        if(idx == 0){
            idx = digits; //以便最后选择第几个数字是答案
        }
        System.out.println("idx:"+idx);
        //3.得到最后数字的base
        int number = 1;
        for(int i=1; i<digits; i++){
            number *= 10;
        }
        System.out.println("number:"+number);
        //4.整除
        if(digits == idx){
            number += (n / digits) - 1;
        }
        else{
            number += n / digits;
        }

        //5.
        for(int i=idx; i<digits; i++){
            number /= 10;
        }
        
        return number % 10;
    }
}
```

## 方法二：正解

![----------------------](../.gitbook/assets/image%20%2822%29.png)

![--------------------](../.gitbook/assets/image%20%2815%29.png)

![------------------------------](../.gitbook/assets/image%20%281%29.png)

```java
class Solution {
    public int findNthDigit(int n) {
        int digit = 1;
        long start = 1;
        long count = 9;
        while(n > count){
            n -= count;
            start *= 10; //1, 10, 100
            digit += 1; //1,2,3 位数
            count = digit * start * 9; //e.g.两位数一共有多少个数字 2 * 10 * 9 = 180
        }
        //n是第几个数位
        long num = start + (n-1)/digit;
        return Long.toString(num).charAt((n-1) % digit) - '0';//数字在第几位
    }
}
```

