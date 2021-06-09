### [701. Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

You are given the `root` node of a binary search tree (BST) and a `value` to insert into the tree. Return *the root node of the BST after the insertion*. It is **guaranteed** that the new value does not exist in the original BST.

**Notice** that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return **any of them**.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/10/05/insertbst.jpg)

```
Input: root = [4,2,7,1,3], val = 5
Output: [4,2,7,1,3,5]
Explanation: Another accepted tree is:
```

![img](https://assets.leetcode.com/uploads/2020/10/05/bst.jpg)



#### **题解**

思路一: 

插入位置只需要找到一个节点: 

- 节点值比需要插入节点值大
- 节点的左孩子节点比需要插入节点值小, 或者该节点不存在左孩子

如果没有找到上述节点, 那么说明需要插入的节点是最大节点, 只要将节点插入最右侧节点的右子树即可.

递归的写法:

```java
class Solution {
    // 保存前一个节点
    private TreeNode pre;
    public TreeNode insertIntoBST(TreeNode root, int val) {
        TreeNode newNode = new TreeNode(val);
        if (root == null) return newNode;
        TreeNode node = findNode(root, val);
        if (node == null) {
            // 此时node是最大值, pre代表了最右侧的节点
            pre.right = newNode;
        } else {
            newNode.left = node.left;
            node.left = newNode;
        }
        return root;
    }
    // findNode寻找给定节点node, node满足一下条件:
    // node.left.val < val, val < node.val 
    // 否则返回null
    private TreeNode findNode(TreeNode root, int val) {
        if (root == null) return null;
        TreeNode left = findNode(root.left, val);
        if (left != null) return left;
        // 前节点为空, 代表此时为树最左侧节点, 只需要判断当前值即可
        if (pre == null && val < root.val) {
            return root;
        }
        if (pre != null && pre.val < val && val < root.val) {
            return root;
        }
        // 更新前一个节点
        pre = root;
        return findNode(root.right, val);
    }
}
```

迭代写法:

```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        TreeNode newNode = new TreeNode(val);
        if (root == null) return newNode;
        Stack<TreeNode> s = new Stack<>();
        TreeNode node = root, pre = null;
        while (!s.isEmpty() || node != null) {
            if (node != null) {
                s.push(node);
                node = node.left;
            } else {
                node = s.pop();
                if (pre == null && val < node.val) {
                    node.left = newNode;
                    return root;
                }
                if (pre != null && pre.val < val && val < node.val) {
                    newNode.left = node.left;
                    node.left = newNode;
                    return root;
                }
                pre = node;
                node = node.right;
            }
        }
        pre.right = newNode;
        return root;
    }
}
```



思路二: 

寻找一个叶子节点, 将新的节点作为叶子节点的左孩子或者右孩子即可.

```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) return new TreeNode(val);
        if (val < root.val) {
            // 小于插入左子树
            root.left = insertIntoBST(root.left, val);
        } else {
            // 大于插入右子树
            root.right = insertIntoBST(root.right, val);
        }
        return root;
    }
}
```

使用二分查找插入的位置:

```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        TreeNode newNode = new TreeNode(val);
		TreeNode node = root;
        while (node != null) {
            if (val < node.val) {
                if (node.left == null) {
                    node.left = newNode;
                    return root;
                }
                node = node.left;
            } else {
                if (node.right == null) {
                    node.right = newNode;
                	return root;
                }
                node = node.right;
            }
        }
        return root;
    }
}
```

