---
description: >-
  在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于
  0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？
---

# 面试题47：礼物的最大价值

![](../.gitbook/assets/image.png)

## 方法一：动态规划

1. 设 `f(i, j)` 为从棋盘左上角走至单元格 `(i ,j)` 的礼物最大累计价值
   * `f(i,j)`等于 `f(i,j-1)`和 `f(i-1,j)`中的较大值加上当前单元格礼物价值 `grid(i,j)` 。
   * `f(i,j)= max[f(i,j−1),f(i−1,j)]+grid(i,j)`  
2. **状态定义：**设动态规划矩阵 dp，`dp(i,j)`代表从棋盘的左上角开始，到达单元格 `(i,j)` 时能拿到礼物的最大累计价值。
3. **转移方程：**
   1. 当 i = 0且 j = 0时，为起始元素；
   2. 当 i = 0i=0 且 j !=0 时，为矩阵第一行元素，只可从左边到达；
   3. 当 i ! =0 且 j = 0 时，为矩阵第一列元素，只可从上边到达；
   4. 当 i !=0 且 j !=0 时，可从左边或上边到达；
4. **初始状态：**
   1.  `dp[0][0] = grid[0][0]`  
5.  **返回值：** 

   1. `dp[m-1][n-1]` 

![](../.gitbook/assets/image%20%284%29.png)

![](../.gitbook/assets/image%20%2817%29.png)

```java
class Solution {
    public int maxValue(int[][] grid) {
        int row = grid.length;
        int col = grid[0].length;

        for(int i=0; i < row; i++){
            for(int j=0; j < col; j++){
                if(i == 0 && j == 0){ //初始位置
                    continue;
                }
                else if(i == 0 && j != 0){ //第一行
                    grid[i][j] += grid[i][j-1];
                }
                else if(j == 0 && i != 0){ //第一列
                    grid[i][j] += grid[i-1][j];
                }
                else{ //其他情况
                    grid[i][j] += Math.max(grid[i][j-1], grid[i-1][j]);
                }
            }
        }
        return grid[row-1][col-1];
    }
}
```

