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
            Perform Dijkastra's Algo to find out the Shortest Distance to all nodes And Shortest Path b/w two node?[ Using Priority Queue ]
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
        const previous = new Map();
        const queue = new PriorityQueue();
    
        for (let vertex of this.adjacencyList.keys()) {
          if (vertex === start) {
            distances.set(vertex, 0);
            queue.enqueue(vertex, 0);
          } else {
            distances.set(vertex, Infinity);
            queue.enqueue(vertex, Infinity);
          }
          previous.set(vertex, vertex);
        }

        let iterationCount = 0;
    
        while (!queue.isEmpty()) {
          iterationCount++;
    
          const { node: current } = queue.dequeue();
    
          for (let [neighbor, weight] of this.adjacencyList.get(current).entries()) {
            const totalDistance = distances.get(current) + weight;
    
            if (totalDistance < distances.get(neighbor)) {
              distances.set(neighbor, totalDistance);
              previous.set(neighbor, current);
              queue.enqueue(neighbor, totalDistance);
            }
          }
        }
          
        console.log('Number of iterations:', iterationCount);
          
        return { distances, previous };
      }
    
      getPath(start, end) {
        // get the previousNodes map from dijkstra algo
        const { distances, previous } = this.dijkstra(start);
        
        console.log(previous)
        
        // push the end node in the path array
        const path = [end];
        
        // set the end node as current for backtracking
        let current = end;
    
        // run the loop until we reach to the start node
        while (current !== start) {
          const previousNode = previous.get(current);
    
          // put the previousNode value in array
          path.unshift(previousNode);
          
          // make it as current node 
          current = previousNode;
        }
    
        return path;
      }
    }
    
    // Example usage:
    
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
    
    const { distances, previous } = graph.dijkstra('A');
    
    console.log('Shortest distances:', distances);
    console.log('Shortest path from A to E:', graph.getPath('A', 'F'));

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
            Determine the shortest distance between 2 nodes in a Unit Matrix using Dijkastra's Algo?
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
      constructor(matrix) {
        this.matrix = matrix;
        this.row = matrix.length;
        this.col = matrix[0].length;
        this.distances = new Array(this.row).fill().map(() => new Array(this.col).fill(Infinity));
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
      
      dijkstra(src, des) {
        const queue = new PriorityQueue();
        let [ i, j ] = src;
        let [desRow, desCol] = des;
        
        this.distances[i][j] = 0;
        
        queue.enqueue({i,j}, 0);
        
        while (!queue.isEmpty()) {
    
          const { node: current, distance: d } = queue.dequeue();
          
          for (let [row, col] of this.getAdjacencyCells(current.i, current.j)) {
            
            if (d + 1 < this.distances[row][col]) {
              this.distances[row][col] = d + 1;
              
              if(row == desRow && col == desCol) 
              {
                console.log(`distanse from [${i},${j}] to [${desRow},${desCol}] is ${d+1}`);
              }
                
              queue.enqueue({i: row, j: col}, d + 1);
            }
          }
        }
          
        console.log(this.distances) 
      }
    }
    
    const matrix = [
      [0, 1, 0],
      [1, 0, 1],
      [1, 1, 0],
      [0, 1, 1]
    ];
        
    let graph = new Graph(matrix);
    graph.dijkstra([0,0], [3,2]);
     ```
     </p>
  </details>


  ---

17. <details>
    <summary>
        <b>
            Determine the Cheapest Flights wit K stops using Dijkastra's Algo?
        </b>
    </summary>
     <p>
       
    ```javascript
    class PriorityQueue {
      constructor() {
        this.queue = [];
      }
    
      enqueue(steps, node, distance) {
        this.queue.push({ steps, node, distance });
        this.queue.sort((a, b) => a.steps - b.steps);
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
      }
    
      dijkstra(start, end, steps) {
        const distances = new Map();
        const previous = new Map();
        const queue = new PriorityQueue();
    
        for (let vertex of this.adjacencyList.keys()) {
          if (vertex === start) {
            distances.set(vertex, 0);
            queue.enqueue(0, vertex, 0);
          } else {
            distances.set(vertex, Infinity);
            queue.enqueue(Infinity, vertex, Infinity);
          }
          previous.set(vertex, vertex);
        }
    
        while (!queue.isEmpty()) {
          const { steps: k, node: current, distance: d } = queue.dequeue();
    
          if (current === end) {
            return d == Infinity ? -1 : d;
          }
    
          // Skip if we exceed the maximum number of steps
          if (k < steps) {
            for (let [neighbor, weight] of this.adjacencyList.get(current).entries()) {
              const totalDistance = distances.get(current) + weight;
    
              if (totalDistance < distances.get(neighbor) && k < steps) {
                distances.set(neighbor, totalDistance);
                previous.set(neighbor, current);
    
                queue.enqueue(k + 1, neighbor, totalDistance);
              }
            }
          }
        }
      }
    }
    
    const graph = new Graph();
    
    graph.addVertex('A');
    graph.addVertex('B');
    graph.addVertex('C');
    graph.addVertex('D');
    graph.addVertex('E');
    graph.addVertex('F');
    
    graph.addEdge('A', 'B', 5);
    graph.addEdge('A', 'D', 2);
    graph.addEdge('D', 'B', 2);
    graph.addEdge('B', 'C', 5);
    graph.addEdge('B', 'E', 1);
    graph.addEdge('E', 'C', 1);
    
    console.log('Cheapest price:', graph.dijkstra('A', 'E', 2));
     ```
     </p>
  </details>


  ---

18. <details>
    <summary>
        <b>
            Determin the Shortest Path, Distance and Negative Cycle in Directed weighted Graph using Bellman Ford Algo?
        </b>
    </summary>
     <p>
       
    ```javascript
    class Graph {
      
      constructor() {
        this.edges = [];
        this.nodes = new Set();
      }
    
      addEdge(source, destination, weight) {
        // edges
        this.edges.push({ source, destination, weight });
        
        // vertex
        this.nodes.add(source);
        this.nodes.add(destination);
      }
    
      bellmanFord(start) {
        
        // distance map
        this.distances = new Map();
        // previous map for path
        const previous = new Map();
    
        // Initialize distances with Infinity except for the start node
        for (let node of this.nodes) {
          this.distances.set(node, Infinity);
          previous.set(node, null);
        }
        
        this.distances.set(start, 0);
    
        // Relax edges repeatedly |V| - 1 times
        for (let i = 0; i < this.nodes.size - 1; i++) {
          
          // run the loop on every edge
          for (let { source, destination, weight } of this.edges) {
            // Reflax the edges
            let totalDistance = this.distances.get(source) + weight;
            if (this.distances.get(source) != Infinity && totalDistance < this.distances.get(destination)) {
              this.distances.set(destination, totalDistance);
              previous.set(destination, source);
            }
          }
        }
        
        this.flag = false;
        
        // Nth relaxation to Check for negative cycles
        for (const { source, destination, weight } of this.edges) {
          
          // If graph trying to update it in the Nth iteration means 
          // we have negative cycles
          if (this.distances.get(source) != Infinity && this.distances.get(source) + weight < this.distances.get(destination)) {
            this.flag = true; // Negative-weight cycle found
          }
        }
        
        let d = this.flag ? null : this.distances;
    
        return { distances: d, previous: previous };
      }
      
      getPath(start, end) {
        const { distances, previous } = this.bellmanFord(start);
        
        if (distances == null) {
          throw new Error('Graph contains negative-weight cycles');
        }
        
        const path = [];
        let current = end;
    
        while (current !== start) {
          path.unshift(current);
          current = previous.get(current);
        }
    
        path.unshift(start);
        return { path, distance: distances };
      }
    }
    
    const graph = new Graph();
    
    graph.addEdge('A', 'B', 2);
    graph.addEdge('A', 'C', 4);
    graph.addEdge('B', 'C', 1);
    graph.addEdge('B', 'D', 3);
    graph.addEdge('C', 'D', -6);
    
    const result = graph.getPath('A', 'D');
    
    console.log('Shortest path:', result.path);
    console.log('Shortest distance:', result.distance);
    
    console.log("***** Negative Cycle weight Example ********")
    const graph_cycle = new Graph();
    
    graph_cycle.addEdge('A', 'B', -1);
    graph_cycle.addEdge('B', 'C', -2);
    graph_cycle.addEdge('C', 'A', -3);
    
    graph_cycle.getPath('A', 'C');
     ```
     </p>
  </details>


  ---

19. <details>
    <summary>
        <b>
            Determin the Shortest Path, Distance and Negative Cycle in Directed weighted Graph using Floyd Warshall Algo?
        </b>
    </summary>
     <p>
       
    ```javascript
    class Graph {
      // adjacency matrix approach
      constructor(vertices) {
        this.vertices = vertices;
        
        // prepare a matrix
        this.adjMatrix = Array(vertices)
          .fill(null)
          .map(() => Array(vertices).fill(Infinity));
    
        // Initialize the diagonal with 0 (distance from a vertex to itself)
        for (let i = 0; i < vertices; i++) {
          this.adjMatrix[i][i] = 0;
        }
      }
    
      addEdge(source, destination, weight) {
        this.adjMatrix[source][destination] = weight;
      }
    
      floydWarshall() {
        const dist = this.adjMatrix;
    
        // Perform the Floyd-Warshall algorithm
        // run for every node
        for (let k = 0; k < this.vertices; k++) {
          // run for each row and col
          for (let i = 0; i < this.vertices; i++) {
            for (let j = 0; j < this.vertices; j++) {
              // determine the distance if [i,k] + [k,j] < [i][j]
              // if k = 1
              // [0,1] + [1,0] < [0][0]
              if (dist[i][k] + dist[k][j] < dist[i][j]) {
                dist[i][j] = dist[i][k] + dist[k][j];
              }
            }
          }
        }
        
        // to check if there is any negative weight cycles exists
        for(let i=0; i<this.adjMatrix.length; i++) {
          if(dist[i][i] < 0) {
            throw new Error('Graph contains negative-weight cycles');
          }
        }
    
        return dist;
      }
    }
    
    const graph = new Graph(4);
    
    graph.addEdge(0, 1, 3);
    graph.addEdge(0, 3, 7);
    graph.addEdge(1, 2, 2);
    graph.addEdge(2, 0, 1);
    graph.addEdge(2, 3, 5);
    graph.addEdge(3, 2, 4);
    
    const distances = graph.floydWarshall();
    
    console.log('All-pairs shortest distances:');
    for (let i = 0; i < graph.vertices; i++) {
      for (let j = 0; j < graph.vertices; j++) {
        console.log(`From ${i} to ${j}: ${distances[i][j]}`);
      }
    }
    
    console.log("***** Negative Cycle weight Example ********")
    
    const graph_cycle = new Graph(4);
    
    graph_cycle.addEdge(0, 1, 1);
    graph_cycle.addEdge(1, 2, 3);
    graph_cycle.addEdge(2, 3, 2);
    graph_cycle.addEdge(3, 1, -6);
    
    graph_cycle.floydWarshall();
     ```
     </p>
  </details>

---

20. <details>
    <summary>
        <b>
            Determine the MST and MST weight using Prim's Algo?
        </b>
    </summary>
     <p>
       
    ```javascript
    class PriorityQueue {
      constructor() {
        this.queue = [];
      }
    
      enqueue(distance, node, parent) {
        this.queue.push({ distance, node, parent });
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
    
      primsMST(start) {
        // initalize a visited array
        const visited = new Map();
        
        // Stores the weight, node, parent 
        const queue = new PriorityQueue();
        
        // Stoes the edges of MST
        let mstList = [];
        
        // Sum of MST weight
        let mstSum = 0;
    
        // Mark all of the nodes as non visited
        for (let vertex of this.adjacencyList.keys()) {
          if (vertex === start) {
            visited.set(vertex, 1);
            
            // Starting node will have weight as 0 and parent as -1
            queue.enqueue(0, vertex, -1);
            
          } else {
            visited.set(vertex, 0);
          }
        }
        
        while (!queue.isEmpty()) {
          const { distance: weight , node: current, parent } = queue.dequeue();
          
          // If parent is not -1 and node is not visited
          if(parent !== -1 && !visited.get(current)) {
            // put the edge into MST list
            mstList.push({edge1: parent, edge2: current});
            // increase the sum with node weight
            mstSum+=weight;
          }
          
          // set the node as visited
          visited.set(current, 1);
          
          for (let [neighbor, weight] of this.adjacencyList.get(current).entries()) {
            // Push the non visited neighbors in the priority queue
            if(!visited.get(neighbor)) {
              queue.enqueue(weight, neighbor, current);
            }
          }
        }
        
        return { mstList, mstSum };
      }
    }
    
    const graph = new Graph();
    
    graph.addVertex('A');
    graph.addVertex('B');
    graph.addVertex('C');
    graph.addVertex('D');
    graph.addVertex('E');
    
    graph.addEdge('A', 'B', 2);
    graph.addEdge('A', 'C', 1);
    graph.addEdge('B', 'C', 1);
    graph.addEdge('B', 'D', 2);
    graph.addEdge('B', 'E', 2);
    graph.addEdge('D', 'E', 1);
    
    const { mstList, mstSum } = graph.primsMST('A');
    
    console.log('Minimum Spanning tree Edges', mstList);
    console.log('Minimum Spanning tree Weight', mstSum);

     ```
     </p>
  </details>

  ---

21. <details>
    <summary>
        <b>
            Check if given two nodes belongs to same component using Disjoin Set Union by Rank and Union by Set?
        </b>
    </summary>
     <p>
       
    ```javascript
    class DisjointSet {
      
      constructor(n) {
        // array to keep parents
        this.parent = new Array(n);
        // array to keep rank, default 0
        this.rank = new Array(n).fill(0);
        // array to keep size, default 1
        this.size = new Array(n).fill(1);
    
        // set parent values to node itself
        for (let i = 0; i < n; i++) {
          this.parent[i] = i;
        }
      }
    
      findUltimateParent(node) {
        // if parent of the node is node itself return the node
        if (this.parent[node] == node) {
          return this.parent[node];
        }
        // keep use recursion to find the ultimate parent node
        return this.parent[node] = this.findUltimateParent(this.parent[node]);
      }
      
      // Union by Rank
      unionByRank(u, v) {
        let up_u = this.findUltimateParent(u);
        let up_v = this.findUltimateParent(v);
        
        // If parent are the same nodes are in the same component, return
        if(up_u == up_v) return;
        
        // If not then Check the rank of ultimate parents of u and v
        let rank_u = this.rank[up_u];
        let rank_v = this.rank[up_v];
        
        // if rank of ultimate parent of u is less than ultimate parent of v
        // connect from u to v    
        if(rank_u < rank_v) {
          // smaller get attached to the larger one
          this.parent[up_u] = up_v;
        } 
        else if (rank_v < rank_u) {
          this.parent[up_v] = up_u;
        } 
        // If Ranks are same connect either of them 
        // Update the Rank value of the parent edge 
        else {
          this.parent[up_u] = up_v;
          this.rank[up_v]++;
        }
      }
      
      // Union by Size 
      unionBySize(u, v) {
        let up_u = this.findUltimateParent(u);
        let up_v = this.findUltimateParent(v);
        
        // If parents are the same, nodes are in the same component
        if(up_u == up_v) return;
        
        // If not then Check the size of ultimate parents of u and v
        let size_u = this.size[up_u];
        let size_v = this.size[up_v];
        
        // if size of ultimate parent of u is less than ultimate parent of v
        // connect from u to v    
        if(size_u < size_v) {
          // smaller get attached to the larger one
          this.parent[up_u] = up_v;
          
          // increase the size of ultilmate parent of v by the size of up_u
          this.size[up_v] += size_u;
        } 
        // For all other case, connect the edges 
        else {
          this.parent[up_v] = up_u;
          this.size[up_u] += size_v;
        }
      }
    }
    
    const edges = [
      [0, 1],
      [2, 3],
      [4, 5],
      [1, 2],
    ];
    
    const n = 6; // Number of vertices in the graph
    
    const disjointSet_rank = new DisjointSet(n);
    for (const [u, v] of edges) {
      disjointSet_rank.unionByRank(u, v);
    }
    
    let connected_rank = disjointSet_rank.findUltimateParent(2) == disjointSet_rank.findUltimateParent(4)
    console.log(connected_rank);
    
    const disjointSet_size = new DisjointSet(n);
    for (const [u, v] of edges) {
      disjointSet_size.unionBySize(u, v);
    }
    
    let connected_size = disjointSet_size.findUltimateParent(2) == disjointSet_size.findUltimateParent(0)
    console.log(connected_size);
     ```
     </p>
  </details>

  ---

22. <details>
    <summary>
        <b>
            Determine the MST and MST weight using Kruskal's Algo?
        </b>
    </summary>
     <p>
       
    ```javascript
    class DisjointSet {
    
      constructor(n) {
        // array to keep parents
        this.parent = new Array(n);
        // array to keep size, default 1
        this.size = new Array(n).fill(1);
        // set parent values to node itself
        for (let i = 0; i < n; i++) {
          this.parent[i] = i;
        }
      }
    
      findUltimateParent(node) {
        // if parent of the node is node itself return the node
        if (this.parent[node] == node) {
          return this.parent[node];
        }
        // keep use recursion to find the ultimate parent node
        return this.parent[node] = this.findUltimateParent(this.parent[node]);
      }
      
      // Union by Size 
      unionBySize(u, v) {
        let up_u = this.findUltimateParent(u);
        let up_v = this.findUltimateParent(v);
        
        // If parents are the same, nodes are in the same component
        if(up_u == up_v) return;
        
        // If not then Check the size of ultimate parents of u and v
        let size_u = this.size[up_u];
        let size_v = this.size[up_v];
        
        // if size of ultimate parent of u is less than ultimate parent of v
        // connect from u to v    
        if(size_u < size_v) {
          // smaller get attached to the larger one
          this.parent[up_u] = up_v;
          
          // increase the size of ultilmate parent of v by the size of up_u
          this.size[up_v] += size_u;
        } 
        // For all other case, connect the edges 
        else {
          this.parent[up_v] = up_u;
          this.size[up_u] += size_v;
        }
      }
    }
    
    class Graph {
      constructor(numVertices) {
        this.numVertices = numVertices;
        
        // Use array to keep edges
        this.edges = [];
      }
    
      addEdge(source, destination, weight) {
        this.edges.push({ weight, source, destination });
      }
      
      kruskalMST() {
        // Stoes the edges of MST
        let mstList = [];
        
        // Sum of MST weight
        let mstSum = 0;

        // sort the array on weight
        const sortedEdges = this.edges.sort((a, b) => a.weight - b.weight);
    
        // create the instance of Disjoint Set
        const disjointSet = new DisjointSet(this.numVertices);
    
        // Run loop on the sorted edges
        for (const edge of sortedEdges) {
          
          // get the edge
          const { source, destination, weight } = edge;
          
          // if ultimate path of source and destination is not the same 
          // put this pair into the mstList
          if (disjointSet.findUltimateParent(source) !== disjointSet.findUltimateParent(destination)) {
          
            // Run union by size on source, destination edge pair
            disjointSet.unionBySize(source, destination);
            
            // put the edge into MST list
            mstList.push({edge1: source, edge2: destination});
            
            // increase the sum with node weight
            mstSum+=weight;
          }
        }
        
        return { mstList, mstSum };
      }
    }
    
    const graph = new Graph(6);
    
    graph.addEdge(0, 1, 4);
    graph.addEdge(0, 2, 1);
    graph.addEdge(1, 2, 2);
    graph.addEdge(1, 3, 5);
    graph.addEdge(2, 3, 1);
    graph.addEdge(2, 4, 3);
    graph.addEdge(3, 4, 4);
    graph.addEdge(3, 5, 3);
    graph.addEdge(4, 5, 2);
    
    const { mstList, mstSum } = graph.kruskalMST();
    
    console.log('Minimum Spanning tree Edges', mstList);
    console.log('Minimum Spanning tree Weight', mstSum);
     ```
     </p>
  </details>

  ---

23. <details>
    <summary>
        <b>
            Find Number of Strongly Connected Components in a Graph using Kosaraju's Algorithm?
        </b>
    </summary>
     <p>
       
    ```javascript
    class Graph {
      constructor() {
        this.adjacencyList = new Map();
        // list for keeping the Reverse of graph
        this.adjacencyListReverse = new Map();
      }  
    
      addVertex(node) {
        this.adjacencyList.set(node, []);
        this.adjacencyListReverse.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjacencyList.get(node1).push(node2);
      }
    
      getEdges(node) {
        return this.adjacencyList.get(node);
      }
      
      // DFS on Components Graph
      kosarajusAlgo() {
        // Create a visited nodes array
        this.visitedNodes = new Set();
        this.stack = []
        
        // Step - 1: run DFS to get finishing time stack
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        // Push into stack to know finishing time
        for(const node of this.adjacencyList.keys()) {
          // Run the DFS on non visited nodes only
          if(!this.visitedNodes.has(node)) {
            // Calls the DFS with key as starting node 
            this.DFSHelper(node);
          }
        }
        
        // console.log(this.adjacencyListReverse);
        
        // Step -2: Reverse the Graph
        // loop will run for node-first to node-last
        for(const node of this.adjacencyList.keys()) {
          // get the adjencyNodes 
          for(let adjencyNode of this.adjacencyList.get(node)) {
            // reverse the values and store in new Map
            this.adjacencyListReverse.get(adjencyNode).push(node);
          }
        }
        
        // reset the visited array for next step
        this.visitedNodes = new Set();
        
        // console.log(this.adjacencyListReverse);
        
        // Step-3: Perform DFS
        let scc_counter = 0;
        while(this.stack.length > 0) {
          let currentItem = this.stack.pop();
          // Run the DFS on non visited nodes only
          if(!this.visitedNodes.has(currentItem)) {
            scc_counter++;
            // list to store items
            const scc = []; 
            // Calls the DFS with key as starting node 
            this.DFSHelper_Transpose(currentItem, scc);
            
            // Print each SCC 
            console.log(scc);
          }
        }
        
        return scc_counter;
      }
    
      DFSHelper(startingNode) {
        // add the startingNode node in visited array 
        this.visitedNodes.add(startingNode);
        
        let adjencyNodes = this.adjacencyList.get(startingNode);
        
        // iterate over all the adjency nodes of the starting nodes
        for(let adjencyNode of adjencyNodes) {
          
          // if node is not visited
          if(!this.visitedNodes.has(adjencyNode)) {
            // use recursion to reach at the depth of the graph
            this.DFSHelper(adjencyNode);
          }
        }
        
        this.stack.push(startingNode);
      }
      
      DFSHelper_Transpose(startingNode, list) {
        // add the startingNode node in visited array 
        this.visitedNodes.add(startingNode);
        
        let adjencyNodes = this.adjacencyListReverse.get(startingNode);
        
        // iterate over all the adjency nodes of the starting nodes
        for(let adjencyNode of adjencyNodes) {
          // if node is not visited
          if(!this.visitedNodes.has(adjencyNode)) {
            // use recursion to reach at the depth of the graph
            this.DFSHelper_Transpose(adjencyNode, list);
          }
        }
        
        list.push(startingNode)
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
      
      graph.addEdges(0,1);
      graph.addEdges(1,2);
      graph.addEdges(2,0);
      graph.addEdges(2,3);
      graph.addEdges(3,4);
      graph.addEdges(4,5);
      graph.addEdges(5,6);
      graph.addEdges(6,7);
      graph.addEdges(6,4);
      
    console.log('Number of Strongly connected components:', graph.kosarajusAlgo())
     ```
     </p>
  </details>

  ---

24. <details>
    <summary>
        <b>
            Determine the Critical Connections in a network i.e. Bridges using Tarjan's Algo?
        </b>
    </summary>
     <p>
       
    ```javascript
    class Graph {
      constructor() {
        this.adjacencyList = new Map();
        
        // step counter
        this.step = 1;
      }  
    
      addVertex(node) {
        this.adjacencyList.set(node, []);
      }
    
      addEdges(node1, node2) {
        this.adjacencyList.get(node1).push(node2);
        this.adjacencyList.get(node2).push(node1);
      }
    
      getEdges(node) {
        return this.adjacencyList.get(node);
      }
      
      // Tarjan's Algo
      findBridges(startingNode) {
        // create an array for visited nodes
        const visitedNodes = new Set();
        
        // store the step number i.e. Time of Insertion
        const tin = new Array(this.adjacencyList.size).fill(0);
        
        // store the min of step number i.e. Lowset time of Insertion
        const low_tin = new Array(this.adjacencyList.size).fill(0);
        
        // stores the bridges 
        const bridges = [];
        
        // call the dfs method
        this.DFSHelper(startingNode, -1, visitedNodes, tin, low_tin, bridges);
        
        return bridges;
      }
      
      DFSHelper(startingNode, parent, visitedNodes, tin, low_tin, bridges) {
        visitedNodes.add(startingNode);
        
        // set both the tin and low_tin to step number
        tin[startingNode] = this.step;
        low_tin[startingNode] = this.step;
        
        // increase the step
        this.step++;
        
        let adjencyNodes = this.adjacencyList.get(startingNode);
        
        // iterate over all the adjency nodes of the starting nodes
        for (let adjencyNode of adjencyNodes) {
          
          // If adjencyNode is equal to the parent of startingNode then ignore 
          if (adjencyNode == parent) continue;
          
          // if node is not visited
          if (!visitedNodes.has(adjencyNode)) {
            // use recursion to reach at the depth of the graph
            this.DFSHelper(adjencyNode, startingNode, visitedNodes, tin, low_tin, bridges);
            
            // after the completion of DFS traversal
            // update Lowest time of Insertion of the starting Node
            low_tin[startingNode] = Math.min(low_tin[startingNode], low_tin[adjencyNode]);
            
            // If the Lowest time of Insertion value of a neighbor
            // is greater than the Insertion time of the current node (starting node), 
            // it means there is no back edge, indicating a bridge.
            if (low_tin[adjencyNode] > tin[startingNode]) {
              bridges.push({ edge1: adjencyNode, edge2: startingNode });
            }
          } 
          // If adjacency node is already visited, it is in the same path.
          // Thus update the lowest time of insertion only.
          else {
            low_tin[startingNode] = Math.min(low_tin[startingNode], low_tin[adjencyNode]);
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
    graph.addVertex(6);
    
    graph.addEdges(0, 1);
    graph.addEdges(1, 2);
    graph.addEdges(2, 0);
    graph.addEdges(1, 3);
    graph.addEdges(1, 4);
    graph.addEdges(1, 6);
    graph.addEdges(3, 5);
    graph.addEdges(4, 5);
    
    
    console.log("Bridges in the Graph:");
    const bridges = graph.findBridges(0);
    
    for (let bridge of bridges) {
      console.log(bridge);
    }
     ```
     </p>
  </details>

  ---

25. <details>
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

26. <details>
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

20. <details>
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

20. <details>
    <summary>
        <b>
        </b>
    </summary>
     <p>
       
    ```javascript
     ```
     </p>
  </details>





