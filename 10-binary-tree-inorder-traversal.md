# Binary Tree Inorder Traversal

### Metadata

Source: [Leetcode](https://leetcode.com/problems/binary-tree-inorder-traversal/) <br/>
Solved on: `30 May 2023`

### Problem
Given the `root` of a binary tree, return the inorder traversal of its nodes' values.

### Notes
In order traversal, for every node
  - traverse left node recursively, note the value
  - traverse up once there is no more left nodes, note the value
  - traverse right, note the value

### Solution
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var inorderTraversal = function(root) {
  if (!root) {
    return [];
  }

  var list = [];
  var traverseInOrder = (node, list) => {
    if(node.left) {
      traverseInOrder(node.left, list);
    }

    list.push(node.val);

    if(node.right) {
      traverseInOrder(node.right, list);
    }
  };

  traverseInOrder(root, list);

  return list;
};
```