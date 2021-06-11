### [102. Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal)

Given the `root` of a binary tree, return *the level order traversal of its nodes' values*. (i.e., from left to right, level by level).

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]
```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-1000 <= Node.val <= 1000`



#### 题解
层级遍历，使用队列进行遍历。
```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        if (root == null) return new LinkedList<>();
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        List<List<Integer>> res = new LinkedList<>();
        TreeNode node = root;
        int levelLength;
        while (!q.isEmpty()) {
            levelLength = q.size();
            List<Integer> levelList = new LinkedList<>();
            for (;levelLength > 0; levelLength--) {
                node = q.poll();
                levelList.add(node.val);
                if (node.left != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
            res.add(levelList);
        }
        return res;
    }
}
```
DFS模拟层级遍历：
```java
class Solution {
    private List<List<Integer>> res;

    public List<List<Integer>> levelOrder(TreeNode root) {
        res = new LinkedList<>();
        dfs(root, 0);
        return res;
    }

    private void dfs(TreeNode root, int level) {
        if (root == null) return;
        // 首次进入层级添加该层级的list
        if (level == res.size()) {
            res.add(new LinkedList<>());
        }
        res.get(level).add(root.val);
        dfs(root.left, level + 1);
        dfs(root.right, level + 1);
    }
}
```
