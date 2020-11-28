---
description: 输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。
---

# 面试题25：合并两个排序的链表

## 方法一：链表操作

1.  **初始化：** 伪头节点 `dum` ，节点 `cur`指向 `dum`
2.  **循环合并：** 当 `l1​` 或 `l2`​ 为空时跳出
   1. 当`l_1.val < l_2.val`时： cur 的后继节点指定为`l1` ​，并`l1` ​向前走一步
   2. 当`l_1.val > l_2.val`时：cur的后继节点指定为`l2`，并`l2`向前走一步
   3. `cur`节点向前走一步，即`cur = cur.next`
3. 合并剩余的尾部：跳出有两种情况，即`l1`为空或`l2`为空
   1. 若`l1== null`：将`l2`添加至`cur`之后
   2. 反之亦然

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dum = new ListNode(0);
        ListNode cur = dum;

        while(l1 != null && l2 != null){
            if(l1.val < l2.val){
                cur.next = l1;
                l1 = l1.next;
            }
            else{
                cur.next = l2;
                l2 = l2.next;
            }
            cur = cur.next;
        }
        cur.next = l1 == null? l2 : l1;
        return dum.next;
    }
}
```

