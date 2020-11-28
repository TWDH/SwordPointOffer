---
description: 输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)B是A的子结构， 即 A中有出现和B相同的结构和节点值。
---

# 面试题26： 树的子结构

## 方法一：递归

1. 设置变量result
2. 判断两个树A和B都不为空
   1. 若树A和树B的根节点相同，调用`DoesTree1HaveTree2`判断其左右子树是否也相同。
   2. 若`result = false`，表示当前节点A与B不相等，递归树A的左右子树判断是否可行 
3. `DoesTree1HaveTree2`：判断Tree1是否包含Tree2
   1. **\***注意：调用`DoesTree1HaveTree2`的前提条件是，**B的上一个父亲节点与A相同**。如果小树B的根节点为null时，表示**这一支B的父节点都与A相同**，因为B的子节点已经**遍历完成**，**无需再与树A作比较**（这一支），所以**这一支路**\(左or右\)返回**true**。
   2. 如果树A为null，则大的树都遍历完，小的树还没遍历完。不可能相等，返回false。
   3. 如果树A的值与树B不相等，返回false。
   4. 判断树A的左子节点和树B的左子节点是否继续有包含关系，右子节点亦然。

```java
class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        boolean result = false;
        if(A != null & B != null){
            if(A.val == B.val){
                result = DoesTree1HaveTree2(A, B);
            }
            if(!result){
                result = isSubStructure(A.left, B);
            }
            if(!result){
                result = isSubStructure(A.right, B);
            }
        }
        return result;
    }
    public boolean DoesTree1HaveTree2(TreeNode A, TreeNode B){
        if(B == null){
            return true;
        }
        if(A == null){
            return false;
        }
        if(A.val != B.val){
            return false;
        }
        return DoesTree1HaveTree2(A.left, B.left) && DoesTree1HaveTree2(A.right, B.right);
    }
}
```

