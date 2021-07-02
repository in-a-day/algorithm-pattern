### [143. Reorder List](https://leetcode.com/problems/reorder-list/)

You are given the head of a singly linked-list. The list can be represented as:

```
L0 → L1 → … → Ln - 1 → Ln
```

*Reorder the list to be on the following form:*

```
L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
```

You may not modify the values in the list's nodes. Only nodes themselves may be changed.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/04/reorder1linked-list.jpg)

```
Input: head = [1,2,3,4]
Output: [1,4,2,3]
```

### 题解 TODO 递归解法
找到链表的中点, 将后续的节点反转, 从head遍历每个一个节点插入反转后的节点即可.
```java
class Solution {
    public void reorderList(ListNode head) {
        if (head == null || head.next == null) {
            return;
        }
        // 找中间节点
        ListNode mid = findMid(head);
        // 反转后续节点
        ListNode tail = reverse(mid.next);
        // 避免奇数个节点出现死循环
        mid.next = null;
        // 按序合并
        merge(head, tail);
    }
    
    private ListNode findMid(ListNode head) {
        ListNode slow = head;
        ListNode fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    private ListNode reverse(ListNode head) {
        ListNode pre = null, cur = head, next;
        while (cur != null) {
            next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }

    private void merge(ListNode head, ListNode tail) {
        ListNode cur = head, next;
        while (tail != null) {
            next = tail.next;
            tail.next = cur.next;
            cur.next = tail;
            tail = next;
            cur = cur.next.next;
        }
    }
}
```

