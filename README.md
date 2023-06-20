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
              
              // BSF 
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
        
        console.log('**** BSF *****')
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
          
          // DSF 
          depthSearchFirstTraversal(startingNode) {
            // create an array for visited nodes
            let visitedNodes = new Set();
            // call the dfs method
            this.dsfHelper(startingNode, visitedNodes);
          }
          
          dsfHelper(startingNode, visitedNodes) {
              
            // add the startingNode node in visited array 
            visitedNodes.add(startingNode);
            
            console.log("Node - " + startingNode + ", ");
            
            let adjencyNodes = this.adjenacyList.get(startingNode);
            
            // iterate over all the adjency nodes of the starting nodes
            for(let adjencyNode of adjencyNodes) {
              
              // if node is not visited
              if(!visitedNodes.has(adjencyNode)) {
                // use recursion to reach at the depth of the graph
                this.dsfHelper(adjencyNode, visitedNodes);
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
        
        console.log('**** DSF *****')
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
      
      // BSF 
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
      
      // DSF 
      depthSearchFirstTraversal(startingNode) {
        // create an array for visited nodes
        let visitedNodes = new Set();
        // call the dfs method
        this.dsfHelper({startingNode: startingNode, level: 0}, visitedNodes);
      }
      
      dsfHelper(nodeObj, visitedNodes) {
        
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
            this.dsfHelper({startingNode: adjencyNode, level: level+1}, visitedNodes);
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
    
    console.log('**** BSF *****')
    graph.breathSearchFirstTraversal(0);
    
    console.log('**** DSF *****')
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
      
      // BSF on Components Graph
      performBSFOnComponentGraph() {
        // Create a visited nodes array
        this.visitedNodes = new Set();
        
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        for(const node of this.adjenacyList.keys()) {
          // Run the BSF on non visited nodes only
          if(!this.visitedNodes.has(node)) {
            // Calls the BSF with key as starting node 
            this.breathSearchFirstTraversal(node);
          }
        }
      }
      
      // DSF on Components Graph
      performDSFOnComponentGraph() {
        // Create a visited nodes array
        this.visitedNodes = new Set();
        
        // Run loop on every keys in map i.e. every node to track unreachable nodes
        for(const node of this.adjenacyList.keys()) {
          // Run the DSF on non visited nodes only
          if(!this.visitedNodes.has(node)) {
            // Calls the DSF with key as starting node 
            this.dsfHelper({startingNode: node, level: 0});
          }
        }
      }
    
      dsfHelper(nodeObj) {
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
            this.dsfHelper({startingNode: adjencyNode, level: level+1}, this.visitedNodes);
          }
        }
      }
      
    // BSF 
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
    
        console.log('**** BSF *****')
        graph.performBSFOnComponentGraph();
        
        console.log('**** DSF *****')
        graph.performDSFOnComponentGraph();
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
      
      // BSF 
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
      
      // DSF 
      depthSearchFirstTraversal(startingNode) {
        // create an array for visited nodes
        let visitedNodes = new Set();
        // call the dfs method
        return this.dsfHelper({ startingNode: startingNode, parentNode: -1 }, visitedNodes);
      }
      
      dsfHelper(nodeObj, visitedNodes) {
        
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
            let isCyleInRecurssion = this.dsfHelper({ startingNode: adjencyNode, parentNode: startingNode }, visitedNodes);
            
            
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
    
    console.log('**** DSF *****')
    let isCycleDfs = graph.depthSearchFirstTraversal(0);
    console.log("Graph contains cycles (DFS) -", (isCycleDfs ? 'Yes': 'No'));
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





