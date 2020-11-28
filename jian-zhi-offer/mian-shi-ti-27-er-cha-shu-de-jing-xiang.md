---
description: 请完成一个函数，输入一个二叉树，该函数输出它的镜像。
---

# 面试题27： 二叉树的镜像

## 方法一：干换

1. 如果root=null，或左右子树都为null，此时返回root
2. 交换左右子树
3. 递归左子树和右子树

```java
class Solution {
    public TreeNode mirrorTree(TreeNode root) {
        if(root == null){
            return root;
        }
        if(root.left == null && root.right == null){
            return root;
        }
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        
        if(root.right != null){
            mirrorTree(root.right);
        }

        if(root.left != null){
            mirrorTree(root.left);
        }
        return root;
    }
}
```

