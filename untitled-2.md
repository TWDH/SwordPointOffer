---
description: >-
  0,1,,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字。求出这个圆圈里剩下的最后一个数字。例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。
---

# 面试题62：圆圈中最后剩下的数字

![](.gitbook/assets/image%20%283%29.png)

## 方法一：模拟链表

1. 创建ArrayList并将数值放入其中。
2. 将对应数字删除，index表示需要删除数字的索引。
   * 应删除的数字索引：`index + m`; 因为当前数被删除，所以需要再`-1`。
   * 第一个数，因为索引是0，所以公式同样成立（因为把自己算进去了，如何删除第三个数，则对应索引2）。

```java
class Solution {
    public int lastRemaining(int n, int m) {
        //1.创建ArrayList
        ArrayList<Integer> list = new ArrayList<>();
        //2.将数字加入list
        for(int i = 0; i < n; i++){
            list.add(i);
        }
        //3.删除数字
        int index = 0;
        while(n > 1){
            //应删除的数字索引：index + m; 因为当前数被删除，所以需要再-1
            index = (index + m - 1) % n;
            list.remove(index);
            n--;
        }
        return list.get(0);
    }
}
```

