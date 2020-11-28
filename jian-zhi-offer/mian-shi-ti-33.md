---
description: 输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。
---

# 面试题33：二叉搜索树的后序遍历序列

## 方法一：**递归分治**

1. 终止条件： 当 `i >=j` ，说明此子树节点数量 `<=1` ，无需判别正确性，因此直接返回 `true`
2. 递归
   1. 划分左右子树： 遍历后序遍历的 `[i, j]` 区间元素，寻找 第一个大于根节点 的节点，索引记为 `m`。此时，可划分出左子树区间 `[i,m - 1]` 、右子树区间 `[m, j - 1]`、根节点索引 `j`。
3. 判断是否为二叉搜索树：
   1. 左子树：`[i, m-1]`中的元素都应该小于`postorder[j]`, 上一步划分左右子树时已经保证了左子树的正确性，所以只需要判断右子树就可以了。
   2. 右子树：`[m, j-1]`中的元素都应该大于`postorder[j]`, 判断是否为二叉搜索树的条件是，`p = j`。（用来判断**该子树**是否正确）

```java
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        return recur(postorder, 0, postorder.length - 1);
    }

    public boolean recur(int[] postorder, int i, int j){
        if(i >= j){
            return true;
        }
        int p = i;
        while(postorder[p] < postorder[j]){
            p++;
        }
        int m = p;
        while(postorder[p] > postorder[j]){
            p++;
        }
        return p == j && recur(postorder, i, m-1) && recur(postorder, m, j-1);
    }
}
```

