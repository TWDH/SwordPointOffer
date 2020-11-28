---
description: 输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。
---

# 面试题55：二叉树的深度

## 方法一：递归

1. 如果当前节点为null，则返回0。
2. 如果**左子树**的深度比**右子树大**，则返回**左子树+1**，表示现在树的深度。反之亦然。
3. 若左右两子树**深度相同**，返回**任意**一边+1都可以。

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }

        int nLeft = maxDepth(root.left);
        int nRight = maxDepth(root.right);

        int result = nLeft > nRight? (nLeft + 1) : (nRight + 1);
        return result;
    }
}
```



