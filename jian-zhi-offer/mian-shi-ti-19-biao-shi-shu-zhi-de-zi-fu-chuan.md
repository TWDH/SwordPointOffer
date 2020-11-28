# 面试题20：表示数值的字符串

## 方法一：

1. 判断`s=null` 和 s的长度为0
2. 标记**数字**，**点**，**E** 是否出现
   * numSeen
   * dotSeen
   * eSeen
3. 字符串 -&gt; 前后去除空格\(`.trim()`\) -&gt; 转为`toCharArray()` 
4. 主体部分
   1. 判断str\[i\] 是否在 0~9之间，numSeen = true
   2. 判断str\[i\] 会否为 `‘.’`， dotSeen = True，`‘.’`之前不能出现 dotSeen \| eSeen 
   3. 判断str\[i\] 是否为 `e | E` ，eSeen = True，e之前不能出现`e`，**必须**出现数 。重置`numSeen=false`（排除123e或者123e+的情况,确保e之后也出现数）
   4. 判断str\[i\] 是否为`‘-’` or `‘+’` ，如果前一位不是`‘0’ or ‘e’ or ‘E’`，则非法。
   5. 其他不合法字符，返回false
5. 返回numSeen

```java
class Solution {
    public boolean isNumber(String s) {
        if(s == null || s.length() == 0){
            return false;
        }
        boolean numSeen = false;
        boolean dotSeen = false;
        boolean eSeen = false;
        char[] str = s.trim().toCharArray();
        for(int i=0; i<str.length; i++){
            if(str[i] >= '0' && str[i] <= '9'){
                numSeen = true;
            }
            else if(str[i] == '.'){
                if(dotSeen || eSeen){
                    return false;
                }
                dotSeen = true;
            }
            else if(str[i] == 'e' || str[i] == 'E'){
                if(eSeen || !numSeen){
                    return false;
                }
                eSeen = true;
                numSeen = false;
            }
            else if(str[i] == '-' || str[i] == '+'){
                //同时不满足才是非法的
                if(i != 0 && str[i-1] != 'e' && str[i-1] != 'E'){
                    return false;
                }
            }
            else{
                return false;
            }
        }
        return numSeen;
    }
}
```

