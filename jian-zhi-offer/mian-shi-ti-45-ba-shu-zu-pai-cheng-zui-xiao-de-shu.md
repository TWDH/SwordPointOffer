---
description: 输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。
---

# 面试题45：把数组排成最小的数

## 方法一：

1. 创建String数组，用来储存待排序数字
2. 将数字转换为String并存入数组
3. 排序
4. 将排序完的结果集用StringBuilder拼接输出。

![](../.gitbook/assets/image%20%2825%29.png)

```java
class Solution {
    public String minNumber(int[] nums) {
        String[] strs = new String[nums.length];
        for(int i=0; i<nums.length; i++){
            strs[i] = String.valueOf(nums[i]);
        }
        Arrays.sort(strs, (x,y) -> (x+y).compareTo(y+x));
        StringBuilder sb = new StringBuilder();
        for(String str: strs){
            sb.append(str);
        }
        return sb.toString();
    }
}
```

