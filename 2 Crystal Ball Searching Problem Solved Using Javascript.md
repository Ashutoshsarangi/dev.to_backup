2 Crystal ball problem find the 1st hit with minimum time complexity.


``` javascript
const arr = [false, false, false, false, true, true, true, true, true, true];

function two_crystal_balls(breaks) {
  const jmpAmount = Math.floor(Math.sqrt(breaks.length));

  let i = jmpAmount;
  for (; i < breaks.length; i += jmpAmount) {
    if (breaks[i]) {
      break;
    }
  }
  console.log(i, "i");

    const updatedPos = i - jmpAmount;
    
  for (let j = updatedPos; j<= i; j++) {
    if (arr[j]) {
        console.log('Answer ---> ', j);
        return ;
    }
}
  return -1;
}
two_crystal_balls(arr);

/*
Output
6 i
Answer --->  4 
*/
```
