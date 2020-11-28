---
description: 输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。
---

# 面试题57. 和为s的两个数字

## 方法一：HashMap

1. 创建一个HashMap储存&lt;数组值，位置&gt;。
2. 遍历数组，如果搜索到某个值nums\[i\]，使得target-nums\[i\]的值在HashMap中存储过。那么nums\[i\]和target-nums\[i\]的和就是答案。
3. 注意：此题不需要返回索引位置，所以HashMap中的value没有使用

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> hashmap = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            if(hashmap.containsKey(target - nums[i])){
                return new int[]{target - nums[i], nums[i]};
            }
            hashmap.put(nums[i], i);
        }
        return new int[0];
    }
}
```

## 方法二：双指针

1. 设定两个指针`i，j`一头一尾。
2. 如果`nums[i] + nums[j] > target`，则`j`向前移动一位。
3. 如果`nums[i] + nums[j] < target`，则`i`向后移动一位。

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int i = 0; 
        int j = nums.length - 1;

        while(i < j){
            if(nums[i] + nums[j] > target){
                j--;
            }
            else if(nums[i] + nums[j] < target){
                i++;
            }
            else{
                return new int[]{nums[i], nums[j]};
            }
        }
        return new int[0];
    }
}
```

