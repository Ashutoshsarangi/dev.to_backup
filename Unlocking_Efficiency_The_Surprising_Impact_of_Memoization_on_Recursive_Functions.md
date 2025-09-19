## Introduction

I recently conducted an analysis comparing the number of times a function executes when using plain recursion versus memoized recursion. The results were surprising! 😱 😱 



With plain recursion, the function call count can skyrocket due to repeated calculations of the same values. In contrast, memoized recursion significantly reduces the number of executions by storing and reusing previously computed results.



This experiment highlights the efficiency gains that can be achieved with memoization, making it a valuable optimization technique for improving the performance of recursive algorithms.



**The Code difference is only 5 Lines Plain Recurssion of a Fibonacci ()** (See the Difference 😱 )

**No Of times function Executed (Can you read the Number 😅 😵 )**

|**n|Recurssion|memorized-recurssion**  |
|----|----- | ---------------  |
| 10 | **88** | 9 |
| 15 | **986** | 14 |
| 30 | **13,46,268** | 29 |

 


``` javascript
const recursiveFibonacciClosure = (n) => {
    let counter = 0;
    function recursiveFibonacci(n) {
      if (n == 0 || n == 1) {
        return n;
      }
      counter++;
      
      return recursiveFibonacci(n-1) + recursiveFibonacci(n-2);
    }
    
    recursiveFibonacci(n);
    console.log(`${counter} No of time this function is executed.`); 
    // For n= 10 it is calling 88
    // n = 15 ==> 986 times function Executed
    // n = 30 ==> 13,46,268 times function Executed
}

recursiveFibonacciClosure(30);


const memorizeRecurssion = (n) => {
    let counter = 0;
    const memo = {};
    function recursiveFibonacci(n) {
      if (n == 0 || n == 1) {
        return n;
      }
      
       const temp = recursiveFibonacci(n-1) + recursiveFibonacci(n-2);
       
      if (memo[n]) {
          return memo[n]
      } else {
          memo[n] = temp;
      }
      counter++;
      
      return temp;
    }
    
    recursiveFibonacci(n);
    console.log(`${counter} No of time this function is executed.`); 
    // For n= 10 it is calling 9
    // n = 15 ==> 14 times it is executed
    // n = 30 ==> 29 times it is executed
}

memorizeRecurssion(30)
```

#Recursion #Memoization #Coding #Programming #Efficiency #AlgorithmOptimization #SoftwareDevelopment #Javascript #Functional programming
