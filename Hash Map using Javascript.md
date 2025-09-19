## Introduction

- A Hash Map, also known as a Hash Table, is a data structure that implements an associative array abstract data type, a structure that can map keys to values. 
- It uses a hash function to compute an index into an array of buckets or slots, from which the desired value can be found.  

- The primary advantage of a Hash Map is its efficiency. Operations like inserting a new key-value pair, deleting a key-value pair, and looking up a value given a key are all very fast, often taking constant time on average.

## Implementing a Simple Hash Map in JavaScript

```javascript
let hashMap = {};
hashMap['key1'] = 'value1';
hashMap['key2'] = 'value2';
console.log(hashMap['key1']); // Outputs: value1
```

## Handling Collisions

- Handling collisions is an important aspect of implementing a Hash Map. A collision occurs when two different keys produce the same hash. There are several strategies to handle collisions, but the two most common ones are **separate chaining and linear probing.**

**Separate Chaining**: In separate chaining, each slot in the hash table's array contains a linked list (or another data structure that can hold multiple items). When a collision occurs, the new key-value pair is added to the end of the linked list at the corresponding index.

Here's a simple implementation of a Hash Map using separate chaining in JavaScript:

```javascript
class HashMap {
  constructor() {
    this.table = new Array(100).fill(null).map(() => []);
  }

  put(key, value) {
    const index = this.hash(key);
    const chain = this.table[index];
    const existingPair = chain.find(([existingKey]) => existingKey === key);

    if (existingPair) {
      existingPair[1] = value;
    } else {
      chain.push([key, value]);
    }
  }

  get(key) {
    const index = this.hash(key);
    const chain = this.table[index];
    const pair = chain.find(([existingKey]) => existingKey === key);

    if (pair) {
      return pair[1];
    }

    return null;
  }

  hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % this.table.length;
  }
}
```

**Linear Probing**: In linear probing, when a collision occurs, the hash map checks the next slot in the array (and continues to the next one if that's also full, and so on) until it finds an empty slot where it can store the new key-value pair.

Here's a simple implementation of a Hash Map using linear probing in JavaScript:

```javascript
class HashMap {
  constructor() {
    this.table = new Array(100).fill(null);
  }

  put(key, value) {
    let index = this.hash(key);
    while (this.table[index] !== null) {
      index = (index + 1) % this.table.length;
    }
    this.table[index] = [key, value];
  }

  get(key) {
    let index = this.hash(key);
    while (this.table[index] !== null) {
      if (this.table[index][0] === key) {
        return this.table[index][1];
      }
      index = (index + 1) % this.table.length;
    }
    return null;
  }

  hash(key) {
    let hash = 0;
    for (let i = 0; i < key.length; i++) {
      hash += key.charCodeAt(i);
    }
    return hash % this.table.length;
  }
}
```

In both examples, the `hash` method is a simple hash function that converts the key into an integer that is used as an index in the array. In a real-world scenario, you would likely use a more complex hash function to reduce the likelihood of collisions.
