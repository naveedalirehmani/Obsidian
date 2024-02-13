	
#### Big 0
Big O notation is a method of analyzing an algorithms performance. 2 main factors that we consider for this are time and space complexity.
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
