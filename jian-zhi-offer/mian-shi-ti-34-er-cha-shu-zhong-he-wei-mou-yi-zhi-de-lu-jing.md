---
description: 输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。
---

# 面试题34：二叉树中和为某一值的路径

## 方法一：回溯法

1. 创建储存**答案**的链表`res`，和记录**路径**的`path`。
2. 当`root==null`时，**返回**，证明到树的叶子节点。
3. 将当前节点`root`加入到路径`path`中，并在目标`tar`中减去当前`root.val`。
4. 当`tar`（sum）的值为0且左右没有子树时，`path`即为最终答案，加入到`res`中。
5. 依次递归左右子树
6. 删除path中的当前节点。（当一个节点root遍历完左右子树后，总是要将自己删除掉）

![](../.gitbook/assets/image%20%2831%29.png)

```java
class Solution {
    List<List<Integer>> res = new LinkedList<>();
    LinkedList<Integer> path = new LinkedList<>(); //这里左面为什么不可以List<Integer>???

    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        recur(root, sum);
        return res;
    }
    public void recur(TreeNode root, int tar){
        if(root == null){
            return;
        }
        path.add(root.val);
        tar -= root.val;

        if(tar == 0 && root.left == null && root.right == null){
            res.add(new LinkedList(path));
        }
        recur(root.left, tar);
        recur(root.right, tar);
        path.removeLast();
    }
}
```

