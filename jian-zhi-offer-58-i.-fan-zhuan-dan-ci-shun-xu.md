---
description: >-
  输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student.
  "，则输出"student. a am I"。
---

# 面试题58 - I. 翻转单词顺序

## 方法一：分隔+倒序

1. 先使用`trim()`删除头尾空字符。
2. 将字符串String使用`split(" ")`，按单词存入字符串数组str。
3. 注意：如果两个单词之间有多个空格，在使用StringBuilder添加字符时，跳过（continue）。
4. StringBuilder在组成答案是，因为单词间有空格，所以需要在最后`+“ ”`。
5. 返回StringBuilder -&gt; String，使用`toString()`。删除头尾空字符。

```java
class Solution {
    public String reverseWords(String s) {
        //trim()：删除头尾空字符
        //split(" ")：以空格作为分隔标准
        //1.得到每个字符组成的String数组
        String[] str = s.trim().split(" ");
        
        StringBuilder sb = new StringBuilder();
        for(int i = str.length - 1; i >= 0; i--){
            //2.若词之间多余一个空格，则str[i]数组中则存在“”（里面什么都没有）的数值
            if(str[i].equals("")){
                continue;
            }
            //3.倒序组成新的StringBuilder
            sb.append(str[i] + " ");
        }
        //返回为String形式，并删除头尾空字符（因为sb后面每个都加了一个“ ”）
        return sb.toString().trim();
    }
}
```

## 2.方法二：双指针

1. 设置两个指针i\(前\)，j\(后\)。使其可以包括住一个单词
2. 获取单词：j不动，如果当前字符**不是空格（有字符）**，则向前移动i。直到移动到字符前的一个空格。此时将该字符加入StringBuilder。
3. 
```java
class Solution {
    public String reverseWords(String s) {
        //1.删除前后空格
        String str = s.trim();
        StringBuilder sb = new StringBuilder();
        //2.初始化i,j两个指针
        int i = s.length() - 1;
        int j = i;
        while(i >= 0){
            //必须加入i>=0，因为如果这时i已经等于-1了，则出现错误。
            while(i >= 0 && s.charAt(i) != ' '){ //这里注意char用单引号
                i--;
            }
            sb.append(s.substring(i + 1, j + 1) + " ");

            while(i >= 0 && s.charAt(i) == ' '){
                i--;
            }
            j=i;
        }
        return sb.toString().trim();
    }
}
```

