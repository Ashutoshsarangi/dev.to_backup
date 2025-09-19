This article is a simple part of the graph where we are just doing BFS and DFS Traversal using both Graph approaches

1. using adjacent Matrix (BFS)
2. using an Adjacent List (DFS)


```javascript
const adjMatrix = [
    [0, 1, 1, 0, 0],
    [1, 0, 0, 1, 0],
    [1, 0, 0, 0, 1],
    [0, 1, 0, 0, 1],
    [0, 0, 1, 1, 0]
];

const BFS = () => {
    const q = [0];
    const visited = [0];
    let path = '';
    
    while(q.length) {
        const value = q.shift();
        path += value;
        
        for(let j = 0; j< adjMatrix.length; j++) {
// j Means the Node present / not in visited List
            if (adjMatrix[value][j] && visited.indexOf(j) < 0) {
                q.push(j);
                visited.push(j);
            }
        }
    }
    console.log(path);
}

BFS();

// 01234
```

```javascript
const adjList = {
    0: [1, 2],
    1: [0, 3],
    2: [0, 4],
    3: [1, 4],
    4: [2, 3]
}

const DFS = () => {
    const stack = [0];
    const visited = [0];
    let path = '';
    
    while(stack.length) {
        const value = stack.pop();
        path += value;
        
        for(let item of adjList[value]) {
            if (visited.indexOf(item) < 0) {
                stack.push(item);
                visited.push(item);
            }
        }
    }
    console.log(path);
}

DFS();// 02431
```
For a more detailed article on Graph feel free to check out the below link.

[Graphs Data Structure using Javascript](https://dev.to/ashutoshsarangi/approaching-graphs-data-structure-using-javascript-4021)
