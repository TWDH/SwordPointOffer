# 面试题58 - II. 左旋转字符串

## 1.方法一：字符串切片

1. 使用`string.substring(a,b)`，**左闭右开**。

```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        return s.substring(n, s.length()) + s.substring(0, n);
    }
}
```

## 2.方法二：**列表遍历拼接**

1. 利用取余，从第n个开始，遍历字符串。

```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        StringBuilder sb = new StringBuilder();
        for(int i = n; i < n + s.length(); i++){
            sb.append(s.charAt(i % s.length()));
        }
        return sb.toString();
    }
}
```



