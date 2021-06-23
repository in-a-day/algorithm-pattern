### [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

Given the `head` of a singly linked list, reverse the list, and return *the reversed list*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```

**Constraints:**

- The number of nodes in the list is the range `[0, 5000]`.
- `-5000 <= Node.val <= 5000`



#### 题解

反转链表，需要pre，cur，next三个变量，分别保存前一个节点，当前节点，下一个节点。

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pre = null, cur = head, next;
        while (cur != null) {
            next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
}
```



递归写法：反转链表，只需要依次反转以下一个节点为头结点的链表即可即可

```java
class Solution {
    ListNode newHead;
    public ListNode reverseList(ListNode head) {
        if (head == null) return head;
        helper(head);
        head.next = null;
        return newHead;
    }
    
    
    public ListNode helper(ListNode head) {
        if (head == null || head.next == null) {
            newHead = head;
            return head;
        }
        helper(head.next).next = head;
        return head;
    }
}
```

