---
description: 输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）
---

# 面试题6：从未到头打印链表

## **方法一：**栈

* 典型"后进先出"模式，使用栈

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public int[] reversePrint(ListNode head) {
        //1.创建栈
        Stack<ListNode> stack = new Stack<ListNode>();
        ListNode temp = head;
        //2.遍历链表
        while(temp != null){
            stack.push(temp);
            temp = temp.next;
        }
        //3.打印
        int size = stack.size();
        int [] print = new int[size];
        for(int i=0; i<size; i++){
            print[i] = stack.pop().val;
        }
        return print;
    }
}
```



