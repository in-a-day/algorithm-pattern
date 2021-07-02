### [148. Sort List](https://leetcode.com/problems/sort-list/)

Given the `head` of a linked list, return *the list after sorting it in **ascending order***.

**Follow up:** Can you sort the linked list in `O(n logn)` time and `O(1)` memory (i.e. constant space)?

 **Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

```
Input: head = [4,2,1,3]
Output: [1,2,3,4]
```

#### 题解
quick sort or merge sort
归并由于是指针操作, 则不需要额外空间
```java
class Solution {
    public ListNode sortList(ListNode head) {

    }

    private ListNode sort(ListNode left, ListNode right) {
    }

    private ListNode merge(ListNode ls, ListNode le, ListNode rs, ListNode re) {
        if (ls == le && rs == re) return;
        if (le != null) le.next = null;
        if (re != null) re.next = null;
        ListNode fake = new ListNode(0);
        ListNode head = fake;
        while (ls != le && rs != re) {
            if (ls.val < rs.val) {
                fake.next = ls;
                ls = ls.next;
            } else {
                fake.next = rs;
                rs = rs.next;
            }
            fake = fake.next;
        }
        if (ls != le) fake.next = ls;
        if (rs != re) fake.next = rs;
        return head.next;
    }
}
```
