## Introduction

A Trie, also known as a prefix tree, is a specialized tree-based data structure that is used for efficient information retrieval. 

It's particularly useful for use cases that involve searching and prefix matching within strings. 

1. If I tell you about Trie Algorithm you may or may not be interested in this algorithm

2. But if I would tell you you can create a **autocomplete algorithm** using this. you will be more excited to learn this.



**Use Case of this Algorithm**

**1. Autocomplete:** 

a. Tries are often used in search engines or text editors to implement the autocomplete feature.
b. As you start typing, the application suggests possible completions based on the prefix you've entered.  

**2. Spell Checkers:** 

a. Tries can be used to implement spell checkers. If a word isn't present in the trie, it's likely misspelled. 
b. The trie can also suggest corrections by finding similar words.  

**3. IP Routing:**

a. Tries are used in routers to store routing tables. 
b. The router uses a trie to match the longest prefix, which determines the next hop for a packet.

**4. Efficiently Storing and Searching for Strings:** 

a. If you have a dataset of strings where there's a lot of shared prefixes, a trie can store these strings using less space than storing them individually.
b.  The search operation is also efficient, with time complexity proportional to the length of the string you're searching for.


```javascript
class Node {
    constructor() {
        this.end = false;
        this.children = {}
    }
}

class Trie {
    constructor() {
        this.root = new Node ();
    }
    
    insert(word) {
        let head = this.root;
        
        for (let i = 0; i< word.length; i++) {
            if (!head.children[word[i]]) {
                head.children[word[i]] = new Node();
            }
            head = head.children[word[i]];
        }
        head.end = true;
    }
    
    search(word){
        let current = this.root;
        
        for (let i = 0; i < word.length; i++) {
            if (!current.children[word[i]]) {
                return false;
            }
            current = current.children[word[i]]
        }
        
        return true;
    }
    
    autoComplete(word) {
        let current = this.root;
        
        for (let i = 0; i< word.length; i++) {
            if (!current.children[word[i]]) {
                return false;
            }
            current = current.children[word[i]];
        }
        if (Object.keys(current.children).length === 1) {
            console.log('Please Type More...');
            return;
        }
        console.log('children =---> ', current.children);
        
        console.log('Possible Auto Complete Values are --->');
        for (let key in current.children) {
            console.log('---> ', word+key);
        }
    }
}

const test = new Trie();
test.insert('ant');
test.insert('any');
console.log(test.search('ant'));
console.log(test.search('any'));
console.log(test.search('anj'));
test.autoComplete('an')
/*
true
true
false
children =--->  {
  t: Node { end: true, children: {} },
  y: Node { end: true, children: {} }
}
Possible Auto Complete Values are --->
--->  ant
--->  any
*/

```
Feel free to reach out to me if you have any concerns/queries. 

