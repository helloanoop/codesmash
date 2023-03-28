# Same Tree

### Metadata

Source: Leetcode <br/>
Solved on: `28 March 2023`



### Problem
Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.

### Constraints

* The number of nodes in both trees is in the range [0, 100].
* -104 <= Node.val <= 104

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
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {boolean}
 */
var isSameTree = function(p, q) {
    const areNodesEqual = (p, q) => {
        if(p && q) {
            return p.val === q.val;
        }

        if(!p && !q) {
            return true;
        }

        return false;
    }

    if(!areNodesEqual(p, q)) {
        return false;
    }

    const walkAndCheck = (p, q) => {
        if(!p && !q) {
            return true;
        }

        if((!p && q) || (p && !q)) {
            return false;
        }

        if(!areNodesEqual(p, q)) {
            return false;
        }
        if(!areNodesEqual(p, q)) {
            return false;
        }

        if(!walkAndCheck(p.left, q.left)) {
            return false;
        }

        if(!walkAndCheck(p.right, q.right)) {
            return false;
        }

        return true;
    };

    return walkAndCheck(p, q);
};
```
