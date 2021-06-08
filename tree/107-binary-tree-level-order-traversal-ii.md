### [107. Binary Tree Level Order Traversal II](https://leetcode.com/problems/binary-tree-level-order-traversal-ii/)

Given the `root` of a binary tree, return *the bottom-up level order traversal of its nodes' values*. (i.e., from left to right, level by level from leaf to root).



**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[15,7],[9,20],[3]]
```



#### 题解

与层次遍历相同，可以在层次遍历结束后，倒序列表，也可以在遍历添加时直接逆序添加。

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        if (root == null) return new LinkedList<>();
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        LinkedList<List<Integer>> res = new LinkedList<>();
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
          	// 由于使用的是LinkedList, 所以首部添加也是O(1)复杂度
            res.addFirst(levelList);
        }
        return res;
    }
}
```

DFS模拟层次遍历，然后倒序列表。

```java
class Solution {
    private List<List<Integer>> res;
  
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        res = new LinkedList<>();
        dfs(root, 0);
        Collections.reverse(res);
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

