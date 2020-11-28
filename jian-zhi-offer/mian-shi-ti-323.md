---
description: 请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。
---

# 面试题32-3：从上到下打印二叉树 III

## 方法一：deque

1. 当“res层”为偶数时（第0层），在deque中`addLast()`队列中元素（正序存入下一层的元素）
2. 当“res层”为奇数时（第1层），在deque中`addFirst()`队列中元素（倒序存入下一层的元素）

![](../.gitbook/assets/image%20%2832%29.png)

比如res = {{3}}, size=1；则此时res为奇数，添加下一层时{20，9}使用`addFirst()` 

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();
        if(root != null){
            queue.add(root);
        }
        while(!queue.isEmpty()){
            LinkedList<Integer> temp = new LinkedList<>();
            for(int i=queue.size(); i>0; i--){
                TreeNode node = queue.poll();
                if(res.size() % 2 == 0){
                    temp.addLast(node.val);
                }
                else{
                    temp.addFirst(node.val);
                }
                if(node.left != null){
                    queue.add(node.left);
                }
                if(node.right != null){
                    queue.add(node.right);
                }
            }
            res.add(temp);
        }
        return res;
    }
}
```

## 方法二：**层序遍历 + 双端队列（奇偶层逻辑分离）**

\*\*\*\*

