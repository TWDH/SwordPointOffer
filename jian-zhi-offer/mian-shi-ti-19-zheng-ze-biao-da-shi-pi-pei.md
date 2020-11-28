# 面试题19：正则表达式匹配

## 方法一：动态规划

1. `s`表示待匹配字符，`p`表示正则表达式
2. 求出s, p的字符串长度m, n
3. 创建动态规划数组`boolean f[m+1][n+1]` 
4. 双for循环遍历m，n
   1. 如果`p[j] == "*"` ，“_**字母 + \***_ ” 的组合只可能出现以下两种情况
      * “_**字母 + \***_ ” 匹配 s末尾的一个字符，将s中字符扔掉，字母星号组合还可以继续匹配s中的字符
      *  “_**字母 + \***_ ” 不匹配字符，则字母星号组合扔掉 
   2. 如果`p[j] != "*"` 
      * 如果匹配成功 `s[i] = p[j-1]` 
        * `f[i][j] = f[i - 1][j - 1]`  
      * 如果匹配失败 `s[i] = p[j-1]`
        * `f[i][j] = f[i][j - 2]` 
5. 匹配函数matches
   1. 参数（s，p，i，j）
   2. i=0时，直接返回false
   3. `p[j-1] = '.'`则匹配成功返回true
   4. 返回`s[i-1] == p[j-1]` 

![](../.gitbook/assets/image%20%2819%29.png)

![](../.gitbook/assets/image%20%2829%29.png)

* 只有`j`需要在for循环中操作字符串`p`的内容，所以`j-1`是必要的的，而`i`则是在matches函数中体现（字符串需要`-1`的操作）
* `f[i][j]`是对动态规划数组进行的操作，其中增加了`f[0][0]`的初始状态（如图所示）。而当dp操作`[i][j]`时，实际上是对应到真正字符串中的`[i-1][j-1]`索引的操作，所以需要有`-1`操作
* `||`的原因：

![](../.gitbook/assets/image%20%2834%29.png)

```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length();
        int n = p.length();
        boolean[][] f = new boolean[m+1][n+1];
        f[0][0] = true;

        //2.
        for(int i=0; i<=m; i++){
            for(int j=1; j<=n; j++){
                //判断字符串中的(j-1)其实就是dp中的dp[i][j]的j是不是“*”
                if(p.charAt(j-1) == '*'){
                    f[i][j] = f[i][j-2]; //没有匹配上

                    if(matches(s, p, i, j-1)){ //如果s跟p中*前面的字母匹配上了
                        //这里||的原因：
                        //!如果s中的字符，已经跟p中的上一个字符匹配成功，那么这次的p中的第二个字符一定成功，
                        //因为p中的第二个字符有*，可以等于0
                        //例如在第一列，当s中的第一个再次匹配到相同的字符时，
                        //*的作用应该是让第二次匹配到的字符（数量）=0；
                        //因为上文代码中已经使f[i][j] = f[i][j-2]，即此次*匹配=0，继续使用上次匹配的结果。
                        //即如果f[i][j-2]=Ture,则f[i][j]=Ture.
                        f[i][j] = f[i-1][j] || f[i][j]; //只要一个为True即可
                    }
                }
                else{
                    if(matches(s, p, i, j)){
                        f[i][j] = f[i-1][j-1];
                    }
                }
            }
        }
        return f[m][n];
    }
    public boolean matches(String s, String p, int i, int j){
        if(i == 0){
            return false;
        }
        if(p.charAt(j-1) == '.'){
            return true;
        }

        return s.charAt(i-1) == p.charAt(j-1);
    }
}
```

```java
class Solution {
   public boolean isMatch(String s, String p) {
        int n = s.length();
        int m = p.length();
        // dp[i][j]表示s的前i个和p的前j个能否匹配
        boolean[][] dp = new boolean[n + 1][m + 1];
        for (int i = 0; i < n+1; i++) {
            for (int j = 0; j < m+1; j++) {
                // 如果正则表达式为空
                if (j == 0){
                    dp[i][j] = i == 0;
                }else {
                    if (p.charAt(j - 1) != '*'){
                        if ( i > 0 && (s.charAt(i - 1) == p.charAt(j - 1) || p.charAt(j - 1) == '.')){
                            dp[i][j] = dp[i - 1][j - 1];
                        }
                    }else {
                        // 匹配0个
                        if (j >= 2){
                            dp[i][j] = dp[i][j - 2];
                        }
                        // 正则串不动，主串向前挪一步
                        if (i > 0 && j >= 2 && (s.charAt(i - 1) == p.charAt(j - 2) || p.charAt(j - 2) == '.')){
                            dp[i][j] |= dp[i-1][j];
                        }
                    }
                }
            }
        }
        return dp[n][m];
    }
}
```

