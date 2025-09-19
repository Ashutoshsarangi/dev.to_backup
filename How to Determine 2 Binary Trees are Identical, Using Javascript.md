## Introduction

Here identical means both structure and values are in the same position.

To achieve this we need to use DFS algorithm so it will check depth as well. 

This can't be achieved using BFS Algo.

So here I am using In Order Traversal to get the result.

``` javascript
class Node {
    constructor(data)
    {
        this.left = null;
        this.right = null;
        this.data = data;
    }
}

let root1, root2;

// left root right
const checkIdentical = (binaryTree1, binaryTree2) => {
    let tree = '';
    const helper = (root) => {
        if (root == null) {
            return tree;
        }
        helper(root.left);
        tree += root.data;
        helper(root.right);
        
        return tree;
    };
    
    const tree1 = helper(binaryTree1);
    tree = '';
    const tree2 = helper(binaryTree2);
    if (tree1 === tree2) {
        console.log('Both are identical');
    } else {
        console.log('Not Identical');
    }
    
}

root1 = new Node(1);
root1.left = new Node(2);
root1.right = new Node(3);
root1.left.left = new Node(4);
root1.left.right = new Node(5);

root2 = new Node(1);
root2.left = new Node(2);
root2.right = new Node(3);
root2.left.left = new Node(4);
root2.left.right = new Node(5);
checkIdentical(root1, root2);

/*
Both are identical

*/
```

Feel free to reach out to me if you have any concerns
