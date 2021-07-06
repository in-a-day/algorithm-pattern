### [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

Given the `head` of a singly linked list, return `true` if it is a palindrome.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```
Input: head = [1,2,2,1]
Output: true
```

**Constraints:**

- The number of nodes in the list is in the range `[1, 105]`.
- `0 <= Node.val <= 9`


#### 题解
寻找链表的中点, 同时反转中点及其之前的节点, 并判断该链表长度是奇数还是偶数, 最后按序遍历判断即可.
```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }

        ListNode slow = head, fast = head, pre = null, next;
        // 寻找中点(若是偶数, 中点是靠右侧的节点), 并反转中点前的节点(不包含中点)
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            next = slow.next;
            slow.next = pre;
            pre = slow;
            slow = next;
        }

        // 通过fast是否为null判断出链表长度的奇偶
        if (fast == null) {
            // 长度为偶数, 左右进行判断
            fast = slow;
        } else {
            // 长度为奇数, 跳过中点
            fast = slow.next;
        }

        // 判断是否是回文, 不管奇偶都是从反转链表的头结点开始
        while (pre != null) {
            if (pre.val != fast.val) {
                return false;
            }
            pre = pre.next;
            fast = fast.next;
        }
        return true;
    }
}
```

步骤拆分:
```java
class Solution {
    public boolean isPalindrome2(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        ListNode mid = findMiddle(head);
        ListNode preHalfHead, postHalfHead;
        int len  = len(head);
        preHalfHead = reverse(head, mid);

        postHalfHead = mid;
        if ((len & 1) != 0) {
            postHalfHead = mid.next;
        }

        return isPalindrome(preHalfHead, postHalfHead);
    }

    // 偶数取偏右的中点
    private ListNode findMiddle(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    private int len(ListNode head) {
        ListNode cur = head;
        int count = 0;
        while (cur != null) {
            cur = cur.next;
            count++;
        }
        return count;
    }

    // bound不参与反转
    private ListNode reverse(ListNode head, ListNode bound) {
        ListNode pre = null, cur = head, next;
        while (cur != bound) {
            next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }

    private boolean isPalindrome(ListNode pre, ListNode post) {
        while (pre != null) {
            if (pre.val != post.val) {
                return false;
            }
            pre = pre.next;
            post = post.next;
        }
        return true;
    }
}
```
