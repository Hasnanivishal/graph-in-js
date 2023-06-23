# Graph Data Structure And Algorithms Using JavaScript

1. <details>
    <summary>
        <b>Create a Graph using Adjacency List?
        </b>
    </summary>
     <p>
       
    ```javascript
    class Graph {
      constructor() {
        this.adjacencyList = new Map();
      }  

      addVertex(node) {
        this.adjacencyList.set(node, []);
      }

      addEdges(node1, node2){
        this.adjacencyList.get(node1).push(node2);
        this.adjacencyList.get(node2).push(node1);
      }

      getEdges(node) {
        return this.adjacencyList.get(node);
      }
    }

      let graph = new Graph();

      graph.addVertex(0);
      graph.addVertex(1);
      graph.addVertex(2);
      graph.addVertex(3);
      graph.addVertex(4);


      graph.addEdges(0,1);
      graph.addEdges(1,2);
      graph.addEdges(0,3);
      graph.addEdges(3,4);


      console.log('edges for vertex 0 is', graph.getEdges(0));
      console.log('edges for vertex 1 is', graph.getEdges(1));
      console.log('edges for vertex 2 is', graph.getEdges(2));
      console.log('edges for vertex 3 is', graph.getEdges(3));
      console.log('edges for vertex 4 is', graph.getEdges(4));
      ```
     </p>
  </details>

---

2. <details>
    <summary>
        <b>Perform Breadth First Search(BFS) Traversal?
        </b>
    </summary>
     <p>
       
    ```javascript
           class Graph {
              constructor() {
                this.adjacencyList = new Map();
              }  
            
              addVertex(node) {
                this.adjacencyList.set(node, []);
              }
            
              addEdges(node1, node2){
                this.adjacencyList.get(node1).push(node2);
                this.adjacencyList.get(node2).push(node1);
              }
            
              getEdges(node) {
                return this.adjacencyList.get(node);
              }
              
              // BFS 
              breathSearchFirstTraversal(startingNode) {
                this.visitedNodes = new Set();
                this.queue = [];
                
                // add starting node
                this.visitedNodes.add(startingNode);
                
                this.queue.push(startingNode);
                
                
                while(this.queue.length != 0) {
                  // get the first element from queue
                  let currentNode = this.queue.shift();
                  
                  console.log("Node - " + currentNode + ", " );
                  let adjencyNodes = this.adjacencyList.get(currentNode);
                  
                  for(let adjencyNode of adjencyNodes) 
                  {
                    if(!this.visitedNodes.has(adjencyNode)) {
                        // push into visited Array
                        this.visitedNodes.add(adjencyNode);
                        // push into queue to be scaned further
                        this.queue.push(adjencyNode);
                    }
                  }
                }
              }
            }
        
        
        let graph = new Graph();
        
        graph.addVertex(0);
        graph.addVertex(1);
        graph.addVertex(2);
        graph.addVertex(3);
        graph.addVertex(4);
        
        graph.addEdges(0,1);
        graph.addEdges(1,2);
        graph.addEdges(0,3);
        graph.addEdges(3,4);
        
        console.log('**** BFS *****')
        graph.breathSearchFirstTraversal(0);
     ```
     </p>
  </details>
  
---
  
3. <details>
    <summary>
        <b>Perform Depth First Search(DFS) Traversal?
        </b>
    </summary>
     <p>
       
    ```javascript
       class Graph {
          constructor() {
            this.adjacencyList = new Map();
          }  
        
          addVertex(node) {
            this.adjacencyList.set(node, []);
          }
        
          addEdges(node1, node2){
            this.adjacencyList.get(node1).push(node2);
            this.adjacencyList.get(node2).push(node1);
          }
        
          getEdges(node) {
            return this.adjacencyList.get(node);
          }
          
          // DFS 
          depthSearchFirstTraversal(startingNode) {
            // create an array for visited nodes
            let visitedNodes = new Set();
            // call the dfs method
            this.DFSHelper(startingNode, visitedNodes);
          }
          
          DFSHelper(startingNode, visitedNodes) {
              
            // add the startingNode node in visited array 
            visitedNodes.add(startingNode);
            
            console.log("Node - " + startingNode + ", ");
            
            let adjencyNodes = this.adjacencyList.get(startingNode);
            
            // iterate over all the adjency nodes of the starting nodes
            for(let adjencyNode of adjencyNodes) {
              
              // if node is not visited
              if(!visitedNodes.has(adjencyNode)) {
                // use recursion to reach at the depth of the graph
                this.DFSHelper(adjencyNode, visitedNodes);
              }
            }
          }
        }

        let graph = new Graph();
        
        graph.addVertex(0);
        graph.addVertex(1);
        graph.addVertex(2);
        graph.addVertex(3);
        graph.addVertex(4);
        
        graph.addEdges(0,1);
        graph.addEdges(1,2);
        graph.addEdges(0,3);
        graph.addEdges(3,4);
        
        console.log('**** DFS *****')
        graph.depthSearchFirstTraversal(0);
     ```
     </p>
  </details>

---

