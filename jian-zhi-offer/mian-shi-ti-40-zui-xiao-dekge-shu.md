---
description: 输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。
---

# 面试题40：最小的k个数

**Comparator：**  
//从小到大排序 o1 - o2  
//从大到小排序 o2 - o1  
实现int compare\(T o1, T o2\);方法，返回正数，零，负数各代表大于，等于，小于。

## 方法一：最大堆

1. 创建数组res储存答案
2. 创建最大堆
3. 想堆中放入k个数
4. 取arr中的数，并与堆中的数比较。如果堆的最大值&gt;arr中的数，则将其加入堆。
5. 返回堆中的数。

```java
public int[] getLeastNumbers(int[] arr, int k) {
    int[] res = new int[k];
    if(k == 0){
        return res;
    }

    PriorityQueue<Integer> queue = new PriorityQueue<>(new Comparator<Integer>(){
        public int compare(Integer num1, Integer num2){
            return num2 - num1;
        }
    });
    //1.向堆中放入k个元素
    for(int i=0; i<k; i++){
        queue.offer(arr[i]);
    }
    //2.比较arr中元素，与堆中最大值
    for(int i=k; i<arr.length; i++){
        if(queue.peek() > arr[i]){
            queue.poll();
            queue.offer(arr[i]);
        }
    }
    //3.输出
    for(int i=0; i<k; i++){
        res[i] = queue.poll();
    }
    return res;
}
```

