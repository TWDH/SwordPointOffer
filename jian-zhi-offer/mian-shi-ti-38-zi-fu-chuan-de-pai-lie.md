# 面试题38：字符串的排列

## 方法一：回溯法dfs

排序方案：通过交换字符，固定第1位字符（n种情况），第2位字符（n-1种情况）... 最后固定第n位字符（1种情况）

* 字符数组c：存储给定待排序字母。
* x：当前固定位。
* res：List&lt;String&gt;集合存储结果

1. 终止条件：当`x = len(c)-1`时，代表所有位已固定，将当前组合`c`转化为字符串加入结果`res`。
2. 递推参数：当前固定位`x`。
3. 递推：初始化`Set`，用于排除重复字符。将第`x`个字符（固定位）和`i`交换，后进入下层递归。
   1. 枝剪：若`c[i]`在Set中，代表其是重复字符，因此枝剪。
   2. 将`c[i]`加入Set，以便判断后续重复字符。
   3. 固定字符：将`c[i]`和`c[x]`交换，即固定`c[i]`在第`x`位。
   4. 开启下层递归：调用`dfs(x+1)`，即开始固定第`x + 1`位字符
   5. 交换还原：将`c[i]`和`c[x]`交换

```java
class Solution {
    char[] c;
    List<String> res = new LinkedList<>();
    public String[] permutation(String s) {
        c = s.toCharArray();
        dfs(0);
        return res.toArray(new String[res.size()]);
    }

    public void dfs(int x){
        if(x == c.length - 1){
            res.add(String.valueOf(c)); // 添加排列方案
            return;
        }
        HashSet<Character> set = new HashSet<>();
        for(int i = x; i < c.length; i++){
            if(set.contains(c[i])){
                continue; // 重复，因此剪枝
            }
            set.add(c[i]);  
            swap(x, i); // 交换，将 c[i] 固定在第 x 位
            dfs(x+1); // 开启固定第 x + 1 位字符
            swap(x, i); // 恢复交换

        }
    }

    public void swap(int i, int j){
        char temp = c[i];
        c[i] = c[j];
        c[j] = temp;
    }
}
```

