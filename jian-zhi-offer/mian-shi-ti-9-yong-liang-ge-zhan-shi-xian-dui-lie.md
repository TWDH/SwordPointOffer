---
description: "用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead\_操作返回 -1 )来源：力扣（LeetCode）链接：https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie"
---

# 面试题9：用两个栈实现队列

## 方**法一：**双栈

* 把stack1放到stack2中其先后顺序就相反了，实现**先进先出**的队列规律
* 如：stack2为空，stack1不为空
  * 将stack1中的数据pop送入stack2中 
* 如：stack2为空，（stack1也为空）
  * 返回-1 
* 如：stack2不为空，（stack1可为空/不空，无所谓）
  * 返回stack2.pop\(\)的数据 \(此时先把之前送入stack2的数据清理干净，等到stack2为空时再操作stack1\)

```java
class CQueue {
    Deque<Integer> stack1;
    Deque<Integer> stack2;

    public CQueue() {
        stack1 = new LinkedList<Integer>();
        stack2 = new LinkedList<Integer>();
    }
    
    public void appendTail(int value) {
        stack1.push(value);
    }
    
    public int deleteHead() {
        //1.stack2为空，且stack1不为空
        if(stack2.isEmpty()){
            while(!stack1.isEmpty()){
                stack2.push(stack1.pop());
            }
        }
        //2.如果stack2为空，stack1为空
        if(stack2.isEmpty()){
            return -1;
        }
        //3.stack2不为空
        else{
            int deleteValue = stack2.pop();
            return deleteValue;
        }
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```

