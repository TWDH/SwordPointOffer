# 面试题49：丑数

## 方法一：

1. 丑数是另一个丑数乘以2，3，5之后的结果，所以创建一个数组存储排序好的丑数数组。
2. 对于**×2**而言，肯定存在一个丑数T2，排在他前面的丑数×2都会**小于**当前最大丑数；排在他后面的丑数×2都会**大于**当前最大丑数**很多**。T2是唯一丑数**正好大于**当前最大丑数`uglyNumber[i]`的。
3. 对于×3和×5而言，也存在对应的T3，T5。那么下一个丑数一定是T2，T3，T5中的最小值。

```java
class Solution {
    public int nthUglyNumber(int n) {
        if(n <= 0){
            return 0;
        }
        int[] uglyNumber = new int[n];
        uglyNumber[0] = 1;
        int index2 = 0;
        int index3 = 0;
        int index5 = 0;
        for(int i = 1; i < n; i++){
            uglyNumber[i] = getMin(uglyNumber[index2] * 2, uglyNumber[index3] * 3, uglyNumber[index5] * 5);
            while(uglyNumber[index2] * 2 <= uglyNumber[i]){
                index2++;
            }
            while(uglyNumber[index3] * 3 <= uglyNumber[i]){
                index3++;
            }
            while(uglyNumber[index5] * 5 <= uglyNumber[i]){
                index5++;
            }
        }
        return uglyNumber[n-1];
    }

    public int getMin(int a, int b, int c){
        if(a > b){
            a = b;
        }
        if(a > c){
            a = c;
        }
        return a;
    }
}
```

