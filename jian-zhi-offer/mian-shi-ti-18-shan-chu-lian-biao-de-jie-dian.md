---
description: 给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。返回删除后的链表的头节点。注意：此题对比原题有改动
---

# 面试题18：删除链表的节点

## 方法一：双指针

1. 特例处理： 当应删除头节点 head 时，直接返回 head.next 即可。
2. 初始化： `pre = head` , `cur = head.next` 。
3. 定位节点： 当 cur 为空 **或** cur 节点值等于 val 时跳出。否则
   1. 保存当前节点索引，即 pre = cur 。
   2. 遍历下一节点，即 cur = cur.next 。
4. 删除节点： 若 cur 指向某节点，则执行 `pre.next = cur.next`。（若 cur 指向 null ，代表链表中不包含值为 val 的节点。）
5. 返回值： 返回链表头部节点 head 即可

```java
class Solution {
    public ListNode deleteNode(ListNode head, int val) {
        if(head.val == val){
            return head.next;
        }
        ListNode pre = head;
        ListNode cur = head.next;
        while(cur.val != val && cur.next != null){
            pre = cur;
            cur = cur.next;
        }
        if(cur != null){
            pre.next = cur.next;
        }
        return head;
    }
}
```

