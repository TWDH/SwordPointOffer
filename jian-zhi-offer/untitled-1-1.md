# 面试题53：II. 0～n-1中缺失的数字

## 方法一：二分法

1. **初始化：** 左边界 i = 0 ，右边界 j = len\(nums\) - 1；代表闭区间 \[i, j\] 。
2.  **循环二分：**
   1. 计算中点 m = \(i + j\) // 2;
   2. 若 nums\[m\] = m ，则 “右子数组的首位元素” 一定在闭区间 \[m + 1, j\]中，因此执行 i = m + 1
   3. 若 nums\[m\] !=m ，则 “左子数组的末位元素” 一定在闭区间 \[i, m - 1\] 中，因此执行 j = m - 1
3. **返回值：** 跳出时，变量 i 和 j 分别指向 “右子数组的首位元素” 和 “左子数组的末位元素” 。因此返回 i即可。

```java
class Solution {
    public int missingNumber(int[] nums) {
        int i = 0;
        int j = nums.length - 1;

        while(i <= j){
            int mid = (i + j) / 2;
            if(nums[mid] == mid){
                i = mid + 1;
            }
            else{
                j = mid - 1;
            }
        }
        return i;
    }
}
```



