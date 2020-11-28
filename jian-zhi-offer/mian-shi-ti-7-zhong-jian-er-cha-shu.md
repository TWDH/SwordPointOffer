---
description: 输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。
---

# 面试题7：重建二叉树

## **方法一：**递归

1. 判断树是否为null
2. 使用Map建立inorder中数字\(value\)和索引\(index\)的关系
3. 递归调用rebuildTree重建树
   1. 判断preorderStart &lt; preorderEnd
   2. 判断preorderStart == preorderEnd
   3. 当preorderStart &lt; preorderEnd
      * 从前序遍历中找到root
      * 在中序遍历中找到root对应的index
      * 在中序遍历中找到左右子节点的个数leftNodeNum, rightNodeNum
      * 循环调用rebuildTree得到左右子树结构，每次调用时根据左右子树更新preorder, inorder起始，结束的指针位置

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        //1.判断树是否存在
        if(preorder == null || preorder.length == 0){
            return null;
        }
        //2.树的长度
        int length = preorder.length;
        //3.创建Map，中序遍历(数字，索引)
        Map<Integer, Integer> indexMap = new HashMap<Integer, Integer>();
        for(int i=0; i<length; i++){
            indexMap.put(inorder[i], i);
        }
        //4.递归重建树
        TreeNode root = rebuildTree(preorder, 0, length-1, inorder, 0, length-1, indexMap);
        return root;
    }
    public TreeNode rebuildTree(int[] preorder, int preorderStart, int preorderEnd, int[] inorder, int inorderStart, int inorderEnd, Map<Integer, Integer> indexMap){
        //1.树重建完成
        if(preorderStart > preorderEnd){
            return null;
        }
        //2.找到inorder中root的索引
        int rootValue = preorder[preorderStart];
        TreeNode root = new TreeNode(rootValue);
        //2.1 如果头尾指针相等，当前节点便是最后一个叶子节点
        if(preorderStart == preorderEnd){
            return root;
        }
        //2.2 如果树还有子节点
        else{
            int rootIndex = indexMap.get(rootValue);
            //2.2.1得到左右子节点个数
            int leftNodeNum = rootIndex - inorderStart;
            int rightNodeNum = inorderEnd - rootIndex;
            //2.2.2 得到左右子树结构，更新指针位置
            TreeNode leftsubTree = rebuildTree(preorder, preorderStart+1, preorderStart+leftNodeNum, inorder, inorderStart, rootIndex-1, indexMap);
            TreeNode rightsubTree = rebuildTree(preorder, preorderEnd-rightNodeNum+1, preorderEnd, inorder, rootIndex+1, inorderEnd, indexMap);

            root.left = leftsubTree;
            root.right = rightsubTree;

            return root;
        }
    }
}
```

