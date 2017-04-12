---
layout: post
title: Functional Programming in Javascript
tags: [javascript]
---

Below is a simple example to illustrate the power of functional programming. The calculator() function returns a doOperation() function, which returns itself. This design pattern makes the function chain call possible.

doOperation() function takes 3 parameters, a function representing the operation, an operand and an optional callback function. I start to see the beauty of functional programming in Javascript!

```
// define operations: add, multiply, subtract
const add = (a, b) => a + b;
const multiply = (a, b) => a * b;
const subtract = (a, b) => a - b;

// define the calculator function
function calculator() {
    let total = 0;
    function doOperation(operation, operand, /* optional */ callback) {
        total = operation(total, operand);
        if(callback) {
            callback(total);
        }
        return doOperation;
    }
    return doOperation;
}

calculator()
    (add, 3)
    (multiply, 5)
    (subtract, 6, function(result) {
        console.log(result);
    });
```