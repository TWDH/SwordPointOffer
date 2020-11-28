# 面试题52. 两个链表的第一个公共节点

## 方法一：双指针

1. 设计两个指针指向两个List的头部，其中一个长一个短。计算两者的长度，让长的List的指针向后移动lenDiff个位置，使二者起始“链表长度”相等。
2. 找到的第一个相同节点便是公共节点。
3. 注意if...else：相等的情况放在那一边都可以，因为相等lenDiff就为0了。直接寻找第一个相同的点就好。

```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        int headALength = getListLength(headA);
        int headBLength = getListLength(headB);
        // System.out.print(headALength + headBLength);
        int lenDiff = 0;
        ListNode pListHeadLong = null;
        ListNode pListHeadShort = null;
        
        if(headALength > headBLength){
            pListHeadLong = headA;
            pListHeadShort = headB;
            lenDiff = headALength - headBLength;
        }
        else{
            pListHeadLong = headB;
            pListHeadShort = headA;
            lenDiff = headBLength - headALength;
        }


        //较长的链表向前走lenDiff步
        for(int i = 0; i < lenDiff; i++){
            pListHeadLong = pListHeadLong.next;
        }
        //这里前两个条件可以不写，不然两List遍历完还没有共同点，就没有解。
        while(pListHeadLong != null && pListHeadShort != null && pListHeadLong != pListHeadShort){
            pListHeadLong = pListHeadLong.next;
            pListHeadShort = pListHeadShort.next;
        }

        ListNode result = pListHeadLong;
        return result;      
    }

    public int getListLength(ListNode head){
        int len = 0;
        ListNode Node = head;
        while(Node != null){
            Node = Node.next;
            len++;
        }
        return len;
    }
}
```

