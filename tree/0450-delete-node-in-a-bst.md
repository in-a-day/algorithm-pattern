### [450. Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/)

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

**Follow up:** Can you solve it with time complexity `O(height of tree)`?

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/04/del_node_1.jpg)

```
Input: root = [5,3,6,2,4,null,7], key = 3
Output: [5,4,6,2,null,null,7]
Explanation: Given key to delete is 3. So we find the node with value 3 and delete it.
One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.
```

![img](https://assets.leetcode.com/uploads/2020/09/04/del_node_supp.jpg)



#### 题解

首先寻找被删除节点的位置, 根据BST的性质, 删除该节点使用一个节点替换该节点, 可能有以下情况:

- 如果该节点是一个叶子节点, 不需要替换, 直接删除
- 从该节点的左子树中获取最右节点(不一定是叶子节点), 使用该节点替换需要删除的节点
- 从该节点的右子树中获取最左节点(不一定是叶子节点), 使用该节点替换需要删除的节点

```java
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        // node查找需要删除的节点, pre代表需要删除节点的父节点
        TreeNode node = root, pre = null;
        // 需要删除的节点是父节点的左子节点还是右子节点
        boolean isLeft = true;
        while (node != null) {
            if (node.val > key) {
                pre = node;
                isLeft = true;
                node = node.left;
            } else if (node.val < key) {
                pre = node;
                isLeft = false;
                node = node.right;
            } else {
				// 此时node是需要删除的节点, 寻找右子树中的最左节点
                TreeNode leftNodeOfRight = node.right;
                TreeNode preOfLeft = leftNodeOfRight;
                while (leftNodeOfRight != null && leftNodeOfRight.left != null) {
                    preOfLeft = leftNodeOfRight;
                    leftNodeOfRight = leftNodeOfRight.left;
                }
                // 存在右子树
                if (leftNodeOfRight != null) {
                    // 右子树的最小节点就是删除节点的右子节点, 将删除节点的左子树作为该右子节点的左子树即可
                    if (leftNodeOfRight == preOfLeft) {
                        leftNodeOfRight.left = node.left;
                    } else {
                        // 先移除该节点, 将该节点的右子树设置为父节点的左子树
                        preOfLeft.left = leftNodeOfRight.right;
                        leftNodeOfRight.left = node.left;
                        leftNodeOfRight.right = node.right;
                    }
                }
                // 删除的节点是root节点
                if (pre == null) {
                    return leftNodeOfRight == null ? root.left : leftNodeOfRight;
                }
                // 将删除节点的父节点指向新节点
                if (leftNodeOfRight != null) {
                    if (isLeft) pre.left = leftNodeOfRight;
                    else pre.right = leftNodeOfRight;
                } else {
					if (isLeft) pre.left = node.left;
                    else pre.right = node.left;
                }
                return root;
            }
        }
        return root;
    }
}
```

