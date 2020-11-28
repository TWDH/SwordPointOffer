---
description: >-
  在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1
  的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。
---

# 面试题3：数组中的重复数字

## **方法一：**排序

* 输入数组排序
* 扫描排序后数组，查看相邻是否重复
* O\(nlogn\)

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Arrays.sort(nums);
        for(int i=0; i<nums.length-1; i++){
            if(nums[i] == nums[i+1]){
                return nums[i];
            }
        }
        return -1;
    }
}
```



## **方法二：**哈希表

* 扫描每一个数字，判断哈希表里是否包含该数字
* 如果哈希表中无此数字，则将其加入哈希表
* 如果哈希表中有此数字，则找到答案
* O\(n\)

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i=0; i<nums.length; i++){
            if(map.containsKey(nums[i])){
                return nums[i];
            }
            map.put(nums[i], 0 );
        }
        return -1;
    }
}
```

## **方法三：**奇思妙想

* 扫描数组，当扫描到下标为**i**的数字**m**时
  * 比较数字m==i ?
    * 是，接着扫描下一个数字
    * 否，将数字m与**第m个数字**比较
      * 相等：找到重复数
      * 不相等：第i个数和第m个数交换

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        for(int i=0; i<nums.length; i++){
            //数字m不等于i
            if(i != nums[i]){
                //数字m与第m个数字比较
                if(nums[i] == nums[nums[i]]){
                    return nums[i];
                }
                else{
                    swap(nums, i, nums[i]);
                }
            }           
        }
        return -1;
    }
    private void swap (int[]nums, int a, int b){
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }
}
```

