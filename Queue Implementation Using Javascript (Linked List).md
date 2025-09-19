## Introduction
 
If you are not confident or want to understand more about Linked list and their types and how we can do operations on the same please refer to my other article related to the Single Linked List and Double Linked List

[Approaching Single and Double Linked Lists Using Javascript With All Operations:- Last Stop Solution]("https://dev.to/ashutoshsarangi/approaching-single-and-double-linked-lists-using-javascript-with-all-operations-last-stop-40m1")

2. This Article is about using the Single linked List and creating a **Queue data Structure**.

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
    
    append(value){
        const newNode = new Node(value);
        
        if (this.head === null) {
            this.head = this.tail = newNode;
            this.size = 1;
            return ;
        }
        
        let currentNode = this.head;
        const pos = this.size-1;
        let counter = 0;
        
        while (currentNode) {
            if (counter++ === pos) {
                currentNode.next = newNode;
                this.tail = newNode;
                this.size++;
                break;
            }
            currentNode = currentNode.next;
        }
    }
    
    deleteFromHead() {
        if (this.head === null) {
            return ;
        }
        let currentNode = this.head;
        this.head = currentNode.next;
        this.size--;
        return this.head.value;
    }
    
    traversal() {
        let currentNode = this.head;
        
        while (currentNode) {
            console.log(currentNode.value);
            currentNode = currentNode.next;
        }
    }
    
    reverse(){
        let currentNode = this.head;
        let nextNode = null;
        let prevNode = null;
        
        while(currentNode) {
            nextNode = currentNode.next;
            currentNode.next = prevNode;
            if (prevNode === null) {
                this.tail = prevNode;
            }
            prevNode = currentNode;
            currentNode = nextNode;
        }
        
        this.head = prevNode;
        this.traversal();
    }
    
    
}


class Queue{
    queue;
    constructor() {
        this.queue = new LinkedList();
    }
    
    push(value) {
        this.queue.append(value)
    }
    
    pop() {
        this.queue.deleteFromHead();
    }
    
    peak() {
        console.log(this.queue.head.value)
    }
    
    traversal() {
        this.queue.traversal()
    }
    reverse() {
        this.queue.reverse();
    }
}


const q = new Queue();

q.push(20);
q.push(13);
q.push(3);
q.push(5);
q.push(9);

q.pop()
console.log(q);
q.traversal()
console.log('---------------Peak--------------')
q.peak()
console.log('-------------After Reverse ---------------');
q.reverse()

/*
Queue {
  queue: LinkedList {
    tail: Node { value: 9, next: null },
    head: Node { value: 13, next: [Node] },
    size: 4
  }
}
13
3
5
9
---------------Peak--------------
13
-------------After Reverse ---------------
9
5
3
13
*/

```
