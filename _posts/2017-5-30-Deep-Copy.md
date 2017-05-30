---
layout: post
title: Deep Copy in Javascript
categories: [Javascript]
---

You may run into situations that require to perform a deep copy of an Javascript object. Below is some commonly used approaches.

1. Use the built-in JSON.stringify() and JSON.parse(). This works for most of the situations but fails on Date() object.

```
var copyObj = JSON.parse(JSON.stringify(obj));
```

2. Use the [cloneDeep() function](https://lodash.com/docs/4.17.4#cloneDeep) in lodash library

```
var objects = [{ 'a': 1 }, { 'b': 2 }];
var copyObj = _.cloneDeep(objects);
```

3. Use the [extend() function](https://api.jquery.com/jquery.extend/) in jQuery library.

```
var copyObj = jQuery.extend(true, {}, oldObject);
```

4. Use VanillaJS to implement a deep copy.

```
function clone(objectToBeCloned) {
  // ff the parameter is not an object, just returns it.
  if (!(objectToBeCloned instanceof Object)) {
    return objectToBeCloned;
  }

  let objectClone;
  
  // Filter out special objects.
  const Constructor = objectToBeCloned.constructor;

  switch (Constructor) {
    // Implement other special objects here.
    case RegExp:
      objectClone = new Constructor(objectToBeCloned);
      break;
    case Date:
      objectClone = new Constructor(objectToBeCloned.getTime());
      break;
    default:
      objectClone = new Constructor();
  }
  
  // Clone each property.
  for (let prop in objectToBeCloned) {
    objectClone[prop] = clone(objectToBeCloned[prop]);
  }
  
  return objectClone;
}
```

