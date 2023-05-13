# Unique items in array

### Problem
Find unique items in an array

### My Solution
```javascript
var arr = [
  { name: "John", age: 25 },
  { name: "Jane", age: 30 },
  { name: "John", age: 25 },
  { name: "Mary", age: 35 },
  { name: "Jane", age: 30 },
  { name: "anoop", age: 20 }
];

var areEqual = function(o1, o2) {
  return JSON.stringify(o1) === JSON.stringify(o2);
}

var uniqArr = [];
while(arr.length) {
  var item = arr[0];
  var arrLength = arr.length;
  
  arr = arr.filter(function(i) {
     return !areEqual(item, i);
  });
  
  if((arrLength - arr.length) === 1) {
    uniqArr.push(item);
  }
}

console.log(uniqArr);
```

### ChatGPT Solution
```javascript
var arr = [
  { name: "John", age: 25 },
  { name: "Jane", age: 30 },
  { name: "John", age: 25 },
  { name: "Mary", age: 35 },
  { name: "Jane", age: 30 },
  { name: "anoop", age: 20 }
];

var uniqueElements = [...new Set(arr.map(item => JSON.stringify(item)))].map(item => JSON.parse(item));

console.log(uniqueElements);
```