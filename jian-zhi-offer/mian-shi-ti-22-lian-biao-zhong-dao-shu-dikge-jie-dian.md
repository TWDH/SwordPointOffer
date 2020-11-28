# 面试题22： 链表中倒数第k个节点

## 方法一：双指针

1. 设置前后两个指针`pAhead`和`pBehind` 
2. 让第一个指针`pAhead`先向前走`(k-1)`步。此时前后两个指针差`(k-1)`步
3. 第二个指针指`pBehind`向头节点，同时移动两个指针，直到第一个指针`pAhead`到达末尾
4. 此时第二个指针`pBehind`正好为答案
5. 注意：
   1. 头节点为空，整个链表为空
   2. k=0
   3. k的值**大于**节点数

```java
class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        if(head == null || k == 0){
            return null;
        }

        ListNode pAhead = head;
        ListNode pBehind = null;
        
        for(int i=0; i<k-1; i++){
            if(pAhead.next != null){
                pAhead = pAhead.next;
            }
            else{
                return null;
            }
        }
        pBehind = head;
        while(pAhead.next != null){
            pAhead = pAhead.next;
            pBehind = pBehind.next;
        }
        return pBehind;
    }
}
```

