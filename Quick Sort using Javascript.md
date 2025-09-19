Implementing Quick Sort is bit tricky but if you understand it and keep on practice it will be easier.


``` javascript

const quickSort = (arr, lo, hi) => {
    if (lo >= hi) {
        return ;
    }
    
    const pivotIndex = getPivotIndex(arr, lo, hi);
    quickSort(arr, lo, pivotIndex-1);
    quickSort(arr, pivotIndex+1, hi);
}

const getPivotIndex = (arr, lo, hi) => {
    const pivot = arr[hi];
    let idx = lo-1;
    
    for (let i = lo; i< hi; i++) {
        if (arr[i] <= pivot) {
            idx++;
            const temp = arr[i];
            arr[i] = arr[idx];
            arr[idx] = temp;
        }
    }
    idx++;
    const temp = arr[idx];
    arr[idx] = pivot;
    arr[hi] = temp;
    
    return idx;
}
const arr = [9,1,0,3,2,5,9,10, 11];
quickSort(arr, 0, 8);
console.log(arr); // [0, 1,  2,  3, 5, 9, 9, 10, 11]
```
Try to dry run it you will get the clear picture.
