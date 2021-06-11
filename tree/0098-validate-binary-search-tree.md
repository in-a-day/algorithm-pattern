### [98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

Given the `root` of a binary tree, *determine if it is a valid binary search tree (BST)*.

A **valid BST** is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg)

```
Input: root = [2,1,3]
Output: true
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg)

```
Input: root = [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `-231 <= Node.val <= 231 - 1`



#### **题解**

BST中序遍历得到的结果就是一个升序序列.

```java
class Solution {
    private TreeNode pre;
    public boolean isValidBST(TreeNode root) {
        return helper(root);
    }
    
    private boolean helper(TreeNode root) {
        if (root == null) return true;
        boolean left = helper(root.left);
        if (!left) return false;
        if (pre != null && root.val <= pre.val) return false;
        // 更新前一个节点
        pre = root;
        return helper(root.right);
    }
}
```

迭代判断:

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;
        Stack<TreeNode> s = new Stack<>();
        TreeNode node = root, pre = null;
        boolean isValid = true;
        while (!s.isEmpty() || node != null) {
            if (node != null) {
                s.push(node);
                node = node.left;
            } else {
                node = s.pop();
                // 不是升序返回false
                if (pre != null && node.val <= pre.val) return false;
                // 更新前一个节点
                pre = node;
                node = node.right;
            }
        }
        return true;
    }
}
```

