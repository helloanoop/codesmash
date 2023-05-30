# Minimum Depth of Binary Tree

### Metadata

Source: [Leetcode](https://leetcode.com/problems/minimum-depth-of-binary-tree) <br/>
Solved on: `30 May 2023`

### Problem
Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

### Solution
```javascript
var minDepth = function(root) {
  if(!root) {
    return 0;
  }

  var minDepth = 1;
  var queue = [root.left, root.right];

  while(queue.length) {
    var nextQueue = [];
    var n1;
    var n2;

    while(queue.length) {
      n1 = queue.shift();
      n2 = queue.shift();

      if(!n1 && !n2) {
        break;
      }

      if(n1) {
        nextQueue.push(n1.left);
        nextQueue.push(n1.right);
      }
      if(n2) {
        nextQueue.push(n2.left);
        nextQueue.push(n2.right);
      }
    }

    if(!n1 && !n2) {
      break;
    }

    minDepth++;
    queue = nextQueue;
  }

  return minDepth;
};
```

### Recursive Solution
```javascript
var minDepth = function(root) {
  if (root === null) {
    return 0;
  }
  
  if (root.left === null && root.right === null) {
    return 1;
  }
  
  var min = Infinity;
  
  if (root.left) {
    min = Math.min(min, minDepth(root.left));
  }
  
  if (root.right) {
    min = Math.min(min, minDepth(root.right));
  }
  
  return min + 1;
};
```