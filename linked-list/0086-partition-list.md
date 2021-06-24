### [86. Partition List](https://leetcode.com/problems/partition-list/)

Given the `head` of a linked list and a value `x`, partition it such that all nodes **less than** `x` come before nodes **greater than or equal** to `x`.

You should **preserve** the original relative order of the nodes in each of the two partitions.

 **Example 1:**

![img](https://assets.leetcode.com/uploads/2021/01/04/partition.jpg)

```
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]
```

#### 题解
题目意思其实就是将链表分成两部分: 
1. 小于x的部分lt
2. 大于等于x的部分ge
3. 最终将lt尾节点的next设置为get的首节点
```java
class Solution {
    public ListNode partition(ListNode head, int x) {
        ListNode fakeLtHead = new ListNode(0);
        ListNode fakeGeHead = new ListNode(0);
        ListNode lt = fakeLtHead, ge = fakeGeHead;

        while (head != null) {
            if (head.val < x) {
                lt.next = head;
                lt = lt.next;
            } else {
                ge.next = head;
                ge = ge.next;
            }
            head = head.next;
        }
        lt.next = fakeGeHead.next;
        // ge节点可能存在next节点, 需要将next节点置null
        ge.next = null;

        return fakeLtHead.next;
    }
}
```
