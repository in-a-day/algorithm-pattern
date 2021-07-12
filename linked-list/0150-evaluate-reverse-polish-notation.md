### [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

Evaluate the value of an arithmetic expression in [Reverse Polish Notation](http://en.wikipedia.org/wiki/Reverse_Polish_notation).

Valid operators are `+`, `-`, `*`, and `/`. Each operand may be an integer or another expression.

**Note** that division between two integers should truncate toward zero.

It is guaranteed that the given RPN expression is always valid. That means the expression would always evaluate to a result, and there will not be any division by zero operation.

 

**Example :**

```
Input: tokens = ["10","6","9","3","+","-11","*","/","*","17","+","5","+"]
Output: 22
Explanation: ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```

**Constraints:**

- `1 <= tokens.length <= 104`
- `tokens[i]` is either an operator: `"+"`, `"-"`, `"*"`, or `"/"`, or an integer in the range `[-200, 200]`.

#### 题解
后缀表达式, 使用栈保存操作数, 遇到操作符进行弹栈
```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> s = new Stack<>();
        for (String t : tokens) {
            if ("+".equals(t)) {
                s.push(s.pop() + s.pop());
            } else if ("-".equals(t)) {
                s.push(-s.pop() + s.pop());
            } else if ("*".equals(t)) {
                s.push(s.pop() * s.pop());
            } else if ("/".equals(t)) {
                int a = s.pop(), b = s.pop();
                s.push(b / a);
            } else {
                s.push(Integer.valueOf(t));
            }
        }
        return s.pop();
    }
}
```
