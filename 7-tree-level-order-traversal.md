# Tree Order Traversal

### Metadata

Source: [Leetcode](https://leetcode.com/problems/binary-tree-level-order-traversal) <br/>
Solved on: `21 May 2023`

### Problem
Given the `root` of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

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
 * @return {number[][]}
 */
var levelOrder = function(root) {
  if(!root) {
    return [];
  }

  var out = [[root.val]];
  var queue = [root.left, root.right];

  while (queue.length > 0) {
    var currentLevelValues = [];
    var nextLevelNodes = [];

    while (queue.length > 0) {
      var node = queue.shift();

      if(node) {
        currentLevelValues.push(node.val);
        nextLevelNodes.push(node.left);
        nextLevelNodes.push(node.right);
      }
    }

    queue = nextLevelNodes;
    if(currentLevelValues.length) {
      out.push(currentLevelValues);
    }
  }

  return out;
};
```

### ChatGPT Solution
```javascript
function levelOrder(root) {
  if (!root) {
    return []; // Empty tree, return an empty array
  }
  
  const result = [];
  const queue = [root]; // Queue to store nodes for traversal
  
  while (queue.length > 0) {
    const levelSize = queue.length;
    const currentLevel = [];
    
    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift(); // Dequeue the front node
      
      currentLevel.push(node.val); // Add node value to the current level
      
      if (node.left) {
        queue.push(node.left); // Enqueue left child
      }
      
      if (node.right) {
        queue.push(node.right); // Enqueue right child
      }
    }
    
    result.push(currentLevel); // Add the current level to the result
  }
  
  return result;
}
```
