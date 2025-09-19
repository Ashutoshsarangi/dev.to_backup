There are 2 types of searching algorithms are there as below.

1. Linear Search
2. Binary Search (We must get Sorted array as an input)


``` javascript
const linearSearch = (arr, value) => {
    for (let item of arr) {
        if (item == value) {
            return true;
        }
    }
    return false;
};

console.log(linearSearch([1,2,3,4,5,6,7,8,9], 7));
console.log(linearSearch([1,2,3,4,5,6,7,8,9], 3));
console.log(linearSearch([1,2,3,4,5,6,7,8,9], 10));
console.log(linearSearch([1,2,3,4,5,6,7,8,9], 9));

```


**Binary Search**

``` javascript

const binarySearch =  (arr, value, low = 0, high=arr.length-1) => {
    const mid = Math.floor((low + high)/2);
    const midValue = arr[mid];
    if (low > high) {
        return false;
    }
    if (midValue == value) {
        return true;
    } else if (midValue > value) {
        return binarySearch(arr, value, low, mid);
    } else {
        return binarySearch(arr, value, mid+1, high);
    }
}

const arr = [9,8,7,6,5,4,3,2,1];
arr.sort((a,b) => a-b);

console.log(binarySearch(arr, 7));
console.log(binarySearch(arr, 3));
console.log(binarySearch(arr, 10));
console.log(binarySearch(arr, 9));

```
