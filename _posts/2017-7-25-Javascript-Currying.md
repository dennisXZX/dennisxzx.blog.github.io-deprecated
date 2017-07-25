---
layout: post
title: Javascript Currying
categories: [Javascript]
---

Currying has been one of the topics that baffled me for a long time. In order to truly understand it I have written an example and let's walk it through.

```
function curry(fn) {
  // store the slice method
  const slice = Array.prototype.slice;
	// store the arguments except for the first one
	// equivalent to calling arguments.slice(1)
  const stored_args = slice.call(arguments, 1);    
  
  return function () {
    // equivalent to calling arguments.slice()
    let new_args = slice.call(arguments);
    let args = stored_args.concat(new_args);               
    return fn.apply(null, args);
  }
}

function add(x, y) {
  return x + y;
}

var addFive = curry(add, 5);

addFive(10);
```

When the line `var addFive = curry(add, 5);` is executed, the following happens:

1. slice variable stores a reference to the slice method from the Array prototype.
2. stored_args variables stores an all the arguments except for the function, which is 5.
3. returns a function, which has access to slice and stored_args variables through closure.

When the line `addFive(10);` is executed, the following happens:

1. new_args stores all the arguments, which is 10.
2. args stores values from both stored_args and args, which is 5 and 10.
3. returns the result of a function call using `apply` with all the arguments.

So the concept of currying is it stores the parameters you pass to it for later use, when it receives all the parameters it then call the original function with the help of `apply`.

The best time to use currying is when you find yourself calling a function and passing it mostly the same parameters each time, then the function is a good candidate for currying. You can create a new function by partially applying a set of arguments, so this newly created function will store the repeated parameters and pre-fill the full list of arguments the original function expects.