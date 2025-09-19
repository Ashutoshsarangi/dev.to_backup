This algorithm is used to calculate minimum shortest distance between cities.

along with the attached article, if you wanted to learn more, I added another enhancement.

1. I calculated previous path and from there we can get the complete path how it reached there.


``` javascript

const dijkstra = (graph) => {
    const vertex = graph.length;
    const path = new Array(vertex).fill(false);
    const distance = new Array(vertex).fill(Infinity);
    const prev = [-1];
    distance[0] = 0; // source Node
    
    const getMinDistanceIndex = (path, distance) => {
        let min = Infinity;
        let minIndex = -1;
        
        for (let j = 0; j< vertex; j++) {
            if (path[j] == false && min > distance[j]) {
                min = distance[j];
                minIndex = j;
            }    
        }    
        
        return minIndex;
    }
    
    for (let i = 0; i < vertex; i++) {
        const minDistanceIndex = getMinDistanceIndex(path, distance);
        path[minDistanceIndex] = true;
        
        for (let j = 0; j< vertex; j++) {
            if (path[j] == false && graph[minDistanceIndex][j] > 0 && distance[minDistanceIndex] + graph[minDistanceIndex][j] < distance[j]) {
                distance[j] = distance[minDistanceIndex] + graph[minDistanceIndex][j];
                prev[j] = minDistanceIndex;
            }
        }
    }
    
    console.log(path, distance, prev);
}

const graph = [ [ 0, 4, 0, 0, 0, 0, 0, 8, 0 ],
              [ 4, 0, 8, 0, 0, 0, 0, 11, 0 ],
              [ 0, 8, 0, 7, 0, 4, 0, 0, 2 ],
              [ 0, 0, 7, 0, 9, 14, 0, 0, 0],
              [ 0, 0, 0, 9, 0, 10, 0, 0, 0 ],
              [ 0, 0, 4, 14, 10, 0, 2, 0, 0],
              [ 0, 0, 0, 0, 0, 2, 0, 1, 6 ],
              [ 8, 11, 0, 0, 0, 0, 1, 0, 7 ],
              [ 0, 0, 2, 0, 0, 0, 6, 7, 0 ]];
              
dijkstra(graph);
/*
[true, true, true, true, true, true, true, true, true]
[0, 4, 12, 19, 21, 11, 9,  8, 14]
[-1, 0, 1, 2, 5, 6, 7, 0, 2]
*/
```
 Feel free to reach out to me if you have any concerns

**Reference**
https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/
