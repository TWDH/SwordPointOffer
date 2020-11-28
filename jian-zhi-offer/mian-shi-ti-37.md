---
description: 请实现两个函数，分别用来序列化和反序列化二叉树。
---

# 面试题37：序列化二叉树

![](../.gitbook/assets/image%20%2814%29.png)

## 方法一：层序遍历 BFS

### 1.序列化

1. **特例处理：**如果root为空，则返回空列表`“[]”`     
2. **初始化：**队列`queue`（包含根节点**root**）；序列化列表`res`；
3. **层序遍历：**判定条件 --- `queue`为空跳出
   1. 节点出队，记为node
   2. 若`node`不为空：
      1. 在res中加入`node.val` 
      2. 将左右子节点加入`queue` 
   3. 若`node`为空：
      1. 在res中加入`“null”` 
4. 返回值：拼接链表用`‘，’`隔开

### 2.反序列化

1. **特例处理：**若data为空，直接返回null。
2. **初始化：**
   1. 序列化列表`vals`，指针`i=1`，根节点`root`（值为vals\[0\]）
   2. 队列queue（包含root）
3. **按层构建：**
   1. 节点出队，记为node
   2. 构建node的左子节点：`node.left`的值为`vals[i]`，并将`node.left`入队。
   3. i = i + 1
   4. 构建node的右子节点：`node.right`的值为`vals[i]`，并将`node.right`入队。
   5. i = i + 1
4. **返回值：**
   1. 返回根节点

## 注意：

1. `StringBuilder`使用**append** 
2. `substring`包含第一个，**不**包含**最后一个** 

```java
public class Codec {
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if(root == null){
            return "[]";
        }
        StringBuilder res = new StringBuilder("[");
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while(!queue.isEmpty()){
            TreeNode node = queue.poll();
            if(node != null){
                res.append(node.val + ",");
                queue.add(node.left);
                queue.add(node.right);
            }
            else{
                res.append(null + ",");
            }
        }
        res.deleteCharAt(res.length() - 1);
        res.append("]");

        return res.toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if(data.equals("[]")){
            return null;
        }
        String[] vals = data.substring(1, data.length() -1).split(",");
        TreeNode root = new TreeNode(Integer.parseInt(vals[0]));
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        int i = 1;
        while(!queue.isEmpty()){
            TreeNode node = queue.poll();
            if(!vals[i].equals("null")){
                node.left = new TreeNode(Integer.parseInt(vals[i]));
                queue.add(node.left);
            }
            i++;

            if(!vals[i].equals("null")){
                node.right = new TreeNode(Integer.parseInt(vals[i]));
                queue.add(node.right);
            }
            i++;
        }
        return root;
    }
}
```

