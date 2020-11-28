---
description: 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。
---

# 面试题29：顺时针打印矩阵

## 方法一：模拟，边界判断

1. 判断边界情况，matrix为`null`，或者长宽为0
2. 计算matrix长宽
3. 建立一个相同的矩阵visited，用于记录已访问过点
4. 计算total，当后面for走过的路径长度跟total一样时，遍历完成
5. 建立directions，`{{0,1}, {1,0}, {0,-1}, {-1,0}}` 为`→↓←↑`的顺序。
6. 建立directionIndex 指定向`→↓←↑`哪个方向走
7. 建立result，用于结果输出
8. 建立for循环遍历整个matrix
   1. 将当前点存入`result`中
   2. 将当前点在`visited`中设为已用过的点
   3. 提前计算出nextRow 和 nextCol分别是多少。
   4. 如果超过边界，或者在visited已经用过；则directions更换下一个方法
   5. row和col更新到下一个点的位置
9. 返回result

```java
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        if(matrix == null || matrix.length == 0 || matrix[0].length == 0){
            return new int[0];
        }
        int row_len = matrix.length;
        int col_len = matrix[0].length; 
        boolean[][] visited = new boolean[row_len][col_len];
        int total = row_len * col_len;
        int[][] directions = {{0,1}, {1,0}, {0,-1}, {-1,0}};
        int directionIndex = 0;
        int row = 0;
        int col = 0;
        
        int[] result = new int[total];

        for(int i=0; i<total; i++){

            result[i] = matrix[row][col];
            visited[row][col] = true;
            int nextRow = row + directions[directionIndex][0];
            int nextCol = col + directions[directionIndex][1];

            if(nextRow < 0 || nextRow >= row_len || nextCol < 0 || nextCol >= col_len || visited[nextRow][nextCol]){ //注意=号
                directionIndex = (directionIndex + 1) % 4; //因为总是→↓←↑的顺序转
            }
            row = row + directions[directionIndex][0];
            col = col + directions[directionIndex][1];
        }
        return result;
    }
}
```

