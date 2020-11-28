---
description: >-
  在一个 n * m
  的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
---

# 面试题4：二维数组中的查找

## **方法一：**

1. 选取数组中右上角的数，如果是要查找的数字则直接返回true
2. 如果该数字大于要查找的数字，则提出这个数字所在的列
3. 如果该数字小于要查找的数字，则提出这个数字所在的行

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if(matrix.length==0 || matrix[0].length==0){
            return false;
        }

        boolean found = false;
        int row_len = matrix.length;
        int col_len = matrix[0].length; 

        int row = 0;
        int column = col_len - 1;
        
        while(row < row_len && column >= 0){
            if(matrix[row][column] == target){
                found = true;
                break;
            }
            else if(matrix[row][column] > target){
                column--;
            }
            else{
                row++;
            }
        }
        return found;
    }
}
```

