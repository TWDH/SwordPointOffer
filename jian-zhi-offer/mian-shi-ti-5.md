---
description: 请实现一个函数，把字符串 s 中的每个空格替换成"%20"。
---

# 面试题5：替换空格

## **方法一：**

* ```java
  class Solution {
      public String replaceSpace(String s) {
          if (s.length() == 0 || s == null) {
              return "";
          }
          StringBuilder result = new StringBuilder();
          for(char c : s.toCharArray()){  // toCHarArray:返回一个字符数组,该字符数组中存放了当前字符串中的所有字符
              if(c == ' '){
                  result.append("%20");
              }
              else{
                  result.append(c);
              }
          }
          return result.toString();
      }
  }
  ```

