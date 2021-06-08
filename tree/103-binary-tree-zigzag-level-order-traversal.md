### [103. Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

Given the `root` of a binary tree, return *the zigzag level order traversal of its nodes' values*. (i.e., from left to right, then right to left for the next level and alternate between).



**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[20,9],[15,7]]
```


#### 题解

使用层序遍历，只要每隔一层倒序即可。

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        if (root == null) return new LinkedList<>();
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        List<List<Integer>> res = new LinkedList<>();
        TreeNode node = root;
        int levelLength;
        boolean reverse = false;
        while (!q.isEmpty()) {
            levelLength = q.size();
            LinkedList<Integer> levelList = new LinkedList<>();
            for (;levelLength > 0; levelLength--) {
                node = q.poll();
                if (reverse) levelList.addFirst(node.val);
                else levelList.add(node.val);
                if (node.left != null) q.offer(node.left);
                if (node.right != null) q.offer(node.right);
            }
            reverse = !reverse;
            res.add(levelList);
        }
        return res;
    }
}
```

