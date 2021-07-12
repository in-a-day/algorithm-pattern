Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.



**Example 1:**

```
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
```


#### 题解
使用Java的Stack并记录最小值
```java
class MinStack {
    private final Stack<Pair> s;
    /** initialize your data structure here. */
    public MinStack() {
        s = new Stack<>();
    }
    
    public void push(int val) {
        int min = s.empty() ? val : Math.min(val, getMin());
        s.push(new Pair(val, min));
    }
    
    public void pop() {
        s.pop();
    }
    
    public int top() {
        return s.peek().val;
    }
    
    public int getMin() {
        return s.peek().min;
    }

    private class Pair {
        int val;
        int min;

        Pair(int val, int min) {
            this.val = val;
            this.min = min;
        }
    }
}
```

自定义使用链表实现Stack
```java
class MinStack {
    private Node node;
    
    public MinStack() {
    }

    public void push(int val) {
        if (node == null) {
            node = new Node(val, val);
        } else {
            Node newNode = new Node(val, Math.min(getMin(), val));
            // 每次将新节点设为头结点
            newNode.next = node;
            node = newNode;
        }
    }

    public void pop() {
        node = node.next;
    }

    public int top() {
        return node.val;
    }

    public int getMin() {
        return node.min;
    }

    private class Node {
        int val;
        int min;
        Node next;
        Node(int val, int min) {
            this.val = val;
            this.min = min;
        }
    }
}

```



