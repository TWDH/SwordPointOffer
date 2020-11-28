# 面试题32-2：从上到下打印二叉树 II

## 方法一: BFS

1. 注意分层遍历时，可以用for循环控制每层输出的大小（多少）

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        List<List<Integer>> list = new ArrayList<>();
        if(root != null){
            queue.add(root);
        }
        //bfs
        while(!queue.isEmpty()){
            List<Integer> temp = new ArrayList<>();
            //分层遍历
            for(int i=queue.size(); i>0; i--){
                TreeNode node = queue.poll();
                temp.add(node.val);
                if(node.left != null){
                    queue.add(node.left);
                }
                if(node.right != null){
                    queue.add(node.right);
                }
            }
            list.add(temp);         
        }
        return list;
    }
}
```

