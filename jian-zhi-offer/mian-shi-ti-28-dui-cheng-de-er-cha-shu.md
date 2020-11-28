---
description: 请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。
---

# 面试题28：对称的二叉树

## 方法一：干判断

1. 看**左子树的左边**和**右子树的右边**是否相等
2. 看**左子树的右边**和**右子树的左边**是否相等

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return isSymmetrical(root, root);
    }

    public boolean isSymmetrical(TreeNode root1, TreeNode root2){
        if(root1 == null && root2 == null){
            return true;
        }
        if(root1 == null || root2 == null){
            return false;
        }
        if(root1.val != root2.val){
            return false;
        }
        //此时只有当前节点相等，才会判断其(左右)子节点是否相等
        return isSymmetrical(root1.left, root2.right) && isSymmetrical(root1.right, root2.left);
    }
}
```

