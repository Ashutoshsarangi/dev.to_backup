Bubble Sort and Insertion Sort are 2 basic sorting algorithms are there. I implemented these algorithms using JavaScript.

**Bubble Sort**

``` javascript
const arr = [5,4,3,2,1];

for (let i = 0; i < arr.length; i++) {
    for (j = 0 ; j< arr.length-i; j++) {
        if (arr[j] > arr[j+1]) {
            let temp = arr[j];
            arr[j] = arr[j+1];
            arr[j+1] = temp;
        }
    }
}

console.log(arr); // [1,2,3,4,5]

```

**Insertion Sort**

it is better than bubble sort + if you know the array is almost sorted it is best algorithm

``` javascript
const arr = [5,4,3,2,1];
for (let i = 0; i < arr.length; i++) {
    for (let j = i+1; j < arr.length; j++) {
        if (arr[i] > arr[j]) {
            const temp = arr[j];
            arr[j] = arr[i];
            arr[i] = temp;
        }
    } 
}


console.log(arr); // [1,2,3,4,5]

```

**Selection Sort**

``` javascript
const arr = [5,4,3,2,1];
for (let i = 0; i< arr.length; i++) {
    let min = Infinity;
    let pos = -1;
    for(let j = i; j < arr.length; j++) {
        if (min > arr[j]) {
            min = arr[j];
            pos = j;
        }
    }
    
    const temp = arr[i];
    arr[i] = arr[pos];
    arr[pos] = temp;
}


console.log(arr); // [1,2,3,4,5]

```
