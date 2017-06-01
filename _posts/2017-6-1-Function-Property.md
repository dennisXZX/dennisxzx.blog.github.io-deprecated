---
layout: post
title: Function Property
categories: [Javascript]
---

Since in Javascript, function is nothing but object, so it's natural for a function to have properties. However, many of us might think why on earth we should ever add properties to a function?

Let's take the following two examples to illustrate how function property can help us to store functions in a collection and achieve memoization.

### Storing functions

```
var store = {
    nextId: 1,
    cache: {}, // cache is an object to store unique functions
    add: function(fn) {
        // if the fn does not have an id property
        // that means it's not in the cache object
        if (!fn.id) {
            fn.id = this.nextId++;
            this.cache[fn.id] = fn; // place the function into cache
            return true;
        } else {
            return false;
        }
    }
};

function ninja1(){
    console.log('ninja1');
}

function ninja2(){
    console.log('ninja2');
}

store.add(ninja1); // function is added
store.add(ninja1); // function is not added as it's already in the cache
store.add(ninja2); // function is added
    
// call all the functions in cache
for (let prop in store.cache) {
    store.cache[prop](); // 'ninja1', 'ninja2'
}       
```

### Memoization

```
function isPrime(value) {
		// initialize the answers object if there isn't one
    if (!isPrime.answers) {
        isPrime.answers = {};
    }

		// check if the result is already in answers object
    if (isPrime.answers[value] !== undefined) {
        return isPrime.answers[value];
    }

    var prime = value !== 1;

		// calculate the prime
    for (var i = 2; i < value; i++) {
        if (value % i === 0) {
            prime = false;
            break; 
        }
    }
    
		// store the result into answers object
    isPrime.answers[value] = prime;

		return prime;
}

// calculate the result and stores it in answers object
console.time("app");
console.log(isPrime(104729));
console.timeEnd('app');

// fetch the result form answers object
console.time("app");
console.log(isPrime(104729));
console.timeEnd('app');
```