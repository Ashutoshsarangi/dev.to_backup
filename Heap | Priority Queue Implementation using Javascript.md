## Introduction

A heap is a special tree-based data structure that satisfies the heap property. 
It is a complete binary tree, which means all levels of the tree are fully filled except for the last level, which is filled from left to right.

**There are two types of heaps:** 

1. max heap
2. min heap.  

**Max Heap:** 

In a max heap, for any given node I, the value of I is greater than or equal to the values of its children.
This property must be true for all nodes in the Binary Tree. The highest value (maximum) is at the root of the tree.

**Min Heap:** 

In a min heap, for any given node I, the value of I is less than or equal to the values of its children.
This property must be true for all nodes in the Binary Tree. The lowest value (minimum) is at the root of the tree.

We can call them a priority queue as every time we do an insert and delete operation it will **bubbleUp** and **bubbleDown** respectively.

We can implement the same in an array but how to calculate the leftChildindex, rightChildIndex and parentIndex?

 **Formula**

 **To get child**


> 2i+1(left )
> 2i+2 (right)

**To get parent**

>  i-1/2 


Below I added an implementation of minHeap please check.

``` javascript
class MinHeap {
    constructor() {
        this.data = [];
        this.length = 0;
    }
    
    insert(value) {
        this.data.push(value);
        this.length++;
        this.bubbleUp(this.length-1);
    }
    
    bubbleUp(index) {
        
        if (index == 0) {
            return ;
        }
        
        const parentIndex = this.getParentIndex(index);
        const parentValue = this.data[parentIndex];
        const value = this.data[index];
        
        if (parentValue > value) {
            this.data[parentIndex] = this.data[index];
            this.data[index] = parentValue;
            
            this.bubbleUp(parentIndex);
        }
    }
    
    getParentIndex(index) {
        return Math.floor((index-1)/2);
    }
    
    getLeftChildIndex(index) {
        return 2*index + 1;
    }
    
    getRightChildIndex(index) {
        return 2*index + 2;
    }
    
    bubbleDown(index) {
        if (index >= this.length) {
            return;
        }
        
        const lIndex = this.getLeftChildIndex(index);
        const rIndex = this.getRightChildIndex(index);
        
        const lValue = this.data[lIndex];
        const rValue = this.data[rIndex];
        const value = this.data[index];
        
        if (lValue < rValue && lValue < value) {
            // swap
            this.data[index] = this.data[lIndex];
            this.data[lIndex] = value;
            this.bubbleDown(lIndex);
        } else if (rValue < lValue && rValue < value) {
            this.data[index] = this.data[rIndex];
            this.data[rIndex] = value;
            this.bubbleDown(rIndex)
        }
    }
    
    delete() {
        if (this.length === 0) {
            return -1;
        }
        
        const out = this.data[0];
        if (this.length == 1) {
            this.data = [];
            this.length = 0;
            return out;
        }
        
        this.data[0] = this.data[this.length-1];
        this.length--;
        this.bubbleDown(0);
    }
}

const test = new MinHeap();

test.insert(50);
test.insert(100);
test.insert(101);
test.insert(20);
test.insert(110);
console.log(test)
test.delete();
console.log('---------After Delete -------')
console.log(test)
/*
MinHeap { data: [ 20, 50, 101, 100, 110 ], length: 5 }
---------After Delete -------
MinHeap { data: [ 50, 100, 101, 110, 110 ], length: 4 }
*/

```

Let me know of you have any queries, feel free to connect.
