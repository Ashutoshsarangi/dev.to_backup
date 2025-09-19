## Introduction
 
If you are not confident or want to understand more about Linked list and their types and how we can do operations on the same please refer to my other article related to the Single Linked List and Double Linked List

[Approaching Single and Double Linked Lists Using Javascript With All Operations:- Last Stop Solution]("https://dev.to/ashutoshsarangi/approaching-single-and-double-linked-lists-using-javascript-with-all-operations-last-stop-40m1")

2. This Article is about using the Single linked List and creating a **Stack data Structure**.

Feel free to reach out to me if you have any concerns 

Enjoy the code, Happy Codeing.

``` javascript
 class Node {
     constructor(value) {
         this.value = value;
         this.next = null;
     }
 }
 
 class LinkedList {
     constructor() {
         this.head = this.tail = null;
         this.size = 0;
     }
     
     append(value) {
         const newNode = new Node(value);
         if (this.head === null) {
             console.log('Inside strange')
             this.head = this.tail = newNode;
             this.size = 1;
             return;
         }
         this.tail.next = newNode;
         this.tail = newNode;
         this.size++;
     }
     
     deletAtEnd() {
         if (this.size <= 1) {
             
             this.head = this.tail = null;
             this.size = 0;
             return;
         }
         let currentNode = this.head;
         const pos = this.size -1;
         let counter = 1;
         while (currentNode) {
             if (counter++ === pos) {
                 currentNode.next = null;
                 this.tail = currentNode;
                 this.size--;
                 return ;
             }
             currentNode = currentNode.next;
         }
     }
     
     traversal() {
         let currentNode = this.head;
         while (currentNode) {
             console.log(currentNode.value);
             currentNode = currentNode.next;
         }
     }
     
     reverse() {
        let currentNode = this.head;
        let prevNode = null;
        let nextNode = null;
        
        while (currentNode) {
            nextNode = currentNode.next;
            currentNode.next = prevNode;
            if (prevNode === null) {
                this.tail = currentNode;
            }
            
            prevNode = currentNode;
            currentNode = nextNode;
        }
        
        this.head = prevNode;
        
        this.traversal();
     }
 }
 
 class Stack {
     stack;
     constructor() {
         this.stack = new LinkedList();
     }
     
     push(value) {
        this.stack.append(value);
     }
     
     pop() {
        this.stack.deletAtEnd()
     }
     
     peak() {
        console.log('Peak Value ---> ', this.stack.tail.value); 
     }
     traversal() {
         this.stack.reverse();
     }
 }
 
 
 const test = new Stack();
 
 test.push(20);
 test.push(13);
 test.push(3);
 test.push(5);
 test.push(9);
 
 console.log(test.stack)
 console.log('---------------Peak-------------')
 test.peak()
 console.log('-------------After Pop ------------');
 test.pop();
 test.peak()
 test.traversal()

/*
LinkedList {
  tail: Node { value: 9, next: null },
  head: Node { value: 20, next: Node { value: 13, next: [Node] } },
  size: 5
}
---------------Peak-------------
Peak Value --->  9
-------------After Pop ------------
Peak Value --->  5
5
3
13
20

*/

```

