# Vertical Order Traversal of a Binary Tree

### Metadata

Source: [Leetcode](https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree) <br/>
Solved on: `25 May 2023`

### Problem
Given the root of a binary tree, calculate the vertical order traversal of the binary tree.

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
var verticalTraversal = function(root) {
  if(!root) {
    return [];
  }

  var traverse = function(node, row, col, coord) {
    var entry = {
      row: row,
      val: node.val
    };
    var cols = coord.get(col);
    if(cols) {
      cols.push(entry);
    } else {
      coord.set(col, [entry]);
    }

    if(node.left) {
      traverse(node.left, row + 1, col - 1, coord);
    }

    if(node.right) {
      traverse(node.right, row + 1, col + 1, coord);
    }
  }

  var coord = new Map();
  traverse(root, 0, 0, coord);

  var arr = [];
  for(var entry of coord) {
    arr.push(entry);
  }

  return arr.sort((a, b) => a[0] - b[0]).reduce((memo, i) => {
    var vals = [...i[1]]
      .sort((a, b) => {
        if(a.row !== b.row) {
          return a.row - b.row;
        }

        return a.val - b.val;
      })
      .reduce((memo, i) => {
        memo.push(i.val);
        return memo;
      }, [])

    memo.push(vals);
    return memo;
  }, []);
};
```
