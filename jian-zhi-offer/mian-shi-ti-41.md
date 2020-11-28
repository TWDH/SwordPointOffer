---
description: >-
  如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。来源：力扣（LeetCode）链接：https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof著作权归领扣网络所有。商业转
---

# 面试题41：数据流中的中位数

![](../.gitbook/assets/image%20%2812%29.png)

## 方法一：堆

1. 建立两个堆，**A最小堆**储存**较大**的一半，**B最大堆**储存**较小**的一半。
2. m：A堆中元素个数；n：B堆中元素个数
3. addNum\(num\)函数：（交替插入）
   1. 当 **m=n** \(N为偶数\)时，设定向**A**添加一个元素（也可以向B）。
      * 实现方法：将新元素num插入B，再将B的堆顶元素插入A。（保证B中最大的元素插入A，这样A储存的是较大的一半）
   2. 当 **m≠n**（N为奇数时），设定向**B**添加一个元素（也可以向A）。
      * 实现方法：将新元素加入A，再将A的堆顶元素插入B。（保证A中最小的插入B，这样B储存的是较小的一半）
4. findMedian\(\)函数：
   1. 当m=n时（N为偶数），则中位数为（A+B）/2
   2. 当m≠n时（N为奇数），则中位数为**A**的栈顶元素（因为AB开始均为0，是偶数，则先往A中插入了一个数）

![](../.gitbook/assets/image%20%2830%29.png)

```java
class MedianFinder {
    PriorityQueue<Integer> A, B;
    /** initialize your data structure here. */
    public MedianFinder() {
        //最小堆
        A = new PriorityQueue<Integer>();
        //最大堆
        B = new PriorityQueue<Integer>((o1,o2) -> o2-o1);

    }
    
    public void addNum(int num) {
        //奇数
        if(A.size() != B.size()){
            A.add(num);
            B.add(A.poll());
        }
        //偶数
        else{
            B.add(num);
            A.add(B.poll());
        }
    }
    
    public double findMedian() {
        if(A.size() != B.size()){
            return A.peek();
        }
        else{
            return (A.peek() + B.peek())/2.0;
        }
    }
}
```

