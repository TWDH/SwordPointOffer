---
description: 输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。
---

# 面试题17：打印从1到最大的n位数

## 方法一：转为字符串

1. 创建StringBuilder str，并向其中填入`'0'` 
2. 如果str中表示的数字，还没有到达最大的n位数。则把str左侧的'0'全部取出，留下右侧非零区域来输出。
   1. while中每次判断str时，如果没有到达最大的n位数，会先取出`末尾字符+1` 
      * 末尾是 `>'9'`时，会将其换成`'0'` , 改变字符串str
      * 末尾 `<=‘9’`时，直接赋值`末尾字符+1`  , 改变字符串str
   2. 因为是for循环，如果进位则看更高一位，`+1`然后**break**。如果不进位，直接`+1`然后**break**

* increment函数
  * True：已经到达最大的n位数（进位了）
  * False：还没有到达最大的n位数，还可以继续输出
  * 若发生进位则一直进行for循环，直到不产生进位则break。如果i为0（即到了最高位）还发生了进位，则设置isOverflow为true，并返回至主函数的while判断。

```java
class Solution {
    public int[] printNumbers(int n) {
        int[] result = new int[(int)(Math.pow(10,n))-1];
        StringBuilder str = new StringBuilder();
        

        for(int i=0; i<n; i++){
            str.append('0');
        }
        int count =0;
        while(!increment(str)){
            //去除str左侧的0
            int index = 0;
            
            if(index < str.length() && str.charAt(index) == '0'){
                index++;
            }
            String s_res = str.toString().substring(index);
            result[count] = Integer.parseInt(s_res);
            count++;
        }
        return result;
    }

    public boolean increment(StringBuilder str){
        boolean Overflow = false;
        for(int i=str.length()-1; i >= 0; i--){
            char s = (char)(str.charAt(i) + 1);

            if(s > '9'){
                str.replace(i, i+1, "0");
                //判断是否到达最大的n位数
                if(i == 0){
                    Overflow = true;
                }
                
            }
            else{
                str.replace(i, i+1, String.valueOf(s));
                break;
            }
        }
        return Overflow;
    }
}
```

