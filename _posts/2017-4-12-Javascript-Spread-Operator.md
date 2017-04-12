---
layout: post
title: Javascript Spread Operator
tags: [javascript]
---

Before we have the `...` spread operator, we rely on the hidden parameter `arguments` to deal with dynamic list of arguments.

Example with the `arguments` property.

```
function sum() {
  let sum = 0;
  for(let i=0; i<arguments.length; i++) {
    sum += arguments[i];
  }
  return sum;
}
```
However, one problem with the above approach is that the `arguments` object is not an array, it's an array-like object, which means we cannot apply array method to it. Therefore, we usually use the call() function to bypass the limitations of the `arguments` object.

```
function sum() {
  let sum = 0;
  Array.prototype.forEach.call(arguments, (num) => {
    sum += num;
  })
  return sum;
}
```
Now comes the life saver `...`. 
```
function sum(...args) {
  let sum = 0;
  args.forEach((num) => {
    sum += num;
  })
  return sum;
}
```
Bonus... for the one-liner lover.
```
function sum(...args) {
  return args.reduce((curr, next) => curr + next);
}
```
