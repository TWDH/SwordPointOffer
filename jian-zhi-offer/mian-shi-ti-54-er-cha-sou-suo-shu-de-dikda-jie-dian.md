---
description: 给定一棵二叉搜索树，请找出其中第k大的节点
---

# 面试题54：二叉搜索树的第k大节点

## 方法一：中序遍历（左根右）

1. 因为找第K大的数字，中序遍历是从小到大。我们改变为右根左，变为由大到小。
2. **终止条件：**root为null
3. **递归右子树：**dfs\(root.right\)
4. 实现细节：
   1. 提前返回：`k=0`，代表节点已经找到，无需继续。
   2. **统计序号：**`k = k-1`（找到第K大的值）。
   3. 记录答案：当`k=0`时，节点便是答案，`res = root.val`。
5. 注意：
   1. dfs每次都进入到最后的子树，即当左右子树都为null时，执行此节点中的`k--`操作。不是叶子节点的中间节点，执行完右子树后也会处理root，执行`k--`操作。

```java
class Solution {
    int k, res;
    public int kthLargest(TreeNode root, int k) {
        this.k = k;
        //这里不要引入形参k，dfs中直接使用的是初始值为k
        dfs(root);
        return res;
    }

    public void dfs(TreeNode root){
        if(root == null || k == 0){
            return;
        }
        //右子树
        dfs(root.right);
        //root
        //先--，再判断。因为我们设定k=0时找到答案，已经先进入右子树，即进入第一个节点。
        //代表从右边数第1大的数已经计算。
        k--;
        if(k == 0){
            res = root.val;
        }
        //左子树
        dfs(root.left);
    }
}
```

