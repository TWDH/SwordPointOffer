---
description: "请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的均摊时间复杂度都是O(1)。若队列为空，pop_front 和 max_value\_需要返回 -1"
---

# 面试题59 - II. 队列的最大值

![](../.gitbook/assets/image%20%2833%29.png)

## 方法一：双端队列deque

1. 创建队列queue和双端队列deque（维护一个递减队列deque）。
2. MaxQueue：求最大值直接返回deque的队首；不存在，返回`-1`。
3. push\_back：
   1. queue：直接在队尾加入新元素value
   2. deque：为了得到maxValue，需要维护一个**递减序列**。所以要删除所有deque中小于value的数值\(`deque.peekLast() < value`\)，因为这些被删除的元素永远不可能成为队列中的最大值。
4. pop\_front：
   1. queue：不存在，返回`-1`；存在，直接移除队首的数值，并保存在qHead中。
   2. deque：如果queue中的要移除的队首元素，正好等于deque的队首元素。表示`最大值=queue[0]=deque[0]`，一旦queue\[0\]移除，deque的队首元素必须移除。因为原queue中的数值都移除了，所以其不可能成为最大值。 

```java
class MaxQueue {
    //1. 创建队列queue和双端队列deque
    Queue<Integer> queue;
    Deque<Integer> deque;

    public MaxQueue() {
        queue = new LinkedList<>();
        deque = new LinkedList<>();
    }
    
    public int max_value() {
        //2.在deque中的第一个就是最大值
        if(deque.isEmpty()){
            return -1;
        }
        return deque.peekFirst();
    }
    
    public void push_back(int value) {
        //3.1在queue队尾加入元素；
        queue.offer(value);
        //3.2加入deque时，将之前其中所有比value小的都移除(需要维持一个递减序列)
        while(!deque.isEmpty() && deque.peekLast() < value){
            deque.removeLast();
        }
        //3.3将新元素value加入deque
        deque.addLast(value);
    }
    
    public int pop_front() {
        //4.0 如果队列不存在，返回-1
        if(queue.isEmpty()){
            return -1;
        }
        //4.1移除queue中的队首
        int qHead = queue.poll();
        //4.如果deque的队首值跟queue中的队首值一样，则将deque中的队首也移除
        if(qHead == deque.peekFirst()){
            deque.removeFirst();
        }
        return qHead;
    }
}

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue obj = new MaxQueue();
 * int param_1 = obj.max_value();
 * obj.push_back(value);
 * int param_3 = obj.pop_front();
 */
```

