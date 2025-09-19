## Introduction

As a JavaScript developer, I've often found two Array methods a bit tricky to grasp/fully

1. Array.slice 
2. Array.splice. 



So, I decided to dive deep and break down these methods with clear examples. 

**If I re-write the Syntax**

**Array.slice**

``` javascript
returns the deleted elements in a form of Array = Array.prototype.slice(startIndex, endIndex-1);
```


**Array.splice** (P for Permanent - Always remember)

The splice method in JavaScript modifies the contents of an array by **removing or replacing existing elements and/or adding new elements in place**

**Removing element Syntax**

``` javascript
returns the deleted elements in a form of Array = Array.prototype.splice(startIndex, endIndex-1); // permanent 

```
**Adding element Syntax**

``` javascript
// Here 0 is the deletCount
array.splice(startIndex, 0, item1, item2, ..., itemX);
```

**NOTE:-**

1. It changes the original array and returns the deleted array.

2. When it behaves as an add operation it returns [] as it is not removing anything.


**let's see some examples:-**

Q1. Exercise 1 - Using slice to get a part of an array: Create an array of numbers from 1 to 10. Use the slice method to get a new array that includes numbers from 4 to 8.

``` javascript
const arr = Array.from(Array(10), (_, i) => i+1);
console.log('Array --> ', arr);
console.log('get a new array that includes numbers from 4 to 8 --> ', arr.slice(3, 8)); // Array.prototype.slice(startIndex, endIndex-1);

// [ 4, 5, 6, 7, 8 ]
```


Q2. Exercise 2 - Using splice to remove elements from an array: Create an array of fruits. Use the splice method to remove "apple" and "banana" from the array.

``` javascript
const fruits = ['apple', 'banana', 'orange', 'mango', 'kiwi'];

fruits.splice(0, 2)// permanent

console.log('splice method to remove "apple" and "banana" from the array. --> ', fruits);

// [ 'orange', 'mango', 'kiwi' ]
```

Q3. Exercise 3 - Using splice to add elements to an array: Create an array of colors. Use the splice method to add "pink" and "purple" after "red".

``` javascript
const colors = ['red', 'green', 'blue'];

const y = colors.splice(1, 0, "pink", "purple"); /
console.log(y); // [] see above to see why.
console.log('splice method to add "pink" and "purple" after "red" --> ', colors)

// [ 'red', 'pink', 'purple', 'green', 'blue' ]
```

Q4. Exercise 4 - Using slice and splice together: Create an array of letters from 'a' to 'e'. Use slice to get a new array of the first three letters. Then use splice on the original array to remove these letters.

``` Javascript
const letters = ['a', 'b', 'c', 'd', 'e'];
const newSlice = letters.slice(0, 3);
const x = letters.splice(0, 3);
console.log(x);
console.log('slice to get a new array of the first three letters --> ', newSlice) // [ 'a', 'b', 'c' ]

console.log('Then use splice on the original array to remove these letters --> ', letters)[ 'd', 'e' ]
```

Feel free to reach out to me if you have any queries/concerns. 




















