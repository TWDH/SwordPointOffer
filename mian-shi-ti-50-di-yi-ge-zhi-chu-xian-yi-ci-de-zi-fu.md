# 面试题50：第一个只出现一次的字符

## 方法一：HashMap

1. 创建一个HashMap存储：字符\(key\)~出现是否**&lt;=**1次\(value\)
2. 第一次扫描数组，如果未出现过为true（小于等于一次），出现过为false（大于1次）。
3. 第二次扫描，返回第一个true

![](.gitbook/assets/image%20%2820%29.png)

```java
class Solution {
    public char firstUniqChar(String s) {
        HashMap<Character, Boolean> map = new HashMap<>();
        char[] chs = s.toCharArray();
        for(char ch : chs){
            map.put(ch, !map.containsKey(ch));
        }
        for(char ch : chs){
            if(map.get(ch)){
                return ch;
            }
        }
        return ' ';
    }
}
```

