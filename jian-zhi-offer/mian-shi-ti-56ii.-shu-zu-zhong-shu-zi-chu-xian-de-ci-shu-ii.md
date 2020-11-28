---
description: 在一个数组 nums 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。
---

# 面试题56：II. 数组中数字出现的次数 II

## 方法一：

1. 二进制表达：
   1. 三个相同的数：每一位的数字加起来必然可以被3整除。
   2. α-只出现一次的数：加上这个数，如果某位不能被整除了，则α的该位是“1”。否则是“0”
2. 注意：
   * 计算每一位数字和时：为保证**二进制规律**，j是从31向下递减，因为bitMask是0001，并且左移。如果`num & bitMask`后等于1，表示该位为1。这样bitSum中存储的数字就是从**小\(左\)到大\(右\)**的了。
   * `& 0001`表示判断某一位是否为1。

```java
class Solution {
    public int singleNumber(int[] nums) {
        // if(nums.length == 0 || nums == null){
        //     return new int{};
        // }
        //每一位上的数字和
        int[] bitSum = new int[32];

        //1.把每个数字的每一位都相加，能被三整除的则α该位是0；否则是1
        //α:只出现一次的数
        for(int i=0; i < nums.length; i++){
            int bitMask = 1; //0001
            //对每一位计算数字和
            //保证二进制规律：左面是高位，右面是低位。因为bitMask是从0001（低位）开始
            //所以j从31向下递减
            for(int j = 31; j >= 0; j--){
                int bit = nums[i] & bitMask; //判断某一位是否为1/0，0110 & 0001 = 0
                if(bit != 0){
                    bitSum[j] += 1;
                }
                bitMask <<= 1; 
            }
        }

        int result = 0;
        for(int k = 0; k < 32; k++){
            //先移动在“加”，因为这样就可以“加”在reuslt向左移位时，右面补的“0”上了
            result <<= 1;
            result += bitSum[k] % 3;
        }
        return result;

    }
}
```

