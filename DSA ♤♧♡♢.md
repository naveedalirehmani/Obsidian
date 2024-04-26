	
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
