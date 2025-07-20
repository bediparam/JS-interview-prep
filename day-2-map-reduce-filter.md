So this is day 2 for me on covering all the basics required to prepare for js interview. Today I am going to cover Array methods - Map, Filter and Reduce.

## Map

So, Map is an array method used to create a new array by applying a function to each element of the input array.

```javascript
const nums = [1, 2, 3, 4];

const multipliedTwo = nums.map((val, index, arr) => {
  return val * 2;
});

console.log(multipliedTwo); // [ 2, 4, 6, 8 ]
```

## Filter

Filter is an array method used to apply condition on each element of the input array and keep the ones that satisfies the condition.

```javascript
const evenNums = nums.filter((val) => {
  return val % 2 == 0;
});

console.log(evenNums); // [ 2, 4 ]
```

## Reduce

Reduce is an array method that Calls the specified callback function for all the elements in an array. The return value of the callback function is the accumulated result, and is provided as an argument in the next call to the callback function.

```javascript
const sum = nums.reduce((acc, val) => {
  return acc + val;
}, 0);

console.log(sum); // 10
```

Before diving into some interview questions, lets understand prototype feature provided by js.

Array.prototype is a core js feature that refers to the object from which all js arrays inherit.

**Note:** Array inherits from array.prototype which inherits from Object.prototype.

## Interview Questions based on prototype, map, filter and reduce

### Write a polyfill for map function?

Note: Polyfill means a function manually written for a functionality that is not supported on older web browsers.

```javascript
Array.prototype.myMap = function (callBackFn) {
  let result = [];
  for (let i = 0; i < this.length; i++) {
    result.push(callBackFn(this[i], i, this));
  }
  return result;
};

const multipliedThree = nums.myMap((val) => {
  return val * 3;
});
```

### write a polyfill for filter function?

```javascript
Array.prototype.myFilter = function (callBackFn) {
  let result = [];
  for (let i = 0; i < this.length; i++) {
    if (callBackFn(this[i], i, this)) result.push(this[i]);
  }
  return result;
};

const oddNums = nums.myFilter((val) => {
  return val % 2 !== 0;
});
```

### write a polyfill for reduce function?

```javascript
Array.prototype.myReduce = function (callBackFn, initialValue) {
  let acc = initialValue;
  for (let i = 0; i < this.length; i++) {
    acc = acc ? callBackFn(acc, this[i], i, this) : this[i];
  }
  return acc;
};

const sumNums = nums.myReduce((acc, val) => {
  return acc + val;
});
```

## Differences btw map and forEach?

Map is used to return a new array where as forEach is used to iterate through array and doesn't return anything.
We can chain array functions on map whereas not possible through forEach.

```javascript
const isMoreThan3Multiple = nums
  .map((val) => {
    return val * 2;
  })
  .filter((val) => val > 3);
```

### Write a function to return total of students marks after 20 marks are added to the students less than 60.

```javascript
let students = [
  { name: "param", rollNumber: 25, marks: 80 },
  { name: "srijan", rollNumber: 37, marks: 73 },
  { name: "shitiz", rollNumber: 38, marks: 15 },
  { name: "arun", rollNumber: 1, marks: 11 },
];

console.log(
  students.reduce((acc, stu) => {
    let newVal = stu.marks < 60 ? stu.marks + 20 : stu.marks;
    return acc + newVal;
  }, 0)
);
```
