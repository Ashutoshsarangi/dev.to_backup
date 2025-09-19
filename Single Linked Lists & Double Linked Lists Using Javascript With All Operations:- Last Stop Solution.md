**Linked List**

1. Single Linked List
2. Doubly Linked List


**Operations with Time Complexity** 

1. prepend /append **O(1)**
2. Insert in the middle **O(n/2)**
3. Delete from Ends **O(1)**
4. Deletion in the middle **O(n/2)**
5. get head/tail **O(1)**
6. get in general 
7. reverse Linked list **O(n)**
8. One Way Traversal (Single Linked List) **O(n)**
9. Bi-Directional Traversal (Double Linked List) **O(n)**

**Single Linked List with all the Above Operations**

``` javascript
class Node {
    constructor(value) {
        this.value = value;
        this.next = null;
    }
}

class SingleLinkedList {
    
    constructor(value) {
        this.head = this.tail = new Node(value);
        this.size = 1;
    }
    
    append(value) {
        const newNode = new Node(value);
        this.tail.next = newNode;
        this.tail = newNode;
        this.size++;
    }
    
    prepend(value) {
        const newNode = new Node(value);
        newNode.next = this.head;
        this.head = newNode;
        this.size++;
    }
    
    insertInMiddle(value) {
        const newNode = new Node(value);
        let currentHead = this.head;
        const pos = Math.floor(this.size/2);
        let counter = 0
        while(currentHead) {
            if (++counter == pos){
                this.size++;
                const temp = currentHead.next;
                currentHead.next = newNode;
                newNode.next = temp;
                break;
            }
            currentHead = currentHead.next;
        }
    }
    
    traversal() {
        let currentNode = this.head;
        
        while (currentNode) {
            console.log(currentNode.value);
            currentNode = currentNode.next;
        }
    }
    
    deleteAtEnd() {
        let currentNode = this.head;
        
        while(currentNode) {
            if (currentNode.next.next === null) {
                currentNode.next = null;
                this.tail = currentNode;
                this.size--;
            }
            currentNode = currentNode.next;
        }
    }
    
    deleteAtMiddle() {
        let currentNode = this.head;
        const pos = Math.floor(this.size/2);
        let counter = 0;
        let previousCounter = null;
        
        while (currentNode) {
            if (counter++ === pos) {
                previousCounter.next = currentNode.next;
                this.size--;
            }
            previousCounter = currentNode;
            currentNode = currentNode.next;
            
        }
    }
    
    reverse() {
        let prevNode = null;
        let nextNode = null;
        let currentNode = this.head;
        
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
    }
}


const test = new SingleLinkedList(3);
test.append(5);
test.append(9);
test.prepend(13);
test.prepend(20)
test.insertInMiddle(100);

console.log('Head ---> ', test.head);
console.log('Tail. -> ', test.tail);
console.log('-------------------');

test.traversal();
console.log('----------------After delete at End----------');
test.deleteAtEnd();
test.traversal();
console.log('----------------After delete at Middle----------');
test.deleteAtMiddle();
test.traversal();

console.log('----------------After Reverse Linked List----------');
test.reverse();
test.traversal();
console.log('Head ---> ', test.head);
console.log('Tail. -> ', test.tail);
/*
Head --->  Node {
  value: 20,
  next: Node { value: 13, next: Node { value: 100, next: [Node] } }
}
Tail. ->  Node { value: 9, next: null }
-------------------
20
13
100
3
5
9
----------------After delete at End----------
20
13
100
3
5
----------------After delete at Middle----------
20
13
3
5
----------------After Reverse Linked List----------
5
3
13
20
Head --->  Node {
  value: 5,
  next: Node { value: 3, next: Node { value: 13, next: [Node] } }
}
Tail. ->  Node { value: 20, next: null }
*/

```
**Double Linked List with all the above Operations**

