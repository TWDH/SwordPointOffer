---
description: "把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组\_[3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。\_\_来源：力扣（LeetCode）链接：https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-"
---

# 面试题11：旋转数组的最小数字

## **方法一**：二分法

1.  我们考虑**数组中的最后一个元素 xx**：在最小值右侧的元素，它们的值一定都小于等于 xx；而在最小值左侧的元素，它们的值一定都大于等于 xx。
2. 在二分查找的每一步中，左边界为 lowlow，右边界为 highhigh，区间的中点为 pivotpivot

* 第一种情况是 `numbers[pivot] < numbers[high]`，`numbers[pivot]`是分界点（最小值）右侧的元素，可忽略右半部分。 
* 第二种情况是 `numbers[pivot] > numbers[high]`，这说明`numbers[pivot]` 是最小值左侧的元素，忽略二分查找区间的左半部分。 
* 第三种情况是 `numbers[pivot] = numbers[high]`，由于重复元素的存在，我们并不能确定`numbers[pivot]` 究竟在最小值的左侧还是右侧，因此我们不能莽撞地忽略某一部分的元素。我们唯一可以知道的是，由于它们的值相同，所以无论`numbers[high]` 是不是最小值，都有一个它的「替代品」`numbers[pivot]`，因此我们可以忽略二分查找区间的右端点。



```java
public int minArray(int[] numbers) {
    if(numbers.length == 0 || numbers == null){
        return -1;
    }

    int p1 = 0;
    int p2 = numbers.length - 1;
    int mid = 0;

    while(p1 < p2){ //为啥要等于呢: 旋转数组可能重复
        mid = (p1 + p2) / 2;
        if(numbers[mid] < numbers[p2]){
            p2 = mid;                
        }
        else if(numbers[mid] > numbers[p2]){
            p1 = mid+1;
        }
        else{
            p2--;
        }
    }
    return numbers[p1];
}
```

