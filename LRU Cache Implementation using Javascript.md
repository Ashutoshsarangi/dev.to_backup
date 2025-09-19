## Introduction

LRU stands for Least Recently Used. An LRU cache is a type of cache in which the least recently used entries are removed when the cache reaches its capacity. 

- The main reason to use an LRU cache is to improve the performance of accessing data. Accessing data from a cache is typically faster than retrieving it from the main memory or a remote server.
- By storing the most recently used data in the cache, the chance of a cache hit is increased, which in turn improves the speed of data retrieval.


**FYI:**

- A map data structure is used to mimic the behavior of a Hash Table. This allows for efficient lookup, insertion, and deletion operations.
- A Double Linked List is implemented to enable easy movement between elements. This provides the ability to traverse in both directions (forward and backward) and perform constant time insertions and deletions.
- The combination of these two data structures allows for efficient operations, leveraging the advantages of both Hash Tables and Double Linked Lists.

Here's a basic example of how an LRU cache might be implemented in JavaScript:

```javascript
// Why we need this LRU
class Node {
    constructor(key, value) {
        this.key = key;
        this.value = value;
        this.next = null;
        this.prev = null;
    }
}

//Least Recently used
class LRU {
    constructor() {
     this.head = this.tail = null;
     this.map = new Map();
     this.size = 0; // Why I added size, because may be in future we can say if capacity reach to the size, we will remove the tail first and then insert.
    }
    
    get(key) {
        if (this.map.has(key)) {
            const node = this.map.get(key);
            
            if (node !== this.head) {
                this.remove(node);
                this.insert(node);
            }
            
            return node.value;
        }
        
        return -1;
    }
    
    update(key, value) {
        if (this.map.has(key)) {
            let node = this.map.get(key);
            node.value = value;
            
            if (node !== this.head) {
                this.remove(node);
                this.insert(node);
            }
            
            return node.value;
        } else {
            console.log('Key not found'); 
            // Here we can check for capacity if available we can call insert
            // if capacity is not available we will remove the tail and then insert.
        }
    }
    
    remove(node) {
        if (node === this.tail) {
            this.tail = this.tail.prev;
        }
        
        const prevNode = node.prev;
        const nextNode = node.next;
        
        prevNode.next = nextNode;
        nextNode.prev = prevNode;
    }
    
    insert(key, value) {
        const newNode = new Node(key, value);
        this.map.set(key, newNode);
        if (this.head === null) {
            this.head = this.tail = newNode;
            this.size = 1;
            return;
        }
        // We need to insert at the Begining
        newNode.next = this.head;
        this.head.prev = newNode;
        this.head= newNode;
        this.size++;
        return;
    }
}

const test = new LRU();
test.insert('A', 20);
test.insert('B', 10);
test.insert('C', 5);
test.insert('D', 7);

console.log(test);
console.log('------------------');
console.log('C ---> ', test.get('C'));
console.log('D ---> ', test.get('D'));

console.log('D ---> ', test.update('B', 100));

/*
LRU {
  tail: <ref *1> Node {
    key: 'A',
    value: 20,
    next: null,
    prev: Node { key: 'B', value: 10, next: [Circular *1], prev: [Node] }
  },
  head: <ref *2> Node {
    key: 'D',
    value: 7,
    next: Node { key: 'C', value: 5, next: [Node], prev: [Circular *2] },
    prev: null
  },
  map: Map(4) {
    'A' => <ref *1> Node {
      key: 'A',
      value: 20,
      next: null,
      prev: [Node]
    },
    'B' => Node { key: 'B', value: 10, next: [Node], prev: [Node] },
    'C' => Node { key: 'C', value: 5, next: [Node], prev: [Node] },
    'D' => <ref *2> Node {
      key: 'D',
      value: 7,
      next: [Node],
      prev: null
    }
  },
  size: 4
}
------------------
C --->  5
D --->  7
D --->  100
B --->  100
*/
```
Feel free to reach out to me if you have any concerns.
