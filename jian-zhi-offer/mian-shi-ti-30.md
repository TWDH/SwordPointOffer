---
description: 定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。
---

# 面试题30：包含min函数的栈

## 方法一：

1. 栈A为正常的栈，实现正常逻辑
2. 栈B为辅助栈，存储栈A中所有非严格降序的元素， 则栈 AA 中的最小元素始终对应栈 BB 的栈顶元素，即 `min()` 函数只需返回栈 BB 的栈顶元素即可。
3. 函数设计
   * push: 重点为保持栈 B 的元素是 **非严格降序** 的。
     1. 将 x压入栈 A（即 A.add\(x\) ）
     2. 若B为**空**，或x**小于等于**B栈顶元素。将x压入栈B。 
   * pop:  重点为保持栈 A,B 的 **元素一致性**
     1. 执行栈 A 出栈（即 A.pop\(\) ），将出栈元素记为 y ；
     2. 若 y 等于栈 B的栈顶元素，则执行栈 B 出栈（即 B.pop\(\) ） 
   * top:  直接返回栈 A的栈顶元素即可，即返回 `A.peek()` 。 
   *  min**：** 直接返回栈 BB 的栈顶元素即可，即返回 `B.peek()` 。

```java
class MinStack {
    Stack<Integer> A, B;
    /** initialize your data structure here. */
    public MinStack() {
        A = new Stack<>();
        B = new Stack<>();
    }
    
    public void push(int x) {
        A.add(x);
        if(B.empty() || B.peek()>= x){
            B.add(x);
        }
    }
    
    public void pop() {
        if(A.pop().equals(B.peek())){
            B.pop();
        }
    }
    
    public int top() {
       return A.peek();
    }
    
    public int min() {
        return B.peek();
    }
}
```

