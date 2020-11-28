# 面试题53：在排序数组中查找数字 I

## 方法一：二分法

1. 排序数组nums中，所有数字target形成一个窗口。记左边界为left，右边界为right。使用二分法找到左右边界，最终target的数量为`right-left-1` 
2. 初始化：左边界`i=0`，右边界`j=len(nums)-1`。
3. 循环二分：当闭区间\[i,j\]无元素时跳出，即i&gt;j时。
   1. 计算**mid**
   2. 若`nums[m] < target`，则target在`[m+1, j]`中，因此`i = m+1`
   3. 若`nums[m] > target`，则target在`[i, m-1]`中，因此`j = m -1`
   4. 若`nums[m] = target`，分为两种情况：
      1. 查找**右边界**right，则右边界在`[m+1, j]`中，执行`i = m + 1`;
      2. 查找**左边界**left，则左边界在`[i, m-1]`中，执行`j = m - 1`;
4. 返回值：两次二分法找到right和left，返回`right - left - 1`即可。

```java
class Solution {
    public int search(int[] nums, int target) {
        if(nums.length == 0){
                    return 0;
        }
        //初始左右指针位置
        int i = 0;
        int j = nums.length - 1;
        //第一次二分：找right边界
        //这边是“小于等于”，因此当循环结束后，ij不重合，且如果存在target值的话，
        //i的位置就是右边界（target值序列右边第一个大于target值的位置），因为倒数第二次循环一定是i=mid+1；
        //且此时最后一次循环nums[mid]>target所以此时j--,j指向target
       
        while(i <= j){
            int mid = (i + j) / 2;
            //这里是“小于等于”，目的是为了确定右边界，就是说当mid等于target时，因为不确定后面还有没有target，所以同样需要左边收缩范围
            if(nums[mid] <= target){
                i = mid + 1;
            }
            else{
                j = mid - 1;
            }
        }
        //在更新right边界值之前，需要判断这个数组中是否存在target，如果不存在（看j指向的位置是不是target，为什么看的是j指针？详见上面的注释）
        if(j >= 0 && nums[j] != target){
            return 0;
        }
        //更新right边界
        int right = i;
        //重置指针
        i = 0;
        j = nums.length - 1;
        //第二次二分：找left边界
        //结束之后，j指向target序列左边第一个小于它的位置，i指向target（经过上面判断，target一定存在）
        while(i <= j){
            int mid = (i + j) / 2;
            //这里是“大于等于”，目的是确定左边界，因为就算当mid等于target的时候，因为不确定左边还有没有target，所以同样需要收缩右边界
            if(nums[mid] >= target){
                j = mid -1;
            }
            else{
                i = mid + 1;
            }
        }
        //更新左指针
        int left = j;
        return right - left - 1;
    }
}
```

