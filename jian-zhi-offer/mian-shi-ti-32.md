---
description: 从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。
---

# 面试题32：从上到下打印二叉树

## 方法一：BFS

1. 判断极限情况，`root = null` ，返回0
2. 建立队列 `Queue<TreeNode>`和列表`ArrayList<Integer>`, 并将`root`放入队列中。
3. BSF循环：
   1. `queue`为空时跳出
   2. 出队：将队首元素出队，记为`node` 
   3. 打印：将`node.val`添加至`ArrayList`中备用
   4. 添加子节点：若`node`的左右子节点不为空，则依次添加
4. 将`ArrayList`中的元素，依次输入到数组`res`中。

* `queue.poll()` 删除第一个元素
* `queue.add()` 添加一个元素

```java
class Solution {
    public int[] levelOrder(TreeNode root) {
        if(root == null){
            return new int[0];
        }
        Queue<TreeNode> queue = new LinkedList<>();
        ArrayList<Integer> list = new ArrayList<>();
        queue.add(root);

        while(!queue.isEmpty()){
            TreeNode node = queue.poll();
            list.add(node.val);
            if(node.left != null){
                queue.add(node.left);
            }
            if(node.right != null){
                queue.add(node.right);
            }
        }
        
        int[] res = new int [list.size()];
        for(int i=0; i<list.size(); i++){
            res[i] = list.get(i);
        }
        return res;
    }
}
```

