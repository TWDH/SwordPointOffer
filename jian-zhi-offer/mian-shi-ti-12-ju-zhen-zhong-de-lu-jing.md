---
description: >-
  请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的3×4的矩阵中包含一条字符串“bfce”的路径（路径中的字母用加粗标出）。[["a","b","c","e"],["s","f","c","s"],["a","d"
---

# 面试题12：矩阵中的路径

## **方法一：**回溯法

1. 对目标word进行 `toCharArray()`转换
2. 2个for循环遍历数组
3. DFS
   1. 越界/与目标字符不相符，**False**
   2. 字符查找完毕，**True**
   3. 保存当前`(i,j)`数组中的值为`temp` 
   4. 修改其为不会出现在目标数组的特殊符号`'.'` 
   5. 递归寻找`“上下左右”`四个方向，将找到的答案（True/False）返回给结果result
   6. 将数组的\(i,j\)改回为原来字符，如果此字符所有路都不能寻找到正确数组，方便下次寻找

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        char[] wordArray = word.toCharArray(); // word to math

        for(int i=0; i<board.length; i++){
            for(int j=0; j<board[0].length; j++){
                if(dfs(board, wordArray, i, j, 0)){
                    return true;
                }
            }
        }
        return false;
    }

    public boolean dfs(char[][] board, char[] wordArray, int i, int j, int index){
        if(i<0 || i >= board.length || j<0 || j >= board[0].length || board[i][j] != wordArray[index]){
            return false;
        }

        if(index == wordArray.length-1){
            return true;
        }

        char temp = board[i][j];
        board[i][j] = '.';
        //左右上下
        boolean result = dfs(board, wordArray, i-1, j, index+1) || dfs(board, wordArray, i+1, j, index+1) || 
                         dfs(board, wordArray, i, j-1, index+1) || dfs(board, wordArray, i, j+1, index+1);
        board[i][j] = temp;  

        return result;
    }
}
```

