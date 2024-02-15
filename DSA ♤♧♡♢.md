	
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

This algorithms time and space complexity of O(1).
```javascript
function sumNumbersUpToNFormula(n) {
  return (n * (n + 1)) / 2;
}

console.log(sumNumbersUpToNFormula(5));
```

---

#### Performance of Arrays & Objects.

Push and Pop operations on an array have a time complexity of O(1), while shift and unshift have a O(n) has pushing new elements to the start or middle of an array means that we need to reposition all the proceeding elements in a array.

Objects have a time complexity of O(1) when we are accessing, inserting or modifying properties, while searching from the elements while take O(n) amount of time.

---

#### Problem Solving Patterns.

##### Algorithms?
A process of set of steps to accomplish a certain task.
### Problem Solving strategies.

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
