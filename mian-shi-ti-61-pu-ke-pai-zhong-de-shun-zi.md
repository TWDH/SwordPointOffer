---
description: >-
  从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0
  ，可以看成任意数字。A 不能视为 14。
---

# 面试题61：扑克牌中的顺子

![](.gitbook/assets/image%20%2826%29.png)

## 方法一：排序+遍历

1. 判断特殊情况
2. 对数组进行排序
3. 找到大王joker的个数，判断牌中是否有对子。如果有则直接返回false。
4. 依次计算紧贴着的两个牌的差距gap（`nums[i + 1] - nums[i] - 1`），并将它们相加（有可能是跳跃不连续的）。
5. 比较大王joker的个数和牌的差距种树gap。gap需要小于等于joker个数才返回true。

```java
class Solution {
    public boolean isStraight(int[] nums) {
        //0.特殊情况
        if(nums == null || nums.length < 5){
            return false;
        }
        //1.排序
        Arrays.sort(nums);
        //2.找到joker个数
        int joker = 0;
        for(int i = 0; i < 4; i++){
            //计算joker个数
            if(nums[i] == 0){
                joker++;
                continue; //这里直接跳过后面的，以防识别成对子
            }
            //对子，前后两个牌相等
            if(nums[i] == nums[i + 1]){
                return false;
            }
            joker -= (nums[i + 1] - nums[i] - 1);
        }
        return joker >= 0;
    }
}
```

### 朴实无华的写法

```java
class Solution {
    public boolean isStraight(int[] nums) {
        //0.特殊情况
        if(nums == null || nums.length == 0){
            return false;
        }
        //1.数组排序
        Arrays.sort(nums);
        //2.计算joker的数量
        int joker = 0;
        for(int i = 0; i < 5; i++){
            if(nums[i] == 0){
                joker++;
            }
        }
        //3.gap计算相邻两数间隔的距离，需要都加在一起
        int gap = 0;
        for(int i = joker; i < 4; i++){ //这里i=joker起手，因为0会连续出现在数组前面，防止被当成双
            //4.如果连续出现两个数，则返回false
            if(nums[i] == nums[i + 1]){
                return false;
            }
            //5.计算临近两数差
            gap += nums[i + 1] - nums[i] - 1;
        }
        //大王只要比gap多就可以
        return joker >= gap ? true : false;
    }
}
```

