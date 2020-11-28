# 面试题42. 连续子数组的最大和

## 方法一：

1. 设置当前最大值：curSum=0，和全局最大值greatestSum=最小值。
2. 遍历数组num，如果之前的数\(curSum\)加起来是负数，则把当前`nums[i]`设为curSum。因为之前的负数不可能提供更大的sum。否则，将当前数nums\[i\]加入curSum。
3. 如果`curSum>greatestSum`, 则更新greatestSum = curSum。（之后有负数也可以，只要curSum总数大于0即可，当有更大的数时才更新）

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums == null || nums.length <= 0){
            return 0;
        }

        int curSum = 0;
        int greatestSum = Integer.MIN_VALUE;
        for(int i=0 ;i < nums.length; i++){
            if(curSum <= 0){
                curSum = nums[i];
            }
            else{
                curSum += nums[i];
            }
            if(curSum > greatestSum){
                greatestSum = curSum;
            }
        }
        return greatestSum;
    }
}
```

