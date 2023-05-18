# Add Two Numbers stored as Linked Lists

### Metadata

Source: [Leetcode](https://leetcode.com/problems/add-two-numbers) `Medium` <br/>
Solved on: `18 May 2023`

### Problem
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1**
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.

**Example 2**
Input: l1 = [0], l2 = [0]
Output: [0]

**Example 3**
Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]

### My Solution
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
  var add = function(x, y, c) {
    var sum = x + y + c;

    return sum > 9 ? [sum % 10, 1] : [sum, 0]
  };

  var sum = 0;
  var carry = 0;
  [sum, carry] = add(Number(l1.val), Number(l2.val), 0);

  var list = new ListNode(sum, null);
  var listCpy = list;

  l1 = l1.next;
  l2 = l2.next;

  while(l1 || l2) {
    if(l1 && l2) {
      [sum, carry] = add(Number(l1.val), Number(l2.val), carry);
      listCpy.next = new ListNode(sum, null);
      listCpy = listCpy.next;
      l1 = l1.next;
      l2 = l2.next;
      continue;
    }

    if(l1) {
      [sum, carry] = add(Number(l1.val), 0, carry);
      listCpy.next = new ListNode(sum, null);
      listCpy = listCpy.next;
      l1 = l1.next;
      continue;
    }

    if(l2) {
      [sum, carry] = add(0, Number(l2.val), carry);
      listCpy.next = new ListNode(sum, null);
      listCpy = listCpy.next;
      l2 = l2.next;
      continue;
    }
  }

  if(carry) {
    listCpy.next = new ListNode(1, null);
  }

  return list;
};cd ../
cd code 
```

### ChatGPT Solution
```javascript
var addTwoNumbers = function(l1, l2) {
  let dummy = new ListNode(0);
  let current = dummy;
  let carry = 0;

  while (l1 !== null || l2 !== null) {
    let x = l1 !== null ? l1.val : 0;
    let y = l2 !== null ? l2.val : 0;
    let sum = x + y + carry;
    carry = Math.floor(sum / 10);
    current.next = new ListNode(sum % 10);
    current = current.next;

    if (l1 !== null) l1 = l1.next;
    if (l2 !== null) l2 = l2.next;
  }

  if (carry > 0) {
    current.next = new ListNode(carry);
  }

  return dummy.next;
};
```