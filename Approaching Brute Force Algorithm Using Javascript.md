1. Below are few examples which is started with simple to advance level (Travelling Salesman Problem and 0/1 knapsack problem)
2. These examples are based on **brute force Algorithm**


**My Note:-**

1. There are several downsides of this Brute Force Algorithm but before directly jumping into Dynamic programming and other approaches
2. you should have ideas on this approach and you must find out why we need a Dynamic Programming pattern (Recursion + Memorization)


If you closely observe the pattern for the brute force

``` javascript

const wrapper = (value) => {
    const helper = (combinedArray, depth) => {
       if (depth == 3) {
          // operation
           return ;
       }
       
       for (let coin of coins) {
           if (value - coin >=0) {
               combinedArray.push(coin);
               helper(combinedArray, label+1);
               combinedArray.pop();
           }
       }
    }
    
    helper([], 0);
    return result;
};

const res = wrapper(value);
console.log(res);
```

**Q1. Start with 2 coin combinations**

``` javascript
const wrapper = () => {
    const coinSide = ['head', 'tail']
    const result = [];
    const helper = (currentCombination, depth) => {
        if (depth == 2) {
            result.push([...currentCombination]);
            return ;
        }
        
        for (side of coinSide) {
            currentCombination.push(side);
            helper(currentCombination, depth +1);
            currentCombination.pop()
        }
    }
    
    helper([], 0);
    
    return result;
};

const res = wrapper();

console.log(res);
```
**Q2. Start with 3 coin combinations**

``` javascript
const wrapper = () => {
    const coinSide = ['head', 'tail']
    const result = [];
    const helper = (currentCombination, depth) => {
        if (depth == 3) {
            result.push([...currentCombination]);
            return ;
        }
        
        for (side of coinSide) {
            currentCombination.push(side);
            helper(currentCombination, depth +1);
            currentCombination.pop()
        }
    }
    
    helper([], 0);
    
    return result;
};

const res = wrapper();

console.log(res);

/*
[
  [ 'head', 'head', 'head' ],
  [ 'head', 'head', 'tail' ],
  [ 'head', 'tail', 'head' ],
  [ 'head', 'tail', 'tail' ],
  [ 'tail', 'head', 'head' ],
  [ 'tail', 'head', 'tail' ],
  [ 'tail', 'tail', 'head' ],
  [ 'tail', 'tail', 'tail' ]
]
*/
```
**Q3. Seating arrangement**

``` javascript
const wrapper = () => {
    const result = [];
    const group = ['b1', 'b2', 'g1']
    const helper = (combination, depth) => {
        if (depth == 3) {
            result.push([...combination]);
            return;
        }
        
        for (let item of group) {
            if (combination.indexOf(item) < 0) {
                combination.push(item);
            helper(combination, depth +1);
            combination.pop();
            }
        }
    }
    
    helper([], 0);
    
    return result;
};

/*
[
  [ 'b1', 'b2', 'g1' ],
  [ 'b1', 'g1', 'b2' ],
  [ 'b2', 'b1', 'g1' ],
  [ 'b2', 'g1', 'b1' ],
  [ 'g1', 'b1', 'b2' ],
  [ 'g1', 'b2', 'b1' ]
]
*/
```
**Q4. Coin / Sum problem**

``` javascript
// Minimum coin Problem
const wrapper = (value) => {
    let result = 99999;
    let resultArr = [];
    const coins = [10, 6, 1];
    const helper = (value, label, combinedArray) => {
       if (value == 0) {
           if (result > label) {
               result = label;
               resultArr = [...combinedArray]
           }
           return ;
       }
       
       for (let coin of coins) {
           if (value - coin >=0) {
               combinedArray.push(coin);
               helper(value-coin, label+1, combinedArray);
               combinedArray.pop();
           }
       }
    }
    
    helper(value, 0, []);
    console.log(resultArr)
    
    return result;
};

const res = wrapper(12);

console.log(res);
/*
[ 6, 6 ]
2
*/
```
**Q5.Set generation**

