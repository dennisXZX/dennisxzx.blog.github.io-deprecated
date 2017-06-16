---
layout: post
title: Module Pattern vs Module Reveal Pattern
categories: [Javascript]
---

There has been some confusion on the difference between module pattern and module reveal pattern. They are largely the same.

The module pattern dictates the following:

- Private members live in the closure.
- Public members are exposed in a return object.

While the module reveal pattern enhances it by making the return object an object literal with no function definitions.

### Module Pattern

```
const o = {
    const privateVariable1;
    const privateVariable2;
    
    function privateFunc1() {

    }

    return {
        // function is declared in the return object
        test1: function() {

        },
        test2: function() {

        }
    }
}
```

### Module Reveal Pattern

It is conventional to prefix private variable and function names with '_' to distinguish them from the public ones.

```
const o = {

    const _privateVariable1;
    const _privateVariable2;
    
    function _privateFunc1() {

    }

    function test1() {
        _privateFunc1();
    }

    function test2() {
        _privateFunc1();
    }

    return {
        test1: test1,
        test2: test2
    }
}
```