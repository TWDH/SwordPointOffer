# 面试题55：II. 平衡二叉树

## 方法一：先序遍历（根左右）

1. 根：判断当前root的左右子树深度值是否&lt;1。
2. 左：判断root.left是否为平衡树，返回boolean。
3. 右：判断root.right是否为平衡树，返回boolean。

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root == null){
            return true;
        }

        int LeftDepth = TreeDepth(root.left);

        int RightDepth = TreeDepth(root.right);
        //根
        if(Math.abs(LeftDepth - RightDepth) > 1){
            return false;
        } 
        //左，右
        return isBalanced(root.left) && isBalanced(root.right);
    }
    //判断树
    public int TreeDepth(TreeNode root){
        if(root == null){
            return 0;
        }
        int left = TreeDepth(root.left);
        int right = TreeDepth(root.right);

        return left > right ? (left+1) : (right + 1);
    }
}
```

## 2.方法二：后序遍历（左右根）

1. 左：左子树深度**leftDepth**；或`-1`，代表不平衡。
2. 右：右子树深度**rightDepth**；或`-1`，代表不平衡。
3. 根：判断“左“和”右”两部分的深度相差是否`<1`。
   1. 如果符合条件，返回**该节点的深度**（左右子树中，大的那一支`+1`）。
   2. 如果不符合条件，返回`-1`表示**不平衡**。

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return dfs(root) != -1;
    }

    public int dfs(TreeNode root){
        if(root == null){
            return 0;
        }
        //左
        int leftDepth = dfs(root.left);
        if(leftDepth == -1){
            return -1;
        }
        //右
        int rightDepth = dfs(root.right);
        if(rightDepth == -1){
            return -1;
        }
        //根
        return Math.abs(leftDepth - rightDepth) < 2 ? Math.max(leftDepth, rightDepth) + 1 : -1; 
    }
}
```