``` javascript
// Problem 1: Generating All Subsets of a Set
// Problem Statement:
// Given a set of unique elements, generate all possible subsets (the power set).
// This solution need more enhancement.
// Example:
// Input: [1, 2, 3]
// Output: [[], [1], [2], [3], [1, 2], [1, 3], [2, 3], [1, 2, 3]]


const wrapper = () => {
    const result = [[]];
    const input = [1,2,3];
    input.forEach(item => result.push([item]));
  
    const helper = (combination, depth) => {
        if (depth == 2) {
            if (result.indexOf(combination) < 0) {
                result.push([...combination]);
            }
            
            
            return;
        }
        
        for (let item of input) {
           if (combination.indexOf(item) < 0) {
                combination.push(item);
            helper(combination, depth+1);
            combination.pop()
           }
        }
        
    }
    
    helper([], 0);
    result.push([...input])
    return result;
}

const test = wrapper();

console.log(test);
/*
[
  [],          [ 1 ],
  [ 2 ],       [ 3 ],
  [ 1, 2 ],    [ 1, 3 ],
  [ 2, 1 ],    [ 2, 3 ],
  [ 3, 1 ],    [ 3, 2 ],
  [ 1, 2, 3 ]
]
*/
```
**Q6.Travelling sales man problem using brut force algorithm**

``` javascript
// Travelling sales man problem using brut force algorithm

function calculateDistance(matrix, path) {
  let totalDistance = 0;
  for (let i = 0; i < path.length - 1; i++) {
    totalDistance += matrix[path[i]][path[i + 1]];
  }
  // Return to the starting city
  totalDistance += matrix[path[path.length - 1]][path[0]];
  return totalDistance;
}

function permute(arr) {
  const result = [];
  
  const helper = (combination, depth) => {
      if (depth == 4) {
          result.push([...combination]);
          
          return;
      }
      
      for (let item of arr) {
          if (combination.indexOf(item) < 0) {
              combination.push(item);
              helper(combination, depth +1);
              combination.pop()
          }
      }
  }
  helper([], 0);
  
  return result;
}

function tsp(matrix) {
  const cities = Array.from({length: matrix.length}, (_, index) => index)
  console.log(cities)
  const permutations = permute(cities);
  console.log(permutations)
  let minDistance = Infinity;
  let bestPath = [];

  for (let path of permutations) {
    const distance = calculateDistance(matrix, path);
    if (distance < minDistance) {
      minDistance = distance;
      bestPath = path;
    }
  }

  return { minDistance, bestPath };
}

// Example usage:
const distanceMatrix = [
  [0, 10, 15, 20],
  [10, 0, 35, 25],
  [15, 35, 0, 30],
  [20, 25, 30, 0]
];

const result = tsp(distanceMatrix);

console.log(`The shortest distance is: ${result.minDistance}`);
console.log(`The best path is: ${result.bestPath}`);
/*
Initialization:  Calculate Distance Explanation

totalDistance is initialized to 0.
First Iteration (i = 0):

From city 0 to city 1: matrix[0][1] is 10.
Add 10 to totalDistance, making it 10.
Second Iteration (i = 1):

From city 1 to city 3: matrix[1][3] is 25.
Add 25 to totalDistance, making it 35.
Third Iteration (i = 2):

From city 3 to city 2: matrix[3][2] is 30.
Add 30 to totalDistance, making it 65.
Return to Starting City:

From city 2 back to city 0: matrix[2][0] is 15.
Add 15 to totalDistance, making it 80.
Return Total Distance:

The function returns 80, which is the total distance of the path [0, 1, 3, 2, 0].

// Output
[ 0, 1, 2, 3 ]
[
  [ 0, 1, 2, 3 ], [ 0, 1, 3, 2 ],
  [ 0, 2, 1, 3 ], [ 0, 2, 3, 1 ],
  [ 0, 3, 1, 2 ], [ 0, 3, 2, 1 ],
  [ 1, 0, 2, 3 ], [ 1, 0, 3, 2 ],
  [ 1, 2, 0, 3 ], [ 1, 2, 3, 0 ],
  [ 1, 3, 0, 2 ], [ 1, 3, 2, 0 ],
  [ 2, 0, 1, 3 ], [ 2, 0, 3, 1 ],
  [ 2, 1, 0, 3 ], [ 2, 1, 3, 0 ],
  [ 2, 3, 0, 1 ], [ 2, 3, 1, 0 ],
  [ 3, 0, 1, 2 ], [ 3, 0, 2, 1 ],
  [ 3, 1, 0, 2 ], [ 3, 1, 2, 0 ],
  [ 3, 2, 0, 1 ], [ 3, 2, 1, 0 ]
]
The shortest distance is: 80
The best path is: 0,1,3,2

*/

```
**Q7. 0/1 knapsack Brut force Problem**

