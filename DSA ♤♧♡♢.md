	
### Big 0
==Big O notation is a method of analyzing an algorithms performance. 2 main factors that we consider for this are time and space complexity.==
1. Time complexity
	1. Hardware limitations are ignored.
	2. always look at the big picture, recognizing patterns is more important.
	3. constants and static values are ignored.
		1. O(1) constant, O(n) linear, O(n2) quadratic & O(logn) logarithmic.
2. Space complexity

This algorithms has a time and space complexity of O(n).
```javascript
function sumNumbersUpToN(n) {
  let sum = 0;
  for (let i = 1; i <= n; i++) {
    sum += i;
  
  return sum;
}

console.log(sumNumbersUpToN(5));
```

This algorithms time and space complexity of O(1).
```javascript
function sumNumbersUpToNFormula(n) {
  return (n * (n + 1)) / 2;
}

console.log(sumNumbersUpToNFormula(5));
```

---

#### Performance of Arrays & Objects.

==Push and Pop operations on an array have a time complexity of O(1), while shift and unshift have a O(n) has pushing new elements to the start or middle of an array means that we need to reposition all the proceeding elements in a array.==

==Objects have a time complexity of O(1) when we are accessing, inserting or modifying properties, while searching from the elements while take O(n) amount of time.==

---
### Problem Solving Patterns.

##### Algorithms?
A process of set of steps to accomplish a certain task.
#### Problem Solving strategies.

#### Devise a plan to solving a problems, finding an strategy.

1. **Understanding the problem.**
	1. Can I restate the problem?
	2. what are the inputs that go into the problem?
	3. what are the expected output to the problem?
	4. Can the output be derived from the input?
	5. Labelling the important pieces.
2. **Explore Concrete examples**
3. **Break it down**
	1. Explicitly write down the steps you need to take ( very useful ), also writing these in an interview will give you an edge as you will be explaining your thought process.
4. **Solve or Simplify**
5. **Look back & Refactor**
	1. Are you getting the expected result?
	2. Can you understand it at a glance ( not possible all the time though ).
	3. Can you improve the performance ( bigO ) ?
	4. How have other people solved it?

---
### Master common problem solving patterns.

1. **Frequency counter method**
	In the frequency counter method, you count the occurrences of elements in a collection and then compare the frequencies and the values of corresponding elements in two arrays. This approach avoids using nested loops and eliminates the need to delete values.

	For example, if you have a function that takes two arrays as input and checks whether each element in the first array has a corresponding element in the second array that is the square of its value. Instead of iterating through both arrays with nested loops, you can follow these steps:

	1. **Count Frequencies:** Count the frequencies of each unique element in both arrays.
	2. **Compare Frequencies:** Check if the square of each element in the first array has the same frequency in the second array.
    
	By doing this, you efficiently determine if every element in the first array has a matching element in the second array whose value is the square of the original element. This method is more efficient than using nested loops, especially for large datasets, as it avoids unnecessary comparisons and deletions.

	*Example:*
	You can solve the anagram problem with this.
```javascript
function anagram(word1, word2) {
  
	if (word1.length !== word2.length) {
		return false
	}
  
	const word1Frequency = {}
	const word2Frequency = {}

	for (let letter of word1) {
		word1Frequency[letter] = ++word1Frequency[letter] || 1
	}
  
	for (let letter of word2) {
		word2Frequency[letter] = ++word2Frequency[letter] || 1
	}

	for (let props in word1Frequency) {
		if (!(word2Frequency[props] && word2Frequency[props] === word1Frequency[props])) {
			return false
		}
	}

	return true
}

console.log(anagram('iceman', 'cinema')); // Expected output: true
console.log(anagram('hello', 'world')); // Expected output: false
console.log(anagram('listen', 'silent')); // Expected output: true
console.log(anagram('debit card', 'bad credit')); // Expected output: true
console.log(anagram('test', 'rest')); // Expected output: false
console.log(anagram('school master', 'the classroom')); // Expected output: true
```

2. **Multiple Pointer method**
	Creating pointers or values that correspond to an index or position and move towards the beginning, end or middle based on a certain condition 
	Very efficient for solving problems with minimal space complexity as well

	*Example Problem:* 
	Write a function called sumZero which accepts a sorted array of integers. The function should find the first pair where the sum is 0. Return an array that includes both values that sum to zero or undefined if a pair does not exist.

	*Example Problem 2:*
	Find add the unique values in a array of sorted elements, Here it's much easier because the input array is sorted.
```javascript
function countUniqueValues(sortedArray) {
	if (!sortedArray.length) return 0;

	let current = 0;

	for (let index = 0; index < sortedArray.length; index++) {
		if (!(sortedArray[current] === sortedArray[index])) {
			current++;
			sortedArray[current] = sortedArray[index];
		}
	}
	return current + 1;
}
console.log(countUniqueValues([1, 1, 1, 2, 2, 3]));
```

