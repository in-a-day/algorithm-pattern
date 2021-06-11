### [110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the left and right subtrees of *every* node differ in height by no more than 1.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: true
```



#### 题解

判断二叉树是否是高度平衡, 只需要判断左子树与右子树的高度相差不超过1.

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return height(root) != -1;
    }
    // 返回高度, 如果高度相差大于1返回-1代表不是高度平衡的二叉树
	private int height(TreeNode root) {
        if (root == null) return 0;
        int l = height(root.left);
        if (l == -1) return -1;
        int r = height(root.right);
        if (r == -1 || Math.abs(l - r) > 1) return -1;
        return Math.max(l, r) + 1;
    }
}
```