``` javascript
class Node {
    constructor(value) {
        this.value = value;
        this.next = null;
        this.prev = null;
    }
}

class DoubleLinkedList {
    constructor(value) {
        this.head = this.tail = new Node(value);
        this.size = 1;
    }
    
    append(value) {
        const newNode = new Node(value);
        this.tail.next = newNode;
        newNode.prev = this.tail;
        this.tail = newNode;
        this.size++;
    }
    
    prepend(value) {
        const newNode = new Node(value);
        newNode.next = this.head;
        this.head.prev = newNode;
        this.head = newNode;
        this.size++;
    }
    
    insertAtMiddle(value) {
        if (this.size <= 1) {
            this.append(value);  // If size is 1 or less, append the new node at the end
            return;
        }

        const newNode = new Node(value);
        const pos = Math.floor(this.size / 2);
        let counter = 0;
        let currentNode = this.head;
        
        while (currentNode) {
            if (counter++ === pos) {
                const nextNode = currentNode.next;
                currentNode.next = newNode;
                newNode.prev = currentNode;
                newNode.next = nextNode;
                if (nextNode) {
                    nextNode.prev = newNode;
                }
                this.size++;
                break;
            }
            currentNode = currentNode.next;
        }
    }
    
    traverseForward() {
        let currentNode = this.head;
        while (currentNode) {
            console.log(currentNode.value);
            currentNode = currentNode.next;
        }
    }
    
    traverseReverse() {
        let lastNode = this.tail;
        while (lastNode) {
            console.log(lastNode.value);
            lastNode = lastNode.prev;
        }
    }
    
    deleteAtEnd() {
        if (this.size === 1) {  // Handle the case where there's only one element
            this.head = this.tail = null;
            this.size = 0;
            return;
        }

        const lastNode = this.tail;
        this.tail = lastNode.prev;
        this.tail.next = null;
        this.size--;

        // Optional: nullify references to help garbage collection
        lastNode.prev = null;
    }
    
    deleteAtMiddle() {
        if (this.size <= 1) {
            this.deleteAtEnd();  // If size is 1 or less, simply delete the last element
            return;
        }

        let currentNode = this.head;
        const pos = Math.floor(this.size / 2);
        let counter = 0;
        
        while (currentNode) {
            if (counter++ === pos) {
                const prevNode = currentNode.prev;
                const nextNode = currentNode.next;

                if (prevNode) {
                    prevNode.next = nextNode;
                }
                if (nextNode) {
                    nextNode.prev = prevNode;
                }
                this.size--;

                // Optional: nullify references to help garbage collection
                currentNode.next = currentNode.prev = null;
                break;
            }
            currentNode = currentNode.next;
        }
    }
    
    reverseList() {
        let currentNode = this.head;
        let prevNode = null;
        let nextNode = null;

        while (currentNode) {
            nextNode = currentNode.next;
            currentNode.next = prevNode;
            currentNode.prev = nextNode;

            prevNode = currentNode;
            currentNode = nextNode;
        }

        // Swap head and tail
        this.tail = this.head;
        this.head = prevNode;
    }
}

// Test the implementation
const test = new DoubleLinkedList(3);
test.append(5);
test.append(9);
test.prepend(13);
test.prepend(20);

console.log('Head:', test.head.value);  // 20
console.log('Tail:', test.tail.value);  // 9
console.log('Size:', test.size);        // 5
console.log('-------------------------');
test.traverseForward();                 // 20 -> 13 -> 3 -> 5 -> 9
console.log('-------------Reverse Traversal------------');
test.traverseReverse();                 // 9 -> 5 -> 3 -> 13 -> 20
console.log('---------Insert At Middle ----------------');
test.insertAtMiddle(100);
test.traverseForward();                 // 20 -> 13 -> 3 -> 100 -> 5 -> 9
console.log('-------deleteAtEnd-----------');
test.deleteAtEnd();
test.traverseForward();                 // 20 -> 13 -> 3 -> 100 -> 5
console.log('-------deleteAtMiddle-----------');
test.deleteAtMiddle();
test.traverseForward();                 // 20 -> 13 -> 100 -> 5
console.log('-------Reverse Double Linked List-----------');
test.reverseList();
test.traverseForward();                 // 5 -> 100 -> 13 -> 20
```
Feel free to reach out to me if you have any queries/concerns. Available on Linkedin.