3. **Sliding Window**
	This pattern involves creating a window which can either be an array or number from one position to another depending on a certain condition, the window either increases or closes (and a new window is created)
	Very useful for keeping track of a subset of data in an array/string etc.

	*Example* 
```javascript
function maxSumSubArray(array,num) {

	if(!array.length) return null;

	let total = 0;

	for (let index = 0; index < num; index++) {
		total += array[index];
	}
	
	let sum = total;

	for (let index = num; index < array.length; index++) {
		sum = sum - array[index-num] + array[index]
		total = Math.max(sum,total)
	}

	return total
}
```


---
### Recursion 
==A process (a function in our case) that calls itself==

1. **Helper Method Recursion**: 
	Uses an outer function for setup and an inner function for recursive calls.
2. **Pure Recursion**: 
	Solves problems with a single function, calling itself to break down the problem until reaching a base case.
3. **Base Case**: 
	Stopping point for recursion, providing a known result and preventing infinite loops.

*Example* : finding factorial
```javascript
function factorial(n) {
    if (n === 0 || n === 1) {
        return 1;
    }
    return n * factorial(n - 1);
}

const number = 5;
const result = factorial(number);
console.log(`The factorial of ${number} is: ${result}`);

```

*Example* : collecting odd values
```javascript
function collectOddValues(array){

	let result = []

	if(!array.length) return result

	if(!(array[0] % 2 === 0)) result.push(array[0])
	
	result = [...result, ...collectOddValues(array.slice(1))]

	return result
}

console.log(collectOddValues([1,2,3,4,5,6,7,8,9]))
```


----
### Searching algorithms.

#### Describe what a searching algorithm is
==A searching algorithm is a step-by-step process used to find a specific item (such as a number or a piece of data) within a collection of items (like an array or a string).==
	
2. **Implement linear search on arrays**
	Linear search is a searching algorithm where we look for a specific value in a dataset one by one, so here we don't skip a value until we find it, if found we may return it's index or if not we may return -1. big O for this is O(n).
	*Example*
```javascript
function lenearSearch (array,find){
  
	//loop through the list.
	for (let index = 0; index < array.length; index++) {
		const element = array[index];

		// returning index if element if found.
		if(element === find){
			return index
		}
	}

	// returning -1 if element is not found.
	return -1
}

console.log(lenearSearch([1,2,3,4,5,6,7,8,9],1))
```

3. **Implement binary search on sorted arrays**
	Binary search is a more efficient searching algorithm, especially for sorted collections. It works by repeatedly dividing the search interval in half until the target item is found or the interval is empty. 
	1. we divide the data set in half.
	2. check to see if middle values if greater than or less than the findValue
	3. if greater we shift left to middle and if less we shift right to middle.
	4. we repeat the process until a value is found or there is no more values left to divide.
	Big O for this if O(logn) better than O(n) almost as same as O(1) according to some dictionaries. very suitable for large dataset, but only works on sorted dataset.
	*Example*
```javascript
function binarySearch(arr, target) {
    let left = 0;
    let right = arr.length - 1;

    while (left <= right) {
        let mid = Math.floor((left + right) / 2);

        // Check if target is present at mid
        if (arr[mid] === target) {
            return mid;
        }

        // If target is greater, ignore left half
        if (arr[mid] < target) {
            left = mid + 1;
        } else {
            // If target is smaller, ignore right half
            right = mid - 1;
        }
    }

	// If we reach here, then the element was not present
    return -1;
}

// Example usage:
console.log( binarySearch([1, 2, 3, 4, 5, 6, 7, 8, 9], 5) );
```

4. **Implement a naive string searching algorithm**
	*Example 1 Naive approach*
```javascript
function stringPattern(string, pattern) {

	let counter = 0;
	
	for (let index = 0; index < string.length; index++) {
		for (let innerIndex = 0; innerIndex < pattern.length; innerIndex++) {
			if(!(pattern[innerIndex] === string[index+innerIndex])){
				break;
			}
			if(innerIndex == pattern.length-1){
				counter++
			}
		}
	}

	return counter;
}

console.log(stringPattern('omglaksomgjdhglkajshdomglkgjahomgsdg', "omg"));
```

5. **Implement the KMP string searching algorithm**

---
### Sorting algorithms.

- Implement bubble sort
- ﻿﻿Implement selection sort
- ﻿﻿Implement insertion sort
- ﻿﻿Understand why it is important to learn these simpler sorting algorithms

---
### Data structures Introduction.

#### What do they do?
==Data structures are collections of values, the relationships among them, and the functions or operations that can be applied to the data.==
#### Why so many???
==Different data structures excel at different things. Some are highly specialized, while others (like arrays) are more generally used.==


# Hacker Rank - Tiktok assessment

1. Dijkstra algorithm
2. Dequeue - Doubly ended queue - & queues
3. 



