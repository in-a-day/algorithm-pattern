### [124. Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return *the maximum **path sum** of any path*.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg)

```
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg)

```
Input: root = [-10,9,20,null,null,15,7]
Output: 42
Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.
```

**Constraints:**

- The number of nodes in the tree is in the range `[1, 3 * 104]`.
- `-1000 <= Node.val <= 1000`



#### 题解

求最大路径和, 可以求通过每个节点的路径和, 取每个节点的路径和中的最大值即可.

通过一个节点的路径和最大值有以下四种情况:

- 当前节点的值

- 左子树的路径和 + 当前节点值
- 右子树的路径和 + 当前节点值
- 左子树路径和 + 右子树路径和 + 当前节点的值

只需要从以上三种情况中取出最大值即可. 同时使用一个全局变量保存路径和的最大值.



```java
class Solution {
    private int res;
    public int maxPathSum(TreeNode root) {
        res = Integer.MIN_VALUE;
        maxSum(root);
        return res;
    }
    // maxSum(root)的定义是不同是包含左右子树通过当前节点的最大路径和
    // 如果同时包含左右子树导致递归计算父节点时无法使用子节点的路径和
    private int maxSum(TreeNode root) {
        if (root == null) return 0;
        int leftSide = maxSum(root.left);
        int rightSide = maxSum(root.right);
        int oneSideMax = root.val + Math.max(leftSide, rightSide);
        int sideMax = Math.max(oneSideMax, leftSide + rightSide + root.val);
        int max = Math.max(root.val, sideMax);
        if (res < max) res = max;
        // 返回值只能是当前节点值, 或者是通过当前节点的左子树或右子树
        // 不可以是左子树 + 右子树, 这样会有重复路径
        // 例如ex2中的例子来说, 20节点返回时只能返回20 + 15或20 + 7给父节点-10使用
        return Math.max(root.val, oneSideMax);
    }
}
```

