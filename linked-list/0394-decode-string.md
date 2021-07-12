### [394. Decode String](https://leetcode.com/problems/decode-string/)

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there won't be input like `3a` or `2[4]`.

**Example 1:**

```
Input: s = "3[a]2[bc]"
Output: "aaabcbc"
```

**Example 2:**

```
Input: s = "3[a2[c]]"
Output: "accaccacc"
```

**Constraints:**

- `1 <= s.length <= 30`
- `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
- `s` is guaranteed to be **a valid** input.
- All the integers in `s` are in the range `[1, 300]`.

#### 题解
遍历字符串, 使用栈保存元素:
1. 将字符串中的元素依次入栈,
2. 遇到`]`时, 进行弹栈操作
3. 找到对应的'[', 
4. 记录`[ ]`之间的元素与其需要的重复次数
5. 将重复后的字符串重新入栈
6. 重复以上步骤直到字符串遍历完毕

```java
class Solution {
    public String decodeString(String s) {
        Stack<String> stack = new Stack<>();
        LinkedList<String> lst = new LinkedList();
        for (char t : s.toCharArray()) {
            if (']' == t) {
                String popStr = String.valueOf(stack.pop());
                StringBuilder sb = new StringBuilder();
                while (!"[".equals(popStr)) {
                    lst.addFirst(popStr);
                    popStr = stack.pop();
                }
                while (!lst.isEmpty()) {
                    sb.append(lst.poll());
                }
                // 需要重复的次数
                int repeatTimes = Integer.valueOf(stack.pop());
                String repeatStr = sb.toString();
                StringBuilder r = new StringBuilder();
                for (;repeatTimes > 0; repeatTimes--) {
                    r.append(repeatStr);
                }
                stack.push(r.toString());
            } else {
                stack.push(String.valueOf(t));
            }
        }

        StringBuilder res = new StringBuilder();
        while (!stack.empty()) {
            lst.addFirst(stack.pop());
        }
        while (!lst.isEmpty()) {
            res.append(lst.poll());
        }
        return res.toString();
    }
}
```
