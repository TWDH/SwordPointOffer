---
description: >-
  请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random
  指针指向链表中的任意节点或者 null。
---

# 面试题35：复杂链表的复制



![](../.gitbook/assets/image%20%2816%29.png)

## 方法一：

![](../.gitbook/assets/image%20%282%29.png)

1. 拷贝链表：在原链表后复制一个一模一样的链表
   1. 生成克隆节点cloneNode
   2. 记录原链表下一个节点nextNode
   3. 将原节点head连接克隆节点
   4. 克隆节点再连接原链表下一个节点nextNode
   5. 更新head为nextNode
2. 指定随机指针：
   1. 通过head得到cloneNode
   2. 如果head有random指针的话：
      1. 得到head.random指向的节点direct
      2. 使cloneNode.random等于direct.next
   3. 更新head为nextNode
3. 重新连接：
   1. 得到cloneNode为head.next
   2. 记录cloneHead
   3. 操作，使两个链表分开

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null){
            return null;
        }
        copy(head);
        randomDirect(head);
        return reList(head);
    }

    public void copy(Node head){
        while(head != null){
            Node cloneNode = new Node(head.val);
            Node nextNode = head.next;
            head.next = cloneNode;
            cloneNode.next = nextNode;
            head = cloneNode.next;
        }
    }

    public void randomDirect(Node head){
        while(head != null){
            Node cloneNode = head.next;
            if(head.random != null){
                Node direct = head.random;
                cloneNode.random = direct.next;
            }
            head = cloneNode.next;
        }
    }

    public Node reList(Node head){
        Node cloneNode = head.next;
        Node cloneHead = cloneNode;
        head.next = cloneNode.next;
        head = head.next;
        while(head != null){
            cloneNode.next = head.next;
            head.next = head.next.next;//原始链表的连接路径要完成
            head = head.next;
            cloneNode = cloneNode.next; 
        }
        return cloneHead;
    }
}
```

