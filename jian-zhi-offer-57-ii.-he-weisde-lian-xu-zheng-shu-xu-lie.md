---
description: 输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。
---

# 面试题57 - II. 和为s的连续正数序列

## 1.双指针

1. 设置两个指针，small=1，big=2。因为序列是正整数序列且连续。
2. 在循环中每次判断当前序列的总和sum。
   1. 如果`sum < target`，则表示当前sum还需要更大的数。将**big右移**一位。
   2. 如果`sum > target`，则表示sum过大。将**small右移**一位。（一般都是先big右移，发现过大，才small右移。如果这时big左移，一定会变成sum过小的情况。）
   3. 如果`sum = target`，则表示找到序列。因为不可能以**left** \(or right\)为开头再重新找到一个符合条件的序列，所以移动指针**left++** \(or right++，以后发现不对都可以动过else中的语句调整，移动left或者right指针效果相当\)

```java
class Solution {
    public int[][] findContinuousSequence(int target) {
        List<int[]> result = new ArrayList<int[]>();
        
        //1.指定left，right指针
        for(int left = 1, right = 2; left < right;){
            //2.计算sum
            int sum = (left + right) * (right - left + 1) / 2;
            //3.相等：找到序列
            if(sum == target){
                int temp[] = new int[right - left + 1];
                for(int i = left; i <= right; i++){
                    temp[i - left] = i;
                }
                result.add(temp);
                left++;
            }
            //4.sum过小，增大big
            else if(sum < target){
                right++;
            }
            //5.sum过大，增大small
            else{
                left++;
            }
        }
        return result.toArray(new int[result.size()][]);
    }
}
```

### 实现方法二（慢）：

1. 如果不使用：“首相加末项乘项数除二”，则需要每次移动small或big时，都计算curSum。

```java
class Solution {
    public int[][] findContinuousSequence(int target) {
        if(target < 3){
            return new int[0][0];
        }
        //1.创建结果List集合
        List<int[]> result = new ArrayList<int[]>();
        
        //2.设置两根指针small,big
        int small = 1;
        int big = 2;
        int middle = (target + 1) / 2; //因为至少含有两个数
        int curSum = small + big;

        while(small < middle){
            //3.相等：找到序列
            int temp[] = new int[big - small + 1];
            if(curSum == target){
                temp = addResult(small, big);
                result.add(temp);
            }
            //4.sum过大，右移small直到sum小于等于target，每次移动都判断是否等于target。
            while(curSum > target){
                curSum -= small;
                small++;

                int temp2[] = new int[big - small + 1];
                if(curSum == target){
                    temp2 = addResult(small, big);
                    result.add(temp2);
                }
            }
            //5.sum过小，右移big。直到下一个while循环再判断是否等于target
            big++;
            curSum += big;
        }
        return result.toArray(new int[result.size()][]);
    }

    public int[] addResult(int a, int b){
        int[] list = new int[b - a + 1];
        int length = b - a + 1;
        for(int i=0; i < length; i++){
            list[i] = a;
            a++;
        }
        return list;
    }
}
```



