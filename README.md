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
        <b>Perform Breadth First Search(BSF) Traversal?
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
          
          dsfHelper(nodeObj, visitedNodes) {
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

4. <details>
    <summary>
        <b>Determine the level of each node using BFS Or DFS?
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







