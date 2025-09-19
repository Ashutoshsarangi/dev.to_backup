**Q. How to find a way to Home / Source to destination using recurssion**

 "XXXXXEX",
 "X     X",
 "XSXXXXX"
-------------------------------------
"XXXXXEX",
"X   X X",
"X   X X",
"X XXX X",
"X     X",
"XSXXXXXX"

From these 2 patterns find out the path from Source to destination


``` javascript
// const maze = [
//     "XXXXXEX",
//     "X     X",
//     "XSXXXXX"
//     ];
const maze = [
    "XXXXXEX",
    "X   X X",
    "X   X X",
    "X XXX X",
    "X     X",
    "XSXXXXXX"
    ];
const dir = [
    [-1, 0],
    [1, 0],
    [0, -1],
    [0, 1]
    ];
    
visited = {};

path = [];

const findPath = (row, col) => {
    //1. out of bound condition
    if (row < 0 || row >= maze.length || col < 0 || col >= maze[0].length) {
        return false;
    }
    
    //2. Already visited 
    if (visited[`${row}_${col}`]) {
        return false;
    }
    
    
    // found road block 
    if (maze[row][col] === 'X') {
        return false;
    }
    
    // found the End
    
    if (maze[row][col] === 'E') {
         path.push(`${row}_${col}`);
        return true;
    }
    
    path.push(`${row}_${col}`);
    visited[`${row}_${col}`] = true;
    
    for (let item of dir) {
        const [x, y] = item;
        if (findPath(row+x, col+y)) {
            return true;
        }
    }
    path.pop();
    return false;
};

findPath(5,1);
// findPath(2,1);
console.log(path)

/*
node /tmp/n2GEk3kzOo.js
[
  '5_1', '4_1', '4_2',
  '4_3', '4_4', '4_5',
  '3_5', '2_5', '1_5',
  '0_5'
]
*/
```

