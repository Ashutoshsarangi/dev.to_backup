An **adjacency list** and an **adjacency matrix** are two common ways to represent a **graph** in computer science.  

**Adjacency List:** 

1. An adjacency list represents a graph as an array of linked lists.
2. The index of the array represents a vertex and each element in its linked list represents the other vertices that form an edge with the vertex.  

**Pros:**  

1. Space efficient for representing sparse graphs (graphs with fewer edges).
2. Adding a vertex is easier.

**Cons:**
  
1. Less efficient for some types of queries, such as checking whether an edge exists between two vertices.
More complex data structure.

**Adjacency Matrix:** 

1. An adjacency matrix represents a graph as a two-dimensional array, where the cell at the ith row and jth column indicates an edge between vertices i and j.  

**Pros:**  
1. Simple to understand and implement.
2. Efficient for dense graphs (graphs with more edges).
3. Quick to check whether an edge exists between two vertices.

**Cons:**
  
1. Requires more space (O(V^2), where V is the number of vertices).
Adding a vertex is O(V^2), which can be slower than an adjacency list.

**important note**

1. Inform the interviewer beforehand which approach you will follow and tell him / her the pros and cons.


**Graph Traversal**

1. DFS (Depth First Search) (Stack)
2. BFS (Breath First Search) (Queue)
   
**Finding the shortest path BFS would be better**

**Directed vs Undirected Graphs:**

1. **A directed graph**, also called a digraph, is a graph where each edge has a direction. The edges point from one vertex to another.

2. **An undirected graph** is a graph in which edges have no orientation. The edge (x, y) is identical to the edge (y, x).

**Weighted vs Unweighted Graphs:**
  
1. **A weighted graph** is a graph in which each edge is assigned a weight or cost. This is useful in problems where certain edges have different importance or length.

2. **An unweighted graph** is a graph in which all edges are of equal weight or cost.

**Self Loop:**  

1. A self-loop is an edge that connects a vertex to itself.

**Sparse vs Dense Graphs:**

1. A **sparse graph** is a graph in which the number of edges is close to the minimal number of edges. In other words, there are very few edges between vertices.

2. **A dense graph** is a graph in which the number of edges is close to the maximum possible number of edges. In other words, there are many edges between vertices.

**Cyclic vs Acyclic Graphs:**

1. **A cyclic graph** is a graph that contains at least one cycle (a path of edges and vertices wherein a vertex is reachable from itself).

2. **An acyclic graph** is a graph with no cycles. A special type of acyclic graph called a tree, is a connected, undirected graph with no cycles.

```
// Weighted graph adjacency list would look like

{
1: [ {node: 2, weight: 50}, {node: 3, weight: 60}]
...
6: [{node: 1, weight: 40}, {node:5, weight:30 }, {node:4, weight: 90}]
}
```

``` javascript
class Graph {
    constructor() {
        this.adjList = {};
    }
    
    addNode(value) {
        this.adjList[value] = []
    }
    
    addEdge(node1, node2) {
        this.adjList[node1].push(node2);
        this.adjList[node2].push(node1);
    }
    
    removeEdge(node1, node2) {
        this.removeElement(node1, node2);
        this.removeElement(node2, node1);
    }
    
    removeElement(node, value) {
        const index = this.adjList[node].indexOf(value);
        this.adjList[node] = [...this.adjList[node].slice(0, index), ...this.adjList[node].slice(index+1)];
    }
    
    removeNode(node) {
        const connectedNodes = this.adjList[node];
    
        for (let connectedNode of connectedNodes) {
            this.removeElement(connectedNode, node);
        }
        
        delete this.adjList[node];
    }
depthFirstTraversal(startNode) {
        const stack = [];
        const visited = {};
        
        stack.push(startNode);
        visited[startNode] = true;
        
        while(stack.length > 0) {
            const currentNode = stack.pop();
            const connectedNodes = this.adjList[currentNode];
            console.log(currentNode);
            connectedNodes.forEach(connectedNode => {
                if (!visited[connectedNode]) {
                    visited[connectedNode] = true;
                    stack.push(connectedNode);
                }
            })
        }
    }
    
    breathFirstTraversal(startNode) {
        const queue = [];
        const visited = {}
        
        queue.push(startNode);
        visited[startNode] = true;
        
        while(queue.length > 0) {
            const currentElement = queue.shift();
            const connectedNodes = this.adjList[currentElement];
            console.log(currentElement);
            connectedNodes.forEach(connectedNode => {
                if (!visited[connectedNode]) {
                    visited[connectedNode]=true;
                    queue.push(connectedNode);
                }
            });
        }
    }
}

const test = new Graph();

test.addNode(1);
test.addNode(2);
test.addNode(3);
test.addNode(4);
test.addNode(5);
test.addNode(6);
test.addEdge(1,2)
test.addEdge(1,3)
test.addEdge(1,6)
test.addEdge(2, 3);
test.addEdge(2, 5);
test.addEdge(2, 4);
test.addEdge(3, 4);
test.addEdge(3, 5);
test.addEdge(4, 5);
test.addEdge(4, 6);
test.addEdge(5, 6);
console.log('After adding all node and Edge --> ', test.adjList)

test.removeNode(4);

console.log('After Removing node 4 --> ', test.adjList)
console.log('----------Depth First Traversal -------------')
test.depthFirstTraversal(1);
console.log('----------Breath First Traversal -------------')
test.breathFirstTraversal(1);

/*
After adding all node and Edge -->  {
  '1': [ 2, 3, 6 ],
  '2': [ 1, 3, 5, 4 ],
  '3': [ 1, 2, 4, 5 ],
  '4': [ 2, 3, 5, 6 ],
  '5': [ 2, 3, 4, 6 ],
  '6': [ 1, 4, 5 ]
}
After Removing node 4 -->  {
  '1': [ 2, 3, 6 ],
  '2': [ 1, 3, 5 ],
  '3': [ 1, 2, 5 ],
  '5': [ 2, 3, 6 ],
  '6': [ 1, 5 ]
}
----------Depth First Traversal -------------
1
6
5
3
2
----------Breath First Traversal -------------
1
2
3
6
5
*/
```


