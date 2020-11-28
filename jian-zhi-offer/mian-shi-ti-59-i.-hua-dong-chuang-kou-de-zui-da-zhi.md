---
description: 给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值
---

# 面试题59 - I. 滑动窗口的最大值

![](../.gitbook/assets/image%20%289%29.png)

## 方法一：双端队列deque

1. 使用双端队列deque，使得最大值一直在队首\(左边\)。
2. 初始化`i`，j两个指针，指向窗口收尾两个元素。
3. 当`i > 0`，队首元素`deque[0] = num[i-1]`\(已删除元素\)时，将队首元素出队。
   * deque\[0\]队首元素，代表当前窗口的最大值。当i，j向后移动一位后，如果已删除元素（窗口刚划过的元素`num[i-1]`）等于队首元素，一定要将deque\[0\]出队。因为这个元素不可能是新窗口的最大值了。
   * 如果`deque[0] != num[i-1]`，那么表示num中，有后面的数值比前面的大。所以deque会替换为哪个最大的值。详见4。
   * 如果num前面出现较大的值（num降序），则进入deque自然也就靠前deque\[0\] = num\[i-1\]成立；如果num后面出现较大的值（比所有都大时，num升序），则deque\[0\] = num\[i-1\]就不成立了。
4. 删除所有`deque`中小于`num[j]`的数值，以保持deque中是递减序列。
5. 将`num[j]`加入deque尾部。
6. 若形成窗口（`i>=0`），则将窗口最大值`deque[0]`加入`res`。

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums.length == 0 || k == 0){
            return new int[0];
        }
        //1.创建双端队列deque
        Deque<Integer> deque = new LinkedList<>();
        //2.创建放结果的数组res
        int[] res = new int[nums.length - k + 1];
        //3.遍历滑动窗口
        for(int i = 1 - k, j = 0; j < nums.length; i++, j++){
            //3.1 当deque[0] = num[i-1]，将队首元素出队
            if(i > 0 && deque.peekFirst() == nums[i - 1]){
                deque.removeFirst();
            }
            //3.2 如果nums[j]大于deque中的值，将其出队
            while(!deque.isEmpty() && deque.peekLast() < nums[j]){
                deque.removeLast();
            }
            //3.3将nums[i]加入deque
            deque.addLast(nums[j]);

            //3.4加入res
            if(i >= 0){
                res[i] = deque.peekFirst();
            }
        }
        return res;
    }
}
```

## 方法一：变种

* 将 “未形成窗口” 和 “形成窗口后” 两个阶段拆分到两个循环里实现。代码虽变长，但减少了冗余的判断操作。
* 这里的`“i”`是窗口的最后一位。相当于上一个解答中的`“j”`。

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums.length == 0 || k == 0){
            return new int[0];
        }
        //1.创建双端队列deque
        Deque<Integer> deque = new LinkedList<>();
        //2.创建放结果的数组res
        int[] res = new int[nums.length - k + 1];
        //3.遍历滑动窗口(未形成时)
        for(int i = 0; i < k; i++){
            //3.1 如果有num[i]大于deque中的数，则将deque中的数删除
            while(!deque.isEmpty() && nums[i] > deque.peekLast()){
                deque.removeLast();
            }
            //3.2将新的数加入deque
            deque.addLast(nums[i]);
        }
        //3.3将队首加入res
        res[0] = deque.peekFirst();

        //4.遍历滑动窗口(窗口形成时)
        for(int i = k; i < nums.length; i++){
            //4.1如果deque[0]队首，等于刚移除的值。则将其从队首移除
            if(nums[i - k] == deque.peekFirst()){
                deque.removeFirst();
            }
            //4.2 如果有num[i]大于deque中的数，则将deque中的数删除
            while(!deque.isEmpty() && deque.peekLast() < nums[i]){
                deque.removeLast();
            }
            //4.3将新的数加入deque
            deque.addLast(nums[i]);
            //4.4将队首加入res
            res[i - k + 1] = deque.peekFirst();
        }
        return res;
    }
}
```