4. <details>
    <summary>
        <b>Determine the level (Distance from the starting node) of each node using BFS Or DFS?
        </b>
    </summary>
     <p>
       
    ```javascript
     class Graph {

      constructor() {
        this.adjacencyList = new Map();
      }  
    
      addVertex(node) {
        this.adjacencyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjacencyList.get(node1).push(node2);
        this.adjacencyList.get(node2).push(node1);
      }
    
      getEdges(node) {
        return this.adjacencyList.get(node);
      }
      
      // BFS 
      breathSearchFirstTraversal(startingNode) {
        this.visitedNodes = new Set();
        this.queue = [];
        
        // add starting node
        this.visitedNodes.add(startingNode);
        
        this.queue.push({currentNode: startingNode, level: 0});
        
        
        while(this.queue.length != 0) {
          // get the first element from queue
          let { currentNode, level }  = this.queue.shift();
          
          console.log("Node - " + currentNode + ", level - " + level);
          let adjencyNodes = this.adjacencyList.get(currentNode);
          
          for(let adjencyNode of adjencyNodes) 
          {
            if(!this.visitedNodes.has(adjencyNode)) {
                // push into visited Array
                this.visitedNodes.add(adjencyNode);
                // push into queue to be scaned further
                this.queue.push({currentNode: adjencyNode, level: level + 1});
            }
          }
        }
      }
      
      // DFS 
      depthSearchFirstTraversal(startingNode) {
        // create an array for visited nodes
        let visitedNodes = new Set();
        // call the dfs method
        this.DFSHelper({startingNode: startingNode, level: 0}, visitedNodes);
      }
      
      DFSHelper(nodeObj, visitedNodes) {
        
        let { startingNode, level }  = nodeObj;
        
        // add the startingNode node in visited array 
        visitedNodes.add(startingNode);
        
        console.log("Node - " + startingNode + ", level - " + level);
        
        let adjencyNodes = this.adjacencyList.get(startingNode);
        
        // iterate over all the adjency nodes of the starting nodes
        for(let adjencyNode of adjencyNodes) {
          
          // if node is not visited
          if(!visitedNodes.has(adjencyNode)) {
            // use recursion to reach at the depth of the graph
            this.DFSHelper({startingNode: adjencyNode, level: level+1}, visitedNodes);
          }
          
        }
      }
    }

    let graph = new Graph();
    
    graph.addVertex(0);
    graph.addVertex(1);
    graph.addVertex(2);
    graph.addVertex(3);
    graph.addVertex(4);
    
    
    graph.addEdges(0,1);
    graph.addEdges(1,2);
    graph.addEdges(0,3);
    graph.addEdges(3,4);
    
    console.log('**** BFS *****')
    graph.breathSearchFirstTraversal(0);
    
    console.log('**** DFS *****')
    graph.depthSearchFirstTraversal(0);
     ```
     </p>
  </details>

  ---

5. <details>
    <summary>
        <b>
            Determine the level (Distance from the starting node) of each node using BFS Or DFS on a Components Graph?
        </b>
    </summary>
     <p>
       
    ```javascript
    class Graph {
      constructor() {
        this.adjacencyList = new Map();
      }  
    
      addVertex(node) {
        this.adjacencyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjacencyList.get(node1).push(node2);
        this.adjacencyList.get(node2).push(node1);
      }
    
      getEdges(node) {
        return this.adjacencyList.get(node);
      }
      
      // BFS on Components Graph
      performBFSOnComponentGraph() {
        // Create a visited nodes array
        this.visitedNodes = new Set();
        
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        for(const node of this.adjacencyList.keys()) {
          // Run the BFS on non visited nodes only
          if(!this.visitedNodes.has(node)) {
            // Calls the BFS with key as starting node 
            this.breathSearchFirstTraversal(node);
          }
        }
      }
      
      // DFS on Components Graph
      performDFSOnComponentGraph() {
        // Create a visited nodes array
        this.visitedNodes = new Set();
        
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        for(const node of this.adjacencyList.keys()) {
          // Run the DFS on non visited nodes only
          if(!this.visitedNodes.has(node)) {
            // Calls the DFS with key as starting node 
            this.DFSHelper({startingNode: node, level: 0});
          }
        }
      }
    
      DFSHelper(nodeObj) {
        let { startingNode, level }  = nodeObj;
        
        // add the startingNode node in visited array 
        this.visitedNodes.add(startingNode);
        
        console.log("Node - " + startingNode + ", level - " + level);
        
        let adjencyNodes = this.adjacencyList.get(startingNode);
        
        // iterate over all the adjency nodes of the starting nodes
        for(let adjencyNode of adjencyNodes) {
          
          // if node is not visited
          if(!this.visitedNodes.has(adjencyNode)) {
            // use recursion to reach at the depth of the graph
            this.DFSHelper({startingNode: adjencyNode, level: level+1}, this.visitedNodes);
          }
        }
      }
      
    // BFS 
      breathSearchFirstTraversal(startingNode) {
        this.visitedNodes = new Set();
        this.queue = [];
        
        // add starting node
        this.visitedNodes.add(startingNode);
        
        this.queue.push({currentNode: startingNode, level: 0});
        
        
        while(this.queue.length != 0) {
          // get the first element from queue
          let { currentNode, level }  = this.queue.shift();
          
          console.log("Node - " + currentNode + ", level - " + level);
          let adjencyNodes = this.adjacencyList.get(currentNode);
          
          for(let adjencyNode of adjencyNodes) 
          {
            if(!this.visitedNodes.has(adjencyNode)) {
                // push into visited Array
                this.visitedNodes.add(adjencyNode);
                // push into queue to be scaned further
                this.queue.push({currentNode: adjencyNode, level: level + 1});
            }
          }
        }
      }
    }
    
      let graph = new Graph();
    
      graph.addVertex(0);
      graph.addVertex(1);
      graph.addVertex(2);
      graph.addVertex(3);
      graph.addVertex(4);
      graph.addVertex(5);
    
    
      graph.addEdges(0,1);
      graph.addEdges(1,2);
      graph.addEdges(2,0);
      graph.addEdges(3,4);
    
        console.log('**** BFS *****')
        graph.performBFSOnComponentGraph();
        
        console.log('**** DFS *****')
        graph.performDFSOnComponentGraph();
     ```
     </p>
  </details>

---

6. <details>
    <summary>
        <b>
            Check if the given undirected graph is having any cycle or not?
        </b>
    </summary>
     <p>
       
    ```javascript
     class Graph {
    
      constructor() {
        this.adjacencyList = new Map();
      }  
    
      addVertex(node) {
        this.adjacencyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjacencyList.get(node1).push(node2);
        this.adjacencyList.get(node2).push(node1);
      }
    
      getEdges(node) {
        return this.adjacencyList.get(node);
      }
      
      // BFS 
      breathSearchFirstTraversal(startingNode) {
        this.visitedNodes = new Set();
        this.queue = [];
        
        // add starting node
        this.visitedNodes.add(startingNode);
        
        this.queue.push({ currentNode: startingNode, parentNode: -1 });
        
        
        while(this.queue.length != 0) {
          // get the first element from queue
          let { currentNode, parentNode }  = this.queue.shift();
          
          console.log("Node - " + currentNode + ", parentNode - " + parentNode);
          let adjencyNodes = this.adjacencyList.get(currentNode);
          
          for(let adjencyNode of adjencyNodes) 
          {
            if(!this.visitedNodes.has(adjencyNode)) {
                // push into visited Array
                this.visitedNodes.add(adjencyNode);
                // push into queue to be scaned further
                this.queue.push({currentNode: adjencyNode, parentNode: currentNode});
            } 
            
            
            // Check if the visited node is not the parent of the current node
            else if (parentNode != adjencyNode) {
              return true;
            }
            
          }
        }
        
        // return false if no cycles found
        return false;
      }
      
      // DFS 
      depthSearchFirstTraversal(startingNode) {
        // create an array for visited nodes
        let visitedNodes = new Set();
        // call the dfs method
        return this.DFSHelper({ startingNode: startingNode, parentNode: -1 }, visitedNodes);
      }
      
      DFSHelper(nodeObj, visitedNodes) {
        
        let { startingNode, parentNode }  = nodeObj;
        
        // add the startingNode node in visited array 
        visitedNodes.add(startingNode);
        
        console.log("Node - " + startingNode + ", parentNode - " + parentNode);
        
        let adjencyNodes = this.adjacencyList.get(startingNode);
        
        // iterate over all the adjency nodes of the starting nodes
        for(let adjencyNode of adjencyNodes) {
          
          // if node is not visited
          if(!visitedNodes.has(adjencyNode)) {
            // use recursion to reach at the depth of the graph
            let isCyleInRecurssion = this.DFSHelper({ startingNode: adjencyNode, parentNode: startingNode }, visitedNodes);
            
            
            // check if any nested recursion has cycle break the loop by returning true
            if (isCyleInRecurssion == true) return true;
            
    
          }
          
          
          // Check if the visited node is not the parent of the current node
          else if (parentNode != adjencyNode) {
            return true;
          }
          
        }
        
        // return false if no cycles found
        return false;
      }
    }
    
    let graph = new Graph();
    
    graph.addVertex(0);
    graph.addVertex(1);
    graph.addVertex(2);
    graph.addVertex(3);
    graph.addVertex(4);
    graph.addVertex(5);
    
    
    graph.addEdges(0,1); 
    graph.addEdges(1,2);
    graph.addEdges(2,3);
    graph.addEdges(0,4);
    graph.addEdges(4,5);
    graph.addEdges(5,3);
    
    console.log('**** BFS *****')
    let isCycleBfs = graph.breathSearchFirstTraversal(0);
    
    console.log("Graph contains cycles (BFS) -", (isCycleBfs ? 'Yes': 'No'));
    
    console.log('**** DFS *****')
    let isCycleDfs = graph.depthSearchFirstTraversal(0);
    console.log("Graph contains cycles (DFS) -", (isCycleDfs ? 'Yes': 'No'));
     ```
     </p>
  </details>

---

7. <details>
    <summary>
        <b>
            Check if the given a Components undirected graph is having any cycle or not?
        </b>
    </summary>
     <p>
       
    ```javascript
     class Graph {
    
      constructor() {
        this.adjacencyList = new Map();
      }  
    
      addVertex(node) {
        this.adjacencyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjacencyList.get(node1).push(node2);
        this.adjacencyList.get(node2).push(node1);
      }
    
      getEdges(node) {
        return this.adjacencyList.get(node);
      }
      
      // BFS on Components Graph
      performBFSOnComponentGraph() {
        // Create a visited nodes array
        this.visitedNodes = new Set();
        
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        for(const node of this.adjacencyList.keys()) {
          // Run the BFS on non visited nodes only
          if(!this.visitedNodes.has(node)) {
            // Calls the BFS with key as starting node 
            if(this.breathSearchFirstTraversal(node) == true) {
              return true;
            }
          }
        }
        
        return false;
      }
      
      // BFS 
      breathSearchFirstTraversal(startingNode) {
        this.visitedNodes = new Set();
        this.queue = [];
        
        // add starting node
        this.visitedNodes.add(startingNode);
        
        this.queue.push({ currentNode: startingNode, parentNode: -1 });
        
        
        while(this.queue.length != 0) {
          // get the first element from queue
          let { currentNode, parentNode }  = this.queue.shift();
          
          console.log("Node - " + currentNode + ", parentNode - " + parentNode);
          let adjencyNodes = this.adjacencyList.get(currentNode);
          
          for(let adjencyNode of adjencyNodes) 
          {
            if(!this.visitedNodes.has(adjencyNode)) {
                // push into visited Array
                this.visitedNodes.add(adjencyNode);
                // push into queue to be scaned further
                this.queue.push({currentNode: adjencyNode, parentNode: currentNode});
            } 
            
            
            // Check if the visited node is not the parent of the current node
            else if (parentNode != adjencyNode) {
              return true;
            }
            
          }
        }
        
        // return false if no cycles found
        return false;
      }
      
      // DFS 
      // DFS on Components Graph
      performDFSOnComponentGraph() {
        // Create a visited nodes array
        this.visitedNodes = new Set();
        
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        for(const node of this.adjacencyList.keys()) {
          // Run the DFS on non visited nodes only
          if(!this.visitedNodes.has(node)) {
            // Calls the DFS with key as starting node 
            if(this.DFSHelper({startingNode: node, parentNode: -1}) == true) {
              return true;
            }
          }
        }
        
        return false;
      }
      
      DFSHelper(nodeObj) {
        
        let { startingNode, parentNode }  = nodeObj;
        
        // add the startingNode node in visited array 
        this.visitedNodes.add(startingNode);
        
        console.log("Node - " + startingNode + ", parentNode - " + parentNode);
        
        let adjencyNodes = this.adjacencyList.get(startingNode);
        
        // iterate over all the adjency nodes of the starting nodes
        for(let adjencyNode of adjencyNodes) {
          
          // if node is not visited
          if(!this.visitedNodes.has(adjencyNode)) {
            // use recursion to reach at the depth of the graph
            let isCyleInRecurssion = this.DFSHelper({ startingNode: adjencyNode, parentNode: startingNode });
            
            
            // check if any nested recursion has cycle break the loop by returning true
            if (isCyleInRecurssion == true) return true;
            
    
          }
          
          
          // Check if the visited node is not the parent of the current node
          else if (parentNode != adjencyNode) {
            return true;
          }
          
        }
        
        // return false if no cycles found
        return false;
      }
    }
    
    let graph = new Graph();
    
    graph.addVertex(0);
    graph.addVertex(1);
    graph.addVertex(2);
    graph.addVertex(3);
    graph.addVertex(4);
    graph.addVertex(5);
    
    graph.addVertex(6);
    graph.addVertex(7);
    graph.addVertex(8);
    
    graph.addEdges(0,1); 
    graph.addEdges(1,2);
    graph.addEdges(2,3);
    graph.addEdges(0,4);
    graph.addEdges(4,5);
    
    graph.addEdges(6,7);
    graph.addEdges(7,8);
    graph.addEdges(8,6);
    
    console.log('**** BFS *****')
    let isCycleBfs = graph.performBFSOnComponentGraph();
    
    console.log("Graph contains cycles (BFS) -", (isCycleBfs ? 'Yes': 'No'));
    
    console.log('**** DFS *****')
    let isCycleDfs = graph.performDFSOnComponentGraph();
    console.log("Graph contains cycles (DFS) -", (isCycleDfs ? 'Yes': 'No'));
     ```
     </p>
  </details>

---

8. <details>
    <summary>
        <b>
            Check if the given a Components Directed graph is having any cycle or not?
        </b>
    </summary>
     <p>
       
    ```javascript
     class Graph {

      constructor() {
        this.adjacencyList = new Map();
      }  
    
      addVertex(node) {
        this.adjacencyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjacencyList.get(node1).push(node2);
      }
    
      getEdges(node) {
        return this.adjacencyList.get(node);
      }
    
      // Only DFS as BFS will not work on directed graph to detect cycles
      performDFSOnComponentGraph() {
          
        // Create a visited nodes array
        this.visitedNodes = new Set();
        
        // create an array for keeping information about the current path    
        this.visitedPath = new Set();
        
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        for(const node of this.adjacencyList.keys()) {
          
          // Run the DFS on non visited nodes only
          if(!this.visitedNodes.has(node)) {
            
            // Calls the DFS with key as starting node 
            if(this.DFSHelper(node) == true) {
              return true;
            }
            
          }
        }
        
        return false;
      }
      
      DFSHelper(startingNode) {
        
        // add the startingNode node in visited array 
        this.visitedNodes.add(startingNode);
            
        this.visitedPath.add(startingNode);
        
        console.log("Node - " + startingNode + ", ");
        
        let adjencyNodes = this.adjacencyList.get(startingNode);
        
        // iterate over all the adjency nodes of the starting nodes
        for(let adjencyNode of adjencyNodes) {
          // if node is not visited
          if(!this.visitedNodes.has(adjencyNode)) {
            // use recursion to reach at the depth of the graph
            let isCyleInRecurssion = this.DFSHelper(adjencyNode);
            // check if any nested recursion has cycle break the loop by returning true
            if (isCyleInRecurssion == true) {
              return true;
            };
            
          }
          // Check if the visited node is present in the visitedPath i.e. current path
          else if (this.visitedPath.has(adjencyNode)) {
            return true;
          }
        }
        
        // return false if no cycles found, remove it from visitedPath
        this.visitedPath.delete(startingNode);
        return false;
      }
    }
    
    let graph = new Graph();
    
        graph.addVertex(0);
        graph.addVertex(1);
        graph.addVertex(2);
        graph.addVertex(3);
        graph.addVertex(4);
        
        graph.addVertex(5);
        graph.addVertex(6);
        
        graph.addVertex(7);
        graph.addVertex(8);
        graph.addVertex(9);
        
        graph.addEdges(0,1);
        graph.addEdges(1,2);
        graph.addEdges(2,3);
        graph.addEdges(3,4);
        
        graph.addEdges(5,6);
        
        graph.addEdges(7,8);
        graph.addEdges(8,9);
        graph.addEdges(9,7);
    
    console.log('**** DFS *****')
    let isCycleDfs = graph.performDFSOnComponentGraph();
    console.log("Graph contains cycles (DFS) -", (isCycleDfs ? 'Yes': 'No'));
     ```
     </p>
  </details>

  ---

9. <details>
    <summary>
        <b>
            Perform a BFS Traversal on a Matrix using Graph approach?
        </b>
    </summary>
     <p>
       
    ```javascript
        class Graph {
          constructor(matrix) {
            // get the matrix
            this.matrix = matrix;
            this.rows = matrix.length;
            this.cols = matrix[0].length;
            // define the same size matrix for visited entries
            this.visited = new Array(this.rows).fill(false).
                          map(() => new Array(this.cols).fill(false));
          }  
          
          isValidCell(row, col) {
            // lower and upper bound for neighbour's
            return row >= 0 && row < this.rows && col >= 0 && col < this.cols;
          }
          
          getAdjacentCells(row, col) {
            // create an array fro adjacent cells
            const adjacentCells = [];
            
            // iterate over all possible 8 direction of a cell
            for(let deltaRow = -1; deltaRow <= 1; deltaRow++) {
              for(let deltaCol = -1; deltaCol <=1; deltaCol++) {
                const neighbourRow = row + deltaRow;
                const neighbourCol = col + deltaCol;
                
                // validate if its a valid node, it is not visited, 
                if(this.isValidCell(neighbourRow, neighbourCol) && !this.visited[neighbourRow][neighbourCol]) {
                  // push the cell to the adjacent cells array
                  adjacentCells.push([neighbourRow, neighbourCol])
                }
              }
            }
            
            // return the adjacent cell array
            return adjacentCells;
          }
                  
          // BFS 
          breathSearchFirstTraversal(startingRow, startingCol) {
            // create a queue to process the cells
            this.queue = [];
            
            // push the cell to queue and mark it as visited in visited matrix
            this.queue.push([startingRow, startingCol]);
            this.visited[startingRow][startingCol] = true;
            
            while(this.queue.length > 0) {
              // get the first element from queue
              let [row, col]  = this.queue.shift();
              
              console.log(`Visiting cell: [${row}, ${col}]`);
              
              // get the adjacent cells for this cell i.e. the filtered one
              const adjacentCells = this.getAdjacentCells(row, col);
              
              // push the cell to queue and mark them as visited
              for(let [adjRow, adjCol] of adjacentCells) 
              {
                this.visited[adjRow][adjCol] = true;
                this.queue.push([adjRow, adjCol]);
              }
            }
          }
        }
        
        const matrix = [
          [0, 1, 0],
          [1, 0, 1],
          [1, 1, 0],
          [0, 1, 1]
        ];
        
        let graph = new Graph(matrix);
        console.log('**** BFS *****')
        graph.breathSearchFirstTraversal(0,0);
     ```
     </p>
  </details>

  ---

10. <details>
    <summary>
        <b>
            Perform a DFS Traversal on a Matrix using Graph approach?
        </b>
    </summary>
     <p>
       
    ```javascript
    class Graph {
      constructor(matrix) {
        this.matrix = matrix;
        this.row = matrix.length;
        this.col = matrix[0].length;
        this.visitedNodes = new Array(this.row).fill().map(() => new Array(this.col).fill(false));
      }
      
      validCells(row, col) {
        return row >=0 && col >= 0 && row < this.row && col < this.col;
      }
      
      getAdjacencyCells(row, col) {
        const directions = [
          [-1, 0], // Up
          [1, 0],  // Down
          [0, -1], // Left
          [0, 1]   // Right
        ];
        
        const adjacencyCells = [];
        
        for(let [dr, dc] of directions) {
            const newRow = row + dr;
            const newCol = col + dc;
            
            if(this.validCells(newRow, newCol)) {
              adjacencyCells.push([newRow, newCol]);
            }
        }
        
        return adjacencyCells;
      }
      
      dfsTraversal(startingRow, startingCol) {
        this.dfsTraversalHelper(startingRow, startingCol);
      }
      
      dfsTraversalHelper(startingRow, startingCol) {
        this.visitedNodes[startingRow][startingCol] = true;
        
        console.log(`Visiting cell: [${startingRow}, ${startingCol}]`);
        
        for(const [adjR, adjC] of this.getAdjacencyCells(startingRow, startingCol)) {
          if(!this.visitedNodes[adjR][adjC]) {
            this.dfsTraversalHelper(adjR, adjC);
          }
        }
      }
    }
    
    const matrix = [
      [0, 1, 0],
      [1, 0, 1],
      [1, 1, 0],
      [0, 1, 1]
    ];
        
    let graph = new Graph(matrix);
    console.log('**** DFS *****')
    graph.dfsTraversal(0,0);
     ```
     </p>
  </details>


  ---

11. <details>
    <summary>
        <b>
            Check if the given undirected graph is Bipartite?
        </b>
    </summary>
     <p>
       
    ```javascript
     class Graph {
    
      constructor() {
        this.adjacencyList = new Map();
      }  
    
      addVertex(node) {
        this.adjacencyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjacencyList.get(node1).push(node2);
        this.adjacencyList.get(node2).push(node1);
      }
    
      getEdges(node) {
        return this.adjacencyList.get(node);
      }
      
      // BFS 
      isBipartiteBFS(startingNode) {
        // Fill all the visited nodes with default color -1
        this.visitedNodes = new Array(this.adjacencyList.size).fill(-1);
        
        this.queue = [];
        
        // set color of starting node as false
        this.visitedNodes[startingNode] = 0;
        
        this.queue.push(startingNode);
        
        while(this.queue.length != 0) {
          // get the first element from queue
          let currentNode  = this.queue.shift();
          let adjencyNodes = this.adjacencyList.get(currentNode);
    
          for(let adjencyNode of adjencyNodes) 
          {
            // if color of node is not set
            if(this.visitedNodes[adjencyNode] == -1) {
                // invert the color of the node from its adjacent
                this.visitedNodes[adjencyNode] = 1 - this.visitedNodes[currentNode];
                // push into queue to be scaned further
                this.queue.push(adjencyNode);
            }
            // If the color of current node and adjency node is same means not bipartite
            else if (this.visitedNodes[adjencyNode] == this.visitedNodes[currentNode]) {
                return false;
            }
          }
        }
        
        // if no conditions meets return true
        return true;
      }
      
      // DFS 
      isBipartiteDFS(startingNode) {
        // Fill all the visited nodes with default color -1
        this.visitedNodes = new Array(this.adjacencyList.size).fill(-1);
        
        // call the dfs method with starting color value
        return this.DFSHelper(startingNode, 0);
      }
      
      // DFS Algo
      DFSHelper(startingNode, color) {
        // set color of starting node to the color value
        this.visitedNodes[startingNode] = color;
        
        let adjencyNodes = this.adjacencyList.get(startingNode);
    
        // iterate over all the adjency nodes of the starting nodes
        for(let adjencyNode of adjencyNodes) {
          // if node is not visited
          if(this.visitedNodes[adjencyNode] == -1) {
            // call the dfs helper for this node with inverted color value
            // return false if any recursion stack returns false
             if (this.DFSHelper(adjencyNode, 1 - color) == false) {
               return false;
             };
          }
          // Check if the visited node have same color as of its adjacent
          else if (this.visitedNodes[adjencyNode] == color) {
            return false;
          }
          
        }
        
        // if no conditions meets return true
        return true;
      }
    }
    
    let graph = new Graph();
    
    graph.addVertex(0);
    graph.addVertex(1);
    graph.addVertex(2);
    graph.addVertex(3);
    graph.addVertex(4);
    graph.addVertex(5);
    
    graph.addEdges(0,1); 
    graph.addEdges(1,2);
    graph.addEdges(2,3);
    graph.addEdges(3,4);
    graph.addEdges(4,5);
    graph.addEdges(5,1);
    
    console.log('**** BFS *****')
    let isBipartiteBfs = graph.isBipartiteBFS(0);
    console.log("Is Graph Bipartite -", (isBipartiteBfs ? 'Yes': 'No'));
    
    console.log('**** DFS *****')
    let isBipartiteDfs = graph.isBipartiteDFS(0);
    console.log("Is Graph Bipartite -", (isBipartiteDfs ? 'Yes': 'No'));
     ```
     </p>
  </details>

  ---

12. <details>
    <summary>
        <b>
            Perform Topological Sorting on DAG? [ DFS ]
        </b>
    </summary>
     <p>
       
    ```javascript
    class Graph {
      constructor() {
        this.adjacencyList = new Map();
      }
    
      addVertex(vertex) {
        this.adjacencyList.set(vertex, []);
      }
    
      addEdge(source, destination) {
        this.adjacencyList.get(source).push(destination);
      }
    
      topologicalSort() {
        const visited = new Set();
        const stack = [];
    
        for (let vertex of this.adjacencyList.keys()) {
          if (!visited.has(vertex)) {
            this.dfs(vertex, visited, stack);
          }
        }
    
        return stack.reverse();
      }
    
      dfs(vertex, visited, stack) {
        visited.add(vertex);
    
        const neighbors = this.adjacencyList.get(vertex);
    
        for (let neighbor of neighbors) {
          if (!visited.has(neighbor)) {
            this.dfs(neighbor, visited, stack);
          }
        }
    
        stack.push(vertex);
      }
    }
    
    const graph = new Graph();
    
    graph.addVertex('A');
    graph.addVertex('B');
    graph.addVertex('C');
    graph.addVertex('D');
    graph.addVertex('E');
    graph.addVertex('F');
    
    graph.addEdge('A', 'D');
    graph.addEdge('F', 'B');
    graph.addEdge('B', 'D');
    graph.addEdge('F', 'A');
    graph.addEdge('D', 'C');
    
    const topologicalOrder = graph.topologicalSort();
    console.log('Topological Order:', topologicalOrder);

     ```
     </p>
  </details>


  ---

