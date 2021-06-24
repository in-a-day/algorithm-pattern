### [92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)

Given the `head` of a singly linked list and two integers `left` and `right` where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return *the reversed list*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg)

```
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]
```

**Constraints:**

- The number of nodes in the list is `n`.
- `1 <= n <= 500`
- `-500 <= Node.val <= 500`
- `1 <= left <= right <= n`


#### 题解
由于题目中限制了left, right取值, 所以可以去除一些边界判断
```java
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if (left == right || head == null) {
            return head;
        }
        ListNode cur = head, preOfLeft = null;
        for (int i = 1; i < left; i++) {
            // left节点的前一个节点, 最后将该节点的next指向rightNode
            preOfLeft = cur;
            cur = cur.next;
        }
        // 保存leftNode, 最后指向rightNode的next节点
        ListNode leftNode = cur, pre = null, next;
        for (int j = left; j <= right; j++) {
            next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        leftNode.next = cur;
        if (preOfLeft == null) {
          return pre;
        }
        preOfLeft.next = pre;
        return head;
    }
}
```
