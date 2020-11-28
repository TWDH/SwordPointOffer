# 面试题21：调整数组顺序使奇数位于偶数前面

## 方法一：双指针

1. 设置前后两个指针p1, p2
2. p1用来寻找从前向后第一个**偶数**，p2用来寻找从后向前第一个**奇数**。
3. 只要 `p1 < p2`，则将两数交换

```java
class Solution {
    public int[] exchange(int[] nums) {
        if(nums == null || nums.length == 0){
            return nums;
        }

        int p1 = 0; 
        int p2 = nums.length - 1;
        while(p1 < p2){
            //从前向后找到第一个偶数
            while(p1 < p2 && (nums[p1] % 2) != 0){
                p1++;
            }
            //从后向前找到第一个奇数
            while(p1 < p2 && (nums[p2] % 2) == 0){
                p2--;
            }

            if(p1 < p2){
                int temp = nums[p1];
                nums[p1] = nums[p2];
                nums[p2] = temp;
            }
        }
        return nums;
    }
}
```