13. <details>
    <summary>
        <b>
            Perform Topological Sorting on DAG? [ BFS - Kahn's Algorithm ]
        </b>
    </summary>
     <p>
       
    ```javascript
    class Graph {
      constructor() {
        this.adjacencyList = new Map();
      }
    
      addVertex(vertex) {
        this.adjacencyList.set(vertex, []);
      }
    
      addEdge(source, destination) {
        this.adjacencyList.get(source).push(destination);
      }
    
      topologicalSort() {
        // Create a Map to store Indgree values
        const inDegree = new Map();
        
        // Initially set all inDegree as 0
        for(let key of this.adjacencyList.keys()) {
          inDegree.set(key, 0);
        }
        
        // Calculate the inDegree for each node by iterating over the array of each node
        for(let neighbors of this.adjacencyList.values()) {
          for(let neighbor of neighbors) {
            inDegree.set(neighbor, inDegree.get(neighbor) + 1);
          }
        }
        
        let queue = [];
        let result = [];
    
        // push the nodes in the queue whoses inDegree is 0
        for(let [node, degree] of inDegree.entries()) {
          if(degree == 0) {
            queue.push(node);
          }
        }
        
        while (queue.length > 0) {
          // get the first node
          const vertex = queue.shift();
          // push it into the result
          result.push(vertex);
          
          const adjencyNodes = this.adjacencyList.get(vertex);
          
          // iterate over adjacency nodes
          for(let adjencyNode of adjencyNodes) {
            // reduce the inDegree for each adjacency nodes
            inDegree.set(adjencyNode, inDegree.get(adjencyNode) - 1);
            
            // push into the queue if the inDegree is 0
            if(inDegree.get(adjencyNode) == 0) {
              queue.push(adjencyNode);
            }
          }
        }
        
        // return the result array
        return result;
      }
    }
    
    const graph = new Graph();
    
    graph.addVertex('A');
    graph.addVertex('B');
    graph.addVertex('C');
    graph.addVertex('D');
    graph.addVertex('E');
    graph.addVertex('F');
    
    graph.addEdge('A', 'D');
    graph.addEdge('F', 'B');
    graph.addEdge('B', 'D');
    graph.addEdge('F', 'A');
    graph.addEdge('D', 'C');
    
    const topologicalOrder = graph.topologicalSort();
    console.log('Topological Order:', topologicalOrder);
     ```
     </p>
  </details>


  ---

14. <details>
    <summary>
        <b>
            Perform Dijkastra's Algo to find out Shortest Path to all nodes.[ Using Priority Queue ]
        </b>
    </summary>
     <p>
       
    ```javascript
    class PriorityQueue {
      constructor() {
        this.queue = [];
      }
    
      enqueue(node, distance) {
        this.queue.push({ node, distance });
        this.queue.sort((a, b) => a.distance - b.distance);
      }
    
      dequeue() {
        return this.queue.shift();
      }
    
      isEmpty() {
        return this.queue.length === 0;
      }
    }
    
    class Graph {
      constructor() {
        this.adjacencyList = new Map();
      }
    
      addVertex(vertex) {
        this.adjacencyList.set(vertex, new Map());
      }
    
      addEdge(source, destination, weight) {
        this.adjacencyList.get(source).set(destination, weight);
        this.adjacencyList.get(destination).set(source, weight);
      }
    
      dijkstra(start) {
        const distances = new Map();
        const queue = new PriorityQueue();
    
        // set the distance as Infinity for all other nodes
        for (let vertex of this.adjacencyList.keys()) {
          if (vertex === start) {
            distances.set(vertex, 0);
            // push the start node in queue
            queue.enqueue(vertex, 0);
          } else {
            distances.set(vertex, Infinity);
            queue.enqueue(vertex, Infinity);
          }
        }
        
        let iterationCount = 0;
    
        while (!queue.isEmpty()) {
          iterationCount++;
          const { node: current } = queue.dequeue();
    
          // get the adjacency nodes
          for (let [neighbor, weight] of this.adjacencyList.get(current).entries()) {
            const totalDistance = distances.get(current) + weight;
    
            if (totalDistance < distances.get(neighbor)) {
              // update the distance array with new distance value
              distances.set(neighbor, totalDistance);
              // push into the queue
              queue.enqueue(neighbor, totalDistance);
            }
          }
        }
        
        console.log('Number of iterations:', iterationCount);
    
        return distances;
      }
    }
    
    const graph = new Graph();
    
    graph.addVertex('A');
    graph.addVertex('B');
    graph.addVertex('C');
    graph.addVertex('D');
    graph.addVertex('E');
    graph.addVertex('F');
    
    graph.addEdge('A', 'B', 4);
    graph.addEdge('A', 'C', 4);
    graph.addEdge('B', 'C', 3);
    graph.addEdge('C', 'D', 3);
    graph.addEdge('C', 'E', 1);
    graph.addEdge('C', 'F', 6);
    graph.addEdge('D', 'F', 2);
    graph.addEdge('E', 'F', 3);
    
    const distances = graph.dijkstra('A');
    console.log('Shortest distances:', distances);
     ```
     </p>
  </details>


  ---

15. <details>
    <summary>
        <b>
            Perform Dijkastra's Algo to find out Shortest Path to all nodes.[ Using Set ]
        </b>
    </summary>
     <p>
       
    ```javascript
    class Graph {
      constructor() {
        this.adjacencyList = new Map();
        this.nodeRefs = new Map();
      }
    
      addVertex(vertex) {
        this.adjacencyList.set(vertex, new Map());
      }
    
      addEdge(source, destination, weight) {
        this.adjacencyList.get(source).set(destination, weight);
        this.adjacencyList.get(destination).set(source, weight);
      }
    
      dijkstra(startVertex) {
        const distances = new Map();
        const unvisitedNodes = new Set();
    
        // Initialize distances with Infinity for all nodes except the start vertex
        for (let vertex of this.adjacencyList.keys()) {
          if (vertex === startVertex) {
            distances.set(vertex, 0);
            
            const nodeRef = { [vertex]: 0 };
            unvisitedNodes.add(nodeRef);
            
            this.nodeRefs.set(vertex, nodeRef);
          } else {
            distances.set(vertex, Infinity);
            
            const nodeRef = { [vertex]: Infinity };
            unvisitedNodes.add(nodeRef);
            
            this.nodeRefs.set(vertex, nodeRef);
          }
        }
    
        let iterationCount = 0;
    
        while (unvisitedNodes.size > 0) {
          iterationCount++;
    
          // get the first item from set
          const [currentNodeRef] = unvisitedNodes;
          // delete this from set
          unvisitedNodes.delete(currentNodeRef);
          // get the key value i.e. vertex
          const currentVertex = Object.keys(currentNodeRef)[0];
    
          // Visit the neighbors of the current vertex
          for (let [neighbor, weight] of this.adjacencyList.get(currentVertex).entries()) {
            const totalDistance = distances.get(currentVertex) + weight;
    
            if (totalDistance < distances.get(neighbor)) {
              const neighborRef = this.nodeRefs.get(neighbor);
    
              // check if the neighbor has Infinity value or not
              // if not having means someone visit this already with
              // higher distance value
              // remove it from set
              // this will also help in reducing the number of iterations
              if (distances.get(neighbor) !== Infinity) {
                unvisitedNodes.delete(neighborRef);
              }
    
              distances.set(neighbor, totalDistance);
              
              const newNeighborRef = { [neighbor]: totalDistance };
              
              unvisitedNodes.add(newNeighborRef);
              
              this.nodeRefs.set(neighbor, newNeighborRef);
            }
          }
        }
        
        console.log('Number of iterations:', iterationCount);
    
        return distances;
      }
    }
    
    const graph = new Graph();
    
    graph.addVertex('A');
    graph.addVertex('B');
    graph.addVertex('C');
    graph.addVertex('D');
    graph.addVertex('E');
    graph.addVertex('F');
    
    graph.addEdge('A', 'B', 4);
    graph.addEdge('A', 'C', 4);
    graph.addEdge('B', 'C', 3);
    graph.addEdge('C', 'D', 3);
    graph.addEdge('C', 'E', 1);
    graph.addEdge('C', 'F', 6);
    graph.addEdge('D', 'F', 2);
    graph.addEdge('E', 'F', 3);
    
    const distances = graph.dijkstra('A');
    console.log('Shortest distances:', distances);
     ```
     </p>
  </details>


  ---

16. <details>
    <summary>
        <b>
        </b>
    </summary>
     <p>
       
    ```javascript
     ```
     </p>
  </details>


  ---

17. <details>
    <summary>
        <b>
        </b>
    </summary>
     <p>
       
    ```javascript
     ```
     </p>
  </details>


  ---

18. <details>
    <summary>
        <b>
        </b>
    </summary>
     <p>
       
    ```javascript
     ```
     </p>
  </details>


  ---

5. <details>
    <summary>
        <b>
        </b>
    </summary>
     <p>
       
    ```javascript
     ```
     </p>
  </details>

---

5. <details>
    <summary>
        <b>
        </b>
    </summary>
     <p>
       
    ```javascript
     ```
     </p>
  </details>





