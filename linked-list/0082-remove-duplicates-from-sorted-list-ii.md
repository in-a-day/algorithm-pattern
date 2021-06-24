### [82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

Given the `head` of a sorted linked list, *delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list*. Return *the linked list **sorted** as well*.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

```
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg)

```
Input: head = [1,1,1,2,3]
Output: [2,3]
```

**Constraints:**

- The number of nodes in the list is in the range `[0, 300]`.
- `-100 <= Node.val <= 100`
- The list is guaranteed to be **sorted** in ascending order.


#### 题解
删除所有重复元素，只保留出现一次的元素。
```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode fakeNode = new ListNode(0);
        fakeNode.next = head;
        ListNode pre = fakeNode;
        while (head != null && head.next != null) {
            if (head.val == head.next.val) {
                head = head.next;
                if (head.next == null) {
                    pre.next = null;
                    re	turn fakeNode.next;
                }
                if (head.val != head.next.val) {
                    // 例: 1 1 2 2, 将指针设置到2位置
                    head = head.next;
                }
                pre.next = head;
            } else {
                head = head.next;
                pre = pre.next;
            }
        }
        return fakeNode.next;
    }
}
```
