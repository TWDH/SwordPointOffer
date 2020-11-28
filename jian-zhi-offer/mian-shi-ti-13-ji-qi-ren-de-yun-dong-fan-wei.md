# 面试题13： 机器人的运动范围

## 方法一：DFS

1. 创建数组visited标记已经用过的方格
2. DFS：
   1. 越界，不符合K要求，已经visit过的。 返回0，不增加格子的个数。
   2. 标记visited的格子为true
   3. dfs递归，只有**下右**两个方向。到边界时（最后一个符合K的格子），只会是`1+0+0`（增加一个格子），结果依次反向向上传播。

* 计算各个位数之和
  * 首先`%10`得到个位数的数字
  * 将得到的数字`/10`，即将十位右移
  * 直到当前数字为`<=0` 

```java
class Solution {
    public int movingCount(int m, int n, int k) {
        boolean[][] visited = new boolean[m][n];
        return dfs(m, n, 0, 0, visited, k);
    }

    public int dfs(int m, int n, int i, int j,boolean[][] visited, int k){
        if(i >= m || j >= n || sum(i)+sum(j) > k || visited[i][j]){
            return 0;
        }
        visited[i][j] = true;

        int result = 1+ dfs(m, n, i+1, j, visited, k) + dfs(m, n, i, j+1, visited, k);

        return result;
    }

    public int sum(int num){
        int sums = 0;
        while(num != 0){
            sums += num % 10;
            num /=10; 
        }
        return sums;
    }
}
```

