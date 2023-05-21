# Symmetric Tree

### Metadata

Source: [Leetcode](https://leetcode.com/problems/symmetric-tree) <br/>
Solved on: `21 May 2023`

### Problem
Given the `root` of a binary tree, check whether it is a mirror of itself (i.e., symmetric around its center).

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
 * @return {boolean}
 */
var isSymmetric = function(root) {
  if(!root) {
    return true;
  }

  var isNodeSymmetric = function(n1, n2) {
    if(!n1 && !n2) {
      return true;
    }

    if((n1 && !n2) || (!n1 && n2)) {
      return false;
    }

    if(n1.val !== n2.val) {
      return false;
    }

    return isNodeSymmetric(n1.left, n2.right) && isNodeSymmetric(n1.right, n2.left);
  };

  return isNodeSymmetric(root.left, root.right);
};
```

### ChatGPT Solution
Feeling great today! ChatGPT solution and my solution was the same.

### ChatGPT Solution (Iterative Approach)
```javascript
function isSymmetric(root) {
  if (!root) {
    return true; // Empty tree is considered symmetric
  }
  
  // Create a queue to store pairs of nodes for comparison
  const queue = [];
  queue.push(root.left, root.right);
  
  while (queue.length > 0) {
    const node1 = queue.shift();
    const node2 = queue.shift();
    
    if (!node1 && !node2) {
      continue; // Both nodes are null, continue with the next pair
    }
    
    if (!node1 || !node2) {
      return false; // One of the nodes is null, they are not symmetric
    }
    
    if (node1.val !== node2.val) {
      return false; // Values of the nodes are different, they are not symmetric
    }
    
    // Push pairs of nodes for comparison in the next iteration
    queue.push(node1.left, node2.right);
    queue.push(node1.right, node2.left);
  }
  
  return true; // All nodes are symmetric
}
```
