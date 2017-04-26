---
layout: post
title: Selection Sort
categories: [algorithm]
---

Let's look at the selection sort, which has a big O notation of `O(n^2)`. It's not the fastest sorting algorithm, but it paves the way to understand more complicated sorting solutions.

Key points:

1. loop through the array
1. find smallest or biggest number from an array and store its position
2. add it to a new array
3. delete the number in the stored position from the array

Here is the code in Javascript to implement selection sort.

```
const arr = [5, 3, 6, 2, 10];

function findTheSmallestPos(arr) {
	let smallest = arr[0];
	let smallestPos = 0;

	// iterate through the array to find the smallest element
	for(let i = 1; i < arr.length; i++) {
		if(arr[i] < smallest) {
			smallest = arr[i];
			smallestPos = i;
		}
	}

	return smallestPos;
}

function selectionSort(array) {
	let newArray = [];
	let length = array.length;
	// loop through the array
	for(let i = 0; i < length; i++) {		
		// find the position of the smallest value
		let smallestPos = findTheSmallestPos(array);
		// add the smallest value to the new array
		newArray.push(array[smallestPos]);
		// remove it from the array
		array.splice(smallestPos, 1);
	}
	return newArray;
}

console.log(selectionSort(arr));
```