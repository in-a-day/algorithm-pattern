### [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree)

Given the `root` of a binary tree, return *its maximum depth*.

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**

```
Input: root = [3,9,20,null,null,15,7]
Output: 3
```

![leetcode 104](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)_leetcode-104_



#### **题解**

寻找最大深度, 只要取左子树最大深度和右子树最大深度的最大值 + 1即可.

递归DFS, 时间复杂度O(n), 空间复杂度O(n):

```java
class Solution {
    public int maxDepth(TreeNode root) {
		if (root == null) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```

使用层级遍历, 最大深度即最大层级, 时间复杂度O(n), 空间复杂度O(n):

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        TreeNode node;
        int level = 0, levelLength;
        while (!q.isEmpty()) {
            level++;
            levelLength = q.size();
            for (;levelLength > 0; levelLength--) {
                node = q.poll();
                if (node.left != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
        }
        return level;
    }
}
```



