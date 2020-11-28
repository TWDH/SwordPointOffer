# 面试题24：反转链表

## 方法一：链表操作

1. 为防止链表断开，我们需要知道当前的点pNode的前一个节点`pPrev`和后一个节点`pNext`
2. while循环，首先得到`pNode`下一个节点`pNext`备用
3. 如果`pNext==null`，说明已经到链表结尾，直接返回`pReservedHead=pNode`作为反转链表的头节点，否则---&gt;
4. 反转：当前节点`pNode`的下一个节点，设置为`pPrev`。
5. 更新`pPrev`为`pNode`的位置，相当于`pPrev`向后移动一位。
6. 更新`pNode`为之前记录的`pNext`，相当于`pNode`向后移动一位，此时链表不会断。

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pReservedHead = null;
        ListNode pNode = head;
        ListNode pPrev = null;
        
        while(pNode != null){
            ListNode pNext = pNode.next;
            if(pNext == null){
                pReservedHead = pNode;
            }
            pNode.next = pPrev;
            pPrev = pNode;
            pNode = pNext;
        }
        return pReservedHead;
    }
}
```