- The 0/1 Knapsack problem is a classic problem where you are given a set of items, each with a weight and a value, and you need to determine the most valuable combination of items to include in a knapsack, given a maximum weight capacity.

- The "0/1" part of the name refers to the fact that you can't break items into smaller parts; you either take the whole item or don't take it at all (i.e., 0 or 1).

- The brute force solution to the 0/1 Knapsack problem involves generating all possible combinations of items and checking which combination gives the maximum value without exceeding the weight capacity of the knapsack.

- This approach has a time complexity of O(2^n), where n is the number of items, as there are 2^n possible combinations of items.

``` javascript
// 0/1 knapsack Brut force Problem
function knapsackBruteForce(weights, values, capacity) {
  let n = weights.length;
  let maxValue = 0;
  const subsetResult = [];
  const binaryVals = [0, 1];

  // Function to calculate the total weight and value of a subset
  function calculateSubset(subset) {
    let totalWeight = 0;
    let totalValue = 0;
    for (let i = 0; i < subset.length; i++) {
      if (subset[i]) {
        totalWeight += weights[i];
        totalValue += values[i];
      }
    }
    return { totalWeight, totalValue };
  }
  
  const helper = (combination, depth) => {
      if (depth == 4) {
          subsetResult.push([...combination]);
          return ;
      }
      
      for (let item of binaryVals) {
          combination.push(item);
          helper(combination, depth +1);
          combination.pop()
      }
      
  }

    helper([], 0);
    console.log(subsetResult)
  // Generate all subsets using binary representation
  for (let subset of subsetResult) {
    let { totalWeight, totalValue } = calculateSubset(subset);
    if (totalWeight <= capacity && totalValue > maxValue) {
      maxValue = totalValue;
    }
  }

  return maxValue;
}

// Example usage:
const weights = [2, 3, 4, 5];
const values = [3, 4, 5, 6];
const capacity = 5;
const maxVal = knapsackBruteForce(weights, values, capacity);

console.log(`The maximum value in the knapsack is: ${maxVal}`);
/*
[
  [ 0, 0, 0, 0 ], [ 0, 0, 0, 1 ],
  [ 0, 0, 1, 0 ], [ 0, 0, 1, 1 ],
  [ 0, 1, 0, 0 ], [ 0, 1, 0, 1 ],
  [ 0, 1, 1, 0 ], [ 0, 1, 1, 1 ],
  [ 1, 0, 0, 0 ], [ 1, 0, 0, 1 ],
  [ 1, 0, 1, 0 ], [ 1, 0, 1, 1 ],
  [ 1, 1, 0, 0 ], [ 1, 1, 0, 1 ],
  [ 1, 1, 1, 0 ], [ 1, 1, 1, 1 ]
]
The maximum value in the knapsack is: 7
*/

```
