---
description: 输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。
---

# 面试题36：二叉搜索树与双向链表

![](../.gitbook/assets/image%20%286%29.png)

## 方法一：DFS

1. 初始化空节点pre, head。
2. **dfs中序遍历：**
   1. 终止递归条件：当前节点cur为空，则return。
   2. **递归左子树：**`dfs(cur.left)`。
   3. **构建链表：**
      1. 当pre为空时：表示正在访问表头，记为head。
      2. 当pre不为空时：修改双向节点引用，`pre.right = cur`, `cur.right = pre`； 即左=右，右=左。
      3. 更新`pre`，即`pre=cur`，节点cur是后继节点的pre
   4. **递归右子树：**`def(cur.right)`
3. 前后首尾相接，此时`pre`在整个链表末尾

```java
class Solution {
    Node pre, head;
    public Node treeToDoublyList(Node root) {
        if(root == null){
            return null;
        }
        dfs(root);
        head.left = pre;
        pre.right = head;
        return head;
    }
    public void dfs(Node cur){
        if(cur == null){
            return;
        }
        dfs(cur.left);
        if(pre != null){
            pre.right = cur; //pre的下一个节点是cur
        }
        else{
            head = cur; // head头节点为cur
        }
        cur.left = pre; //cur的上一个节点是pre
        pre = cur;
        dfs(cur.right);
    }
}
```

