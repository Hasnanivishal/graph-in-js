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
        this.adjenacyList = new Map();
      }  

      addVertex(node) {
        this.adjenacyList.set(node, []);
      }

      addEdges(node1, node2){
        this.adjenacyList.get(node1).push(node2);
        this.adjenacyList.get(node2).push(node1);
      }

      getEdges(node) {
        return this.adjenacyList.get(node);
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
                this.adjenacyList = new Map();
              }  
            
              addVertex(node) {
                this.adjenacyList.set(node, []);
              }
            
              addEdges(node1, node2){
                this.adjenacyList.get(node1).push(node2);
                this.adjenacyList.get(node2).push(node1);
              }
            
              getEdges(node) {
                return this.adjenacyList.get(node);
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
                  let adjencyNodes = this.adjenacyList.get(currentNode);
                  
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
            this.adjenacyList = new Map();
          }  
        
          addVertex(node) {
            this.adjenacyList.set(node, []);
          }
        
          addEdges(node1, node2){
            this.adjenacyList.get(node1).push(node2);
            this.adjenacyList.get(node2).push(node1);
          }
        
          getEdges(node) {
            return this.adjenacyList.get(node);
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
            
            let adjencyNodes = this.adjenacyList.get(startingNode);
            
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
        this.adjenacyList = new Map();
      }  
    
      addVertex(node) {
        this.adjenacyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjenacyList.get(node1).push(node2);
        this.adjenacyList.get(node2).push(node1);
      }
    
      getEdges(node) {
        return this.adjenacyList.get(node);
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
          let adjencyNodes = this.adjenacyList.get(currentNode);
          
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
        
        let adjencyNodes = this.adjenacyList.get(startingNode);
        
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
        this.adjenacyList = new Map();
      }  
    
      addVertex(node) {
        this.adjenacyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjenacyList.get(node1).push(node2);
        this.adjenacyList.get(node2).push(node1);
      }
    
      getEdges(node) {
        return this.adjenacyList.get(node);
      }
      
      // BFS on Components Graph
      performBFSOnComponentGraph() {
        // Create a visited nodes array
        this.visitedNodes = new Set();
        
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        for(const node of this.adjenacyList.keys()) {
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
        for(const node of this.adjenacyList.keys()) {
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
        
        let adjencyNodes = this.adjenacyList.get(startingNode);
        
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
          let adjencyNodes = this.adjenacyList.get(currentNode);
          
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
        this.adjenacyList = new Map();
      }  
    
      addVertex(node) {
        this.adjenacyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjenacyList.get(node1).push(node2);
        this.adjenacyList.get(node2).push(node1);
      }
    
      getEdges(node) {
        return this.adjenacyList.get(node);
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
          let adjencyNodes = this.adjenacyList.get(currentNode);
          
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
        
        let adjencyNodes = this.adjenacyList.get(startingNode);
        
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
        this.adjenacyList = new Map();
      }  
    
      addVertex(node) {
        this.adjenacyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjenacyList.get(node1).push(node2);
        this.adjenacyList.get(node2).push(node1);
      }
    
      getEdges(node) {
        return this.adjenacyList.get(node);
      }
      
      // BFS on Components Graph
      performBFSOnComponentGraph() {
        // Create a visited nodes array
        this.visitedNodes = new Set();
        
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        for(const node of this.adjenacyList.keys()) {
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
          let adjencyNodes = this.adjenacyList.get(currentNode);
          
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
        for(const node of this.adjenacyList.keys()) {
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
        
        let adjencyNodes = this.adjenacyList.get(startingNode);
        
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
        this.adjenacyList = new Map();
      }  
    
      addVertex(node) {
        this.adjenacyList.set(node, []);
      }
    
      addEdges(node1, node2){
        this.adjenacyList.get(node1).push(node2);
      }
    
      getEdges(node) {
        return this.adjenacyList.get(node);
      }
    
      // Only DFS as BFS will not work on directed graph to detect cycles
      performDFSOnComponentGraph() {
          
        // Create a visited nodes array
        this.visitedNodes = new Set();
        
        // create an array for keeping information about the current path    
        this.visitedPath = new Set();
        
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        for(const node of this.adjenacyList.keys()) {
          
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
        
        let adjencyNodes = this.adjenacyList.get(startingNode);
        
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
            Perform a BFS Traversal on a Matrix using Graph approach
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
            Perform a DFS Traversal on a Matrix using Graph approach
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





