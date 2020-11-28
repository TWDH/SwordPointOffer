---
description: 在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。
---

# 面试题51： 数组中的逆序对

## 方法一：归并排序+递归

![](.gitbook/assets/image%20%2827%29.png)

1. 分治，分为左右两个有序数组（递归到最后只剩一个数的时候一定是有序的）。
2. 比较左右两数组（双指针移动），**较小**的放入原始数组。
3. 当**右数组**有数字进入**原数组**，逆序个数加入**左侧数组的所有值**。
   * 因为两侧此时都是**有序数组**，右侧数进入代表**此数比左边所有数都小**，所以左侧数组所有数都可以和此数形成逆序对。e.g. 图中的 “1”

```java
class Solution {
    public int reversePairs(int[] nums) {
        //小于2个数不可能有逆序数
        int len = nums.length;
        if(len < 2){
            return 0;
        }
        //创建copy数组复制原数组nums，并创建辅助数组temp
        int[] copy = new int[len];
        for(int i = 0; i < len; i++){
            copy[i] = nums[i];
        }

        int[] temp = new int[len];

        return reversePairs(nums, 0, len - 1, temp);
    }
    //计算并返回逆序对的个数（顺便排序）
    public int reversePairs(int[] nums, int left, int right, int[] temp){
        if(left == right){
            return 0;
        }
        //计算左右半区逆序对的个数
        int mid = left + (right - left) / 2;
        int leftPairs = reversePairs(nums, left, mid, temp);
        int rightPairs = reversePairs(nums, mid + 1, right, temp);
        
        //判断左右两部分组成的数组是否已经是有序数组，因为左面有序，右面有序，只要左最大小于右最小则整体有序。
        //递增序列就不会出现逆序对
        if(nums[mid] < nums[mid + 1]){
            return leftPairs + rightPairs;
        }
        
        //合并左右两部分数组，并计算逆序对个数
        int crossPairs = mergeAndCount(nums, left, mid, right, temp);
        return leftPairs + rightPairs + crossPairs;
    }

    public int mergeAndCount(int[] nums, int left, int mid, int right, int[] temp){
        for(int i = left; i <= right; i++){
            temp[i] = nums[i];
        }

        int i = left;
        int j= mid + 1;
        int count = 0;
        
        for(int k = left; k <= right; k++){ //左右边界一定是left < k <= right, 每次分治left或者right都会移动。所以不会都是[0, nums.length)
            //前两个if：判断i和j超出边界
            if(i == mid + 1){
                nums[k] = temp[j];
                j++;
            }
            else if(j == right + 1){
                nums[k] = temp[i];
                i++;
            }
            //temp[i]<=temp[j]，左面的i应该先被归并，否则如果左右相等，计算逆序对就会(有可能)少算。
            //e.g.[1,3,2,3,1] -> [1,3] & [1,2,3]这时就会少算[3,1]这对。
            else if(temp[i] <= temp[j]){
                nums[k] = temp[i];
                i++;
            }
            else{
                nums[k] = temp[j];
                j++;
                count += (mid - i + 1);
            }
        }
        return count;
    }
}
```

