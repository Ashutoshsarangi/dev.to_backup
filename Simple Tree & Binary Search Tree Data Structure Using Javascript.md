## **Simple Tree**

1. we need to always start with the simple one then step by step we can go to the complex Algorithm.


- Simple Tree
- Binary Tree
- Binary Search Tree Without Balancing the Tree Now

**Tree Traversal**

A. Depth First Start

   I. inOrder
   II. preOrder
   III. postOrder

B. Breath First Search (Queue) (W.I.P)


``` javascript
class SimpleTree {
    constructor(value) {
        this.value = value;
        this.children = [];
    }
    
    insertChild(value) {
        const newChild = new SimpleTree(value);
        const lastElement = this.findLastChild(this);
        lastElement.children.push(newChild);
        
        return newChild;
    }
    
    findLastChild(root) {
        if (root.children.length == 0) {
            return root;
        }
        return this.findLastChild(root.children[0]);
    }
    
    traversal(root) {
        console.log(root.value + ' --> ');
        root.children.forEach(child => {
            this.traversal(child);
        })
    }
}

const simpleTree = new SimpleTree('A');
simpleTree.insertChild('B');
simpleTree.insertChild('C');
simpleTree.insertChild('D');
simpleTree.insertChild('E');
simpleTree.insertChild('F');

console.log(simpleTree)
simpleTree.traversal(simpleTree)

/*
{
    "value": "A",
    "children": [
        {
            "value": "B",
            "children": [
                {
                    "value": "C",
                    "children": [
                        {
                            "value": "D",
                            "children": [
                                {
                                    "value": "E",
                                    "children": [
                                        {
                                            "value": "F",
                                            "children": []
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ]
}
*/

```
## **Binary Tree / Binary Search tree (Without Balancing Tree after removal)**

``` javascript
class BinaryTree {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
    
    insertNode(value) {
        const newNode = new BinaryTree(value);
        const {node: lastNode, side} = this.findAppropriatePlace(this, value);
        lastNode[side] = newNode;
        
        return newNode;
    }
    
    removeFromNode(value) {
       this.findAppropriateNodAndrRemove(this, value);
    }
    
    findAppropriateNodAndrRemove(root, value) {
        const side = root.value < value ? 'right' : 'left';
        
        if (root[side].value == value) {
            root[side] = null;
            return ;
        }
        
        return this.findAppropriateNodAndrRemove(root[side], value);
    }
    // root left right
    preOrderTraversal(root) {
        if (root === null) {
            return ;
        }
        console.log(root.value);
        this.preOrderTraversal(root.left);
        this.preOrderTraversal(root.right);
    }
    
    inOrderTraversal(root) {
        // left root right
         if (root === null) {
            return ;
        }
        this.inOrderTraversal(root.left);
        console.log(root.value);
        this.inOrderTraversal(root.right);
    }
    
    // left right root
    postOrderTraversal(root){
         if (root === null) {
            return ;
        }
        this.postOrderTraversal(root.left);
        console.log(root.value);
        this.postOrderTraversal(root.right)
    }

BFS() { // It will Print as like Tree Level
        const arr = [];
        arr.push(this.root)
        const helper = () => {
            if (arr.length === 0) {
                return;
            }
            const root = arr.shift();
            console.log(root.value);
            if (root.left) {
                arr.push(root.left);
            }
            if (root.right) {
                arr.push(root.right);
            }
            helper()
        }
        helper();
    }
    
    findAppropriatePlace(root, value) {
        const side = root.value < value ? 'right' : 'left';
       
        if (side !== '' && root[side] === null) {
            return {node : root, side};
        }
        if(root.value < value) {
            //right
            return this.findAppropriatePlace(root.right, value);
        } else {
            //left
            return this.findAppropriatePlace(root.left, value);
             
        }
    }
    countNonLeafNodes(root) {
        if (root === null) {
            return 0;
        }
        if (root.left === null && root.right === null) {
            return 0;
        }
        
        return 1 + this.countNonLeafNodes(root.left) + this.countNonLeafNodes(root.right);
    }
    
    countLeafNode(root) {
        if (root === null) {
            return 0;
        }
        
        if (root.left === null && root.right === null) {
            return 1;
        }
        
        return this.countLeafNode(root.left) + this.countLeafNode(root.right);
    }
}

const test = new BinaryTree(20);
test.insertNode(10);
test.insertNode(30);
test.insertNode(5);
test.insertNode(12);
test.insertNode(3);
test.insertNode(6);
test.insertNode(11);
test.insertNode(15);
test.insertNode(25);
test.insertNode(40);
console.log(test);
console.log('-------------preOrderTraversal---------');
test.preOrderTraversal(test);
console.log('-------------inOrderTraversal---------');
test.inOrderTraversal(test)
console.log('-------------postOrderTraversal---------');
test.postOrderTraversal(test)
test.removeFromNode(30);
console.log(test)
console.log('------------------------------------')
console.log(test.countNonLeafNodes(test));
console.log(test.countLeafNode(test));
test.BFS(); // It will print The data as like tree level
/*
{
    "value": 20,
    "left": {
        "value": 10,
        "left": {
            "value": 5,
            "left": {
                "value": 3,
                "left": null,
                "right": null
            },
            "right": {
                "value": 6,
                "left": null,
                "right": null
            }
        },
        "right": {
            "value": 12,
            "left": {
                "value": 11,
                "left": null,
                "right": null
            },
            "right": {
                "value": 15,
                "left": null,
                "right": null
            }
        }
    },
    "right": {
        "value": 30,
        "left": {
            "value": 25,
            "left": null,
            "right": null
        },
        "right": {
            "value": 40,
            "left": null,
            "right": null
        }
    }
}

-------------preOrderTraversal---------
20
10
5
3
6
12
11
15
30
25
40
-------------inOrderTraversal---------
3
5
6
10
11
12
15
20
25
30
40
-------------postOrderTraversal---------
3
5
6
10
11
12
15
20
25
30
40
------------------- **After deleting node 30** ------------
BinaryTree {
  value: 20,
  left: BinaryTree {
    value: 10,
    left: BinaryTree { value: 5, left: [BinaryTree], right: [BinaryTree] },
    right: BinaryTree { value: 12, left: [BinaryTree], right: [BinaryTree] }
  },
  right: null
}
countNonLeafNodes:- 4
countLeafNode:- 4

*/
```
