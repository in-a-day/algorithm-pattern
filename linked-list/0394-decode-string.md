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
        Stack<Character> stack = new Stack<>();
        LinkedList<Character> lst = new LinkedList();
        char[] chars = s.toCharArray();
        for (char c : chars) {
            if (']' != c) {
                stack.push(c);
            } else {
                lst.clear();
                char cur = stack.pop();
                // 找出[]包围的字符
                while ('[' != cur) {
                    lst.addFirst(cur);
                    cur = stack.pop();
                }
                // 找出需要重复的次数
                cur = stack.pop();
                int repeatTimes = 0;
                for (int i = 1; Character.isDigit(cur); i *= 10) {
                    repeatTimes += i;
                    cur = stack.pop();
                }
                // 将重复字符放入栈中
                for (; repeatTimes > 0; repeatTimes--) {
                    for (char l : lst) {
                        stack.push(l);
                    }
                }
            }
        }
        StringBuilder res = new StringBuilder();
        while (!stack.empty()) {
            res.append(stack.pop());
        }
        return res.reverse().toString();
    }
}
```

使用一个栈保存从'['到']'或者到'['中的字符，另一个栈保存对应需要重复的次数。

```java
class Solution {
    public String decodeString(String s) {
        Stack<StringBuilder> strs = new Stack<>();
        Stack<StringBuilder> nums = new Stack<>();
        strs.push(new StringBuilder());
        nums.push(new StringBuilder());
        for (char c : s.toCharArray()) {
            if (Character.isDigit(c)) {
                nums.peek().append(c);
            } else if (c == '[') {
                strs.push(new StringBuilder());
                nums.push(new StringBuilder());
            } else if (c == ']') {
                int repeatition = Integer.valueOf(nums.pop().toString());
                String repeatStr = strs.peek().toString();
                for (int i = 0; i < repeatition; i++) {
                    strs.peek().append(repeatStr);
                }
                // 当前字符串与前一个字符串合并
                if (strs.size() != 1) {
                    StringBuilder cur = strs.pop();
                    strs.peek().append(cur);
                }
            } else {
                // 字符
                strs.peek().append(c);
            }
        }
        return strs.pop().toString();
    }
}
```

