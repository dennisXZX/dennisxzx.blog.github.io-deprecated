---
layout: post
title: Binary Search
categories: [algorithm]
---

It's time to pick up my algorithmic power. Let's start with binary search.

Key points:

1. identify the low and high positions
2. calculate the middle position and retrieve the element in that position
3. compare the retrieved element with the item that need to be found
4. Return the element if it's matched, or update the low or high position according to the comparison result

Here is the code in Javascript to implement binary search.

```
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

function binarySearch(array, item) {
	let low = 0;
	let high = array.length - 1;

	// while you haven't narrowed it down to one element
	while (low <= high) {
		// find the middle element
		let mid = Math.floor((low + high) / 2);
		let guess = array[mid];
		
		if (guess === item) {
			return mid;
		} 
		if (guess > item) {
			high = mid - 1;
		} else {
			low = mid + 1;
		}
	}
	// if the item is not in the array, returns -1
	return -1;
}

console.log(binarySearch(arr, 5));
console.log(binarySearch(arr, 1));
console.log(binarySearch(arr, 0));
```