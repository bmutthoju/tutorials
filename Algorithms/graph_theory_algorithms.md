# Graph Theory Algorithms #
## Graph Theory Introduction and Basics ##
### Graph Theory Introduction ###
### Problems in Graph Theory ###
### Depth First Search Algorithm ###
### Breadth First Search Algorithm ###
### Breadth First Search Grid Shortest Path ###

## Graph Theory and Trees ##
### Introduction to Trees ###
### Beginner Tree Algorithms ###
### Rooting a Tree ###
### Finding Tree Center(s) ###
### Identifying Isomorphic Trees ###
1. It is a question of tree equality and what that means
2. Graph Isomorphism
	1. The question of asking whether two graphs G1 and G2 are isomorphic is asking whether they are structurally the same.
	2. Even though G1 and G2 are labelled differently and may appear different they are structurally the same graph
3. Graph Isomorphism (definition)
	1. We can also define the notion of a graph isomorphism more rigorously:
	2. G1(V1, E1) and G2(V2, E2) are isomorphic if there exists a bijection phi between the sets V1 -> V2 such that:
		1. For all u, v in V1, (u, v) is in E1 <=> (phi(u), phi(v)) is in E2
	3. In simple terms, for an isomorphism to exist there needs to be a function phi which can map all the nodes/ edges in G1 to G2 and vice-versa
4. Determining if two graphs are isomorphic is not only not obvious to the human eye, but also a difficult problem for computers.
5. It is still an open question as to whether the graph isomorphism problem is NP complete. However, many polynomial time isomorphism algorithms exist for graph subclasses such as trees
6. Isomorphic Trees:
	1. Identifying Isomorphic Trees
		1. There are several very quick probabilistic (usually hash or heuristic based) algorithms for identifying isomorphic trees. These tend to be fast, but also error prone due to hash collisions in a limited integer space.
			1. Good for competitive programming or a lot of trees
		2. The method we'll be looking at today involves serializing a tree into a unique encoding. This unique encoding is simply a unique string that represents a tree, if another tree has the same encoding then they are isomorphic.
7. Identifying Isomorphic Trees
	1. We can directly serialize unrooted tree, but in practice serializing a rooted tree is typically easier code wise
	2. However, one caveat to watch out for if we're going to root our two trees T1 and T2 to check if they're isomorphic is to ensure that the same root node is selected in both trees before serializing/ encoding the trees.
		1. This can be done by finding center of a tree
8. Procedure:
	1. Find the center(s) of the original tree. We'll see how to handle the case where either tree can have more than 1 center shortly.
	2. Root the tree at the centre nodes
	3. Generate the encoding for each tree and compare the serialized trees for equality
		1. The tree encoding is simply a sequence of left '(' and right ')' brackets. However, you can also think of them as 1's and 0's (i.e a large number) if you prefer
		2. It should also be possible to reconstruct the tree solely from the encoding. This is left as an exercise to the reader...
9. The AHU (Aho, Hopcroft, Ullman) algorithm is a clever serialization technique for representing a tree as a unique string.
	1. Unlike many tree isomorphism invariants and heuristics, AHU is able to capture a complete history of a tree's degree spectrum and structure ensuring a deterministic method of checking for tree isomorphisms.
	2. Let's have a closer look...
10. Tree encoding:
	1. Start by assigning all leaf nodes Knuth tuples: '()'
	2. Process all nodes with grayed out children and combine the labels of their children nodes and wrap them in brackets.

									0
			(()())		2			1	(())	3
				6		7	4		5 (())		8
				()		()	()		9			()
							()
							
		1. Notice that the labels get **sorted** when combined, this is important (larger child label first)
	3. (((())())(()())(()))
11. Tree Encoding Summary
	1. In summary of what we did for AHU:
		1. Leaf nodes are assigned Knuth tuples '()' to begin with
		2. Every time you move up a layer the labels of the previous subtrees get sorted lexicographically and wrapped in brackets.
		3. You cannot process a node until you have processed all its children
12. Unrooted tree encoding pseudocode

		# Returns whether two trees are isomorphic.
		# Parameters tree1 and tree2 are undirected trees
		# stored as adjacency lists.
		function treesAreIsomorphic(tree1, tree2):
			tree1_centers = treeCenters(tree1)
			tree2_centers = treeCenters(tree2)
			
			tree1_rooted = rootTree(tree1, tree1_centers[0])
			tree1_encoded = encode(tree1_rooted)
			
			for center in tree2_centers:
				tree2_rooted = rootTree(tree2, center)
				tree2_encoded = encode(tree2_rooted)
				# Two trees are isomorphic if their encoded
				# canocinal forms are equal.
				if tree1_encoded == tree2_encoded:
					return True
			return False
			
13. Rooted trees are sorted recursively in TreeNode objects: (To keep tree data structure organised)

		# TreeNode object structure.
		class TreeNode:
			# Unique integer id to identify this node.
			int id;
			
			# Pointer to parent TreeNode reference. Only the
			# root node has a null parent TreeNode reference.
			TreeNode parent;
			
			# List of pointers to child TreeNodes.
			TreeNode[] children;
			
14. Unrooted tree encoding pseudocode

		function encode(node):
			if node == null:
				return "" # enables leaf nodes to have ()
				
			labels = []
			for child in node.children():
				labels.add(encode(child))
				
			# Regular lexicographic sort
			sort(labels)
			
			result = ""
			for label in labels:
				results += label
				
			return "(" + result + ")"

### Identifying Isomorphic Trees Source Code ###
1. github.com/williamfiset/algorithms
2. Source code:

```
  /* Example usage */
  
  public static void main(String[] args) {
    
  }
```

## Classic Graph Theory Algorithms ##
### Topological Sort Algorithm ###
1. What is top sort? Where is it used? How to find topological ordering?
2. Many real world situations can be modelled as a graph with directed edges where some events must occur before others
	1. School class prerequisites
	2. Program dependencies
	3. Event scheduling
	4. Assembly instructions
	5. Etc...
3. Example: Suppose you are a student at university X and you want to take class H, then you must take classes A, B, D and E as prerequisites. In this sense there is an ordering on the nodes of the graph.
	1. We can use topological sort to come up with an order in which we can take courses such that we don't take a class for which we have not satisfied the pre-requisites.
4. Example: Another canocial example where an ordering on the nodes of the graph matters is for program build dependencies. A program cannot be built unless its dependencies are first built.
5. A topological ordering is an ordering of the nodes in a directed graph where for each directed edge from node A to node B, node A appears before node B in the ordering.
6. The topological sort algorithm can find a topological ordering in O(V + E) time!
	1. In a topological ordering, all edges point to the right
7. NOTE: Topological orderings are NOT unique
8. Directed Acyclic Graphs (DAG)
	1. Not every graph can have a topological ordering. A graph which contains a **cycle** cannot have a valid ordering
9. The only type of graph which has a valid topological ordering is a Directed Acyclic Graph (DAG). These are graphs with directed edges and no cycles.
	1. How do I verify that my graph does not contain a directed cycle?
	2. Answer: One method is to use Tarjan's strongly connected component algorithm which can be used to find these cycles.
10. By definition, all rooted trees have a topological ordering since they do not contain any cycles
	1. One way to topologically sort:
		1. Pick out leaf nodes (in any order)
		2. Then their parents
		3. Repeat until no more nodes are left
11. **Topological sort algorithm (general DAG)**
	1. Pick an unvisited node
	2. Beginning with the selected node, do a Depth First Search (DFS) exploring only unvisited nodes.
	3. On the recursive callback of the DFS, add the current node to the topological ordering in reverse order

### Shortest/Longest Path on a Directed Acyclic Graph (DAG) ###
1. Directed Acyclic Graph (DAG)
	1. A DAG is a graph with directed edges and no cycles. By definition this means all trees are automatically DAGs since they do not contain cycles.
2. SSSP on DAG
	1. The Single Source Shortest Path (SSSP) problem can be solved efficiently on a DAG in O(V+E) time. This is due to the fact that the nodes can be ordered in a topological ordering via topsort and processed sequentially. (works for -ve edges, too)
		1. Relaxes each edge - updating to better value
	2. Example:
		1. DAG
		
		```
		    B -11--> E
		   /|\      / \
		  3 4 4   -4   9
		 /  |  \ /      \
		A   |   D -5->F-1->H
		 \  |  / \      /
		  6 | 8   2    2
		   \v/     \  /
		    C-11--> G
		```
		
			1. Node A to all other nodes
		2. Step 1: topological ordering
		3. Step 2: Update a node's value if it is better than the previous value
3. Longest path on DAG
	1. What about the logest path? On a general graph this problem is NP-Hard, but on a DAG this problem is solvable in O(V+E)
	2. The trick is to multiply all edge values by -1 then find the shortest path and then multiply the edge values by -1 again
4. Implementation source code: [github.com/williamfiset/algorithms](github.com/williamfiset/algorithms)
	1. `public static Integer[] dagShortestPath(Map<Integer, List<Edge>> graph, int start, int numNodes)`

### Dijkstra's Shortest Path Algorithm ###
1. What is Dijkstra's algorithm?
	1. Dijkstra's algorithm is a Single Source Shortest Path (SSSP) algorithm for graphs with non-negative edge weights
	2. Depending on how the algorithm is implemented and what data structures are used the time complexity is typically `O(E * log (V))` which is competitive against other shortest path algorithms
2. Algorithm prerequisites:
	1. One constraint for Dijkstra's algorithm is that the graph must only contain **non-negative edge weights**. This constraint is imposed to ensure that once a node has been visited its optimal distance cannot be improved
	2. This property is essentially important because it enables Dijkstra's algorithm to act in a greedy manner by always selecting the next most promising node
3. Outline
	1. The goal of this slide deck is for us to understand how to implement Dijkstra's algorithm and implement it efficiently
		1. Lazy Dijkstra's animation
		2. Lazy Dijkstra's pseudo-code
		3. Finding SP + stopping early optimization
		4. Using indexed priority queue + decreaseKey to reduce space and increase performance
		5. Eager Dijkstra's animation
		6. Eager Dijkstra's pseudo-code
		7. Heap optimization with D-ary heap
			1. Boosts performance
4. Quick Algorithm Overview
	1. Maintain a 'dist' array where the distance to every node is positive infinity. Mark the distance to the start node 's' to be 0.
	2. Maintain a PQ of key-value pairs of (node index, distance) pairs which tell you which node to visit next based on sorted min value.
	3. Insert (s, 0) into the PQ and loop while PQ is not empty pulling out the next most promising (node index, distance) pair.
	4. Iterate over all edges outwards from the current node and relax each edge appending new (node index, distance) key value pair to the PQ for every relaxation.
5. Lazy Dijkstra's
	1. dist: [inf, inf, inf, inf, inf]
		1. [0, inf, inf, inf, inf]
		2. [0, 4, inf, inf, inf]
		3. [0, 4, 2, inf, inf]
		4. [0, 3, 2, inf, inf]
		5. [0, 3, 2, 6, inf]
		6. [0, 3, 2, 4, inf]
		7. [0, 3, 2, 4, 7]
	2. PQ
		1. (0, 0) - x
		2. (1, 4) - Best distance from 0 to node 1 is: dist[0] + edge.cost = 0 + 4 = 4
			1. We have already found a better route to get to node 1 (since dist[1] has value 3) so we can ignore this entry in the PQ
				1. This is lazy implementation
					1. We lazily delete the key-value pairs
		3. (2, 1) - x
			1. Next most promising node (distance = 1)
		4. (1, 3) - Best distance from node 2 to node 1 is: dist[2] + edge.cost = 1 + 2 = 3
		5. (3, 6)
			1. We have already found a better route to get to node 3 (since dist[3] has value 4) so we can ignore this entry in the PQ
		6. (3, 4) - Best distance from node 1 to node 3 is: dist[1] + edge.cost = 3 + 1 = 4
		7. (4, 7) - Best distance from node 3 to node 4 is: dist[3] + edge.cost = 4 + 3 = 7
			1. Done
6. Pseudocode:

```
# Runs Dijkstra's algorithm and returns an array that contains
# the shortest distance to every node from the start node s.
# g - adjacency list of weighted graph
# n - the number of nodes in the graph
# s - the index of the starting node (0 <= s < n)
function dijkstra(g, n, s):
  vis = [false, false, ... , false] # size n
  prev = [null, null, ..., null] # size n
  dist = [inf, inf, ... , inf, inf] # size n
  dist[s] = 0
  pq = empty priority queue
  pq.insert((s, 0))
  while pq.size() != 0:
    index, minValue = pq.poll()
	vis[index] = true
	if dist[index] < minValue: continue # optimization
	for (edge : g[index]):
	  if vis[edge.to]: continue
	  newDist = dist[index] + edge.cost
	  if newDist < dist[edge.to]:
	    prev[edge.to] = index # prev node
	    dist[edge.to] = newDist
		pq.insert((edge.to, newDist))
  return (dist, prev)
```

	1. We can keep the edges in the minimum distance path
	2. `vis` - visited array
	3. In practice most standard libraries do not support the decrease key operation for PQs. A way to get around this is to add a new (node index, best distance) pair every time we update the distance to a node
		1. As a result, it is possible to have duplicate node indices in the PQ. This is not ideal, but inserting a new key-value pair in O(log(n)) is much faster than searching for the key in the PQ which takes O(n)
	4. A neat optimization we can do which ignores stale (index, dist) pairs in our PQ is to skip nodes where we already found a better path routing through other nodes before we got to processing this node.
7. Finding the optimal path:
	1. If you wish to not only find the optimal distance to a particular node but also what sequence of nodes were taken to get there you need to track some additional information.

```
# Finds the shortest path between two nodes.
# g - adjacency list of weighted graph
# n - the number of nodes in the graph
# s - the index of the starting node (0 <= s < n)
# e - the index of the end node (0 <= e < n)
function findShortestPath(g, n, s, e):
  dist, prev = dijkstra(g, n, s)
  path = []
  if (dist[e] == inf) return path
  for (at = e; at != null; at = prev[at])
    path.add(at)
  path.reverse()
  return path
```

8. Stopping Early
	1. Suppose you know the destination node you're trying to reach is 'e' and you start at node 's' do you still have to visit every node in the graph?
		1. Yes, in the worst case. However, it is possible to stop early once you have finished visiting the destination node.
	2. The main idea for stopping early is that Dijkstra's algorithm processes each next most promising node in order. So if the destination node has been visited, its shortest distance will not change as more future nodes are visited.
	
```
function dijkstra(g, n, s, e):
  ...
    if index == e:
      return dist[e]
  return inf
```

8. Eager Dijkstra's using an Indexed Priority Queue
	1. Our current lazy implementation of Dijkstra's inserts duplicate key-value pairs (keys being the node index and the value being the shortest distance to get to that node) in our PQ because it's more efficient to insert a new key-value pair in O(log(n)) than it is to update an existing key's value in O(n).
	2. This approach is inefficient for dense graphs because we end up with several stale outdated key-value pairs in our PQ. The eager version of Dijkstra's avoids duplicate key-value pairs and supports efficient value updates in O(log(n)) by using an Indexed Priority Queue (IPQ).
		1. Indexed Priority Queue
			1. Allows access to (key, value) pairs in constant time and updates in O(log(n)) time, if we are using a binary heap
9. Eager Dijkstra's
	1. (0, 0)
	2. (1, 5)
		1. (1, 4) (updated)
	3. (2, 1)
	4. (4, 13)
		1. (4, 9)
	5. (3, 7)
	6. (5, 10)
20. Eager Dijkstra's code:

```
# Runs Dijkstra's algorithm and returns an array that contains
# the shortest distance to every node from the start node s.
# g - adjacency list of weighted graph
# n - the number of nodes in the graph
# s - the index of the starting node (0 <= s < n)
function dijkstra(g, n, s):
  vis = [false, false, ..., false] # size n
  dist = [inf, inf, ... , inf, inf] # size n
  dist[s] = 0
  ipq = empty indexed priority queue
  ipq.insert(s, 0)
  while ipq.size() != 0:
    index, minValue = ipq.poll()
	vis[index] true
	if dist[index] < minValue: continue
	for (edge : g[index]):
	  if vis[edge.to]: continue
	  newDist = dist[index] + edge.cost
	  if newDist < dist[edge.to]:
	    dist[edge.to] = newDist
		if !ipq.contains(edge.to):
		  ipq.insert(edge.to, newDist)
		else:
		  ipq.decreaseKey(edge.to, newDist)
  return dist
```

21. D-ary Heap optimization
	1. When executing Dijkstra's algorithm, especially on dense graphs, there are a lot more updates (i.e decreaseKey operations) to key-value pairs than there are dequeue (poll) operations.
	2. A D-ary heap is a heap variant in which each node has D children. This speeds up decrease key operations at the expense of more costly removals.
	3. Example: D-ary Heap (with D = 4)
	
	```
	                     (5, 2)
							  
	  (2, 6)    (3, 3)            (8, 5)    (9, 4)
	  |          |                 |         |
	()()()()   ()()()()          ()()()()  ()()()() 
	```
	
		1. Suppose we want to update the node with index 6 to have a new shortest distance of 1 (a.k.a decreaseKey(6, 1))
		2. Assuming we have an Indexed D-ary Heap we can update the key's value in O(1) but we still need to adjust its position
			1. Bubble-up is required
		3. In contrast suppose we want to remove the root node
			1. In a D-ary heap we have to search D children of the current node to find the minimum (k, v) pair to swap downwards
				1. Removals are clearly much more expensive, but they are also a lot less common in Dijkstra's than decreaseKey operations
					1. There are much fewer removals as compared to updates in Dijkstra's algorithm
						1. This might be a good candidate for the algorithm
	4. Optimal D-ary Heap degree
		1. What is the optimal D-ary heap degree to maximize performance of Dijkstra's algorithm?
			1. In general `D = E/V` is the best degree to use to balance removals against drecreaseKey operations improving Dijkstra's time complexity to `O(E*log_E/V(V))` which is much better especially for dense graphs which have lots of decreaseKey operations
22. The state of the art
	1. The current state of the art as of now is the Fibonacci heap which gives Dijkstra's algorithm a time complexity of O(E + Vlog(V))
	2. However, in practice, Fibonacci heaps are very difficult to implement and have a large enough constant amortized overhead to make them impractical unless your graph is quite large (to see the benefit)
23. Source code and slides: [github.com/williamfiset/algorithms](github.com/williamfiset/algorithms)

### Dijkstra's Shortest Path Algorithm | Source Code ###
1. `Edge`
	1. `int to`
	2. `double cost`
2. `createEmptyGraph()` - initializes adjacency list
3. `addEdge(int from, int to, int cost)` (`cost` must not be negative)
4. `getGraph()`
5. `dijkstra(int start, int end)`
	1. `MinIndexedDHeap<Double> ipq = new MinIndexedDHeap<>(degree, n)` (another video in DS series)
	2. `Arrays.fill(dist, Double.POSITIVE_INFINITY)`
	3. `if (minValue > dist[nodeId]) continue;` - we have already found the path
	4. `if (nodeId == end) return dist[end]`
6. `public List<Integer> reconstructPath(int start, int end)`
	1. `Collections.reverse(path)` (`List<Integer> path`)

### Bellman-Ford Algorithm ###
1. BF algorithem overview
	1. In graph theory, the Bellman-Ford (BF) algorithm is a Single Source Shortest Path (SSSP) algorithm. This means it can find the shortest path from one node to any other node.
	2. However, BF is not ideal for most SSP problems because it has a time complexity of O(EV). It is better to use Dijkstra's algorithm which is much faster. It is on the order of O((E + V) log(V)) when using a binary heap priority queue.
	3. However, Dijkstra's algorithm can fail when the graph has negative edge weights. This is when BF becomes really handy because it can be used to detect **negative cycles** and **determine where they occur**.
	4. Finding negative cycles can be useful in many types of applications. One particularly neat application arises in finance when performing an **arbitrage** between two or more markets.
		1. We can start with a stock or security and end up with a profit - risk-free gains
2. Negative Cycles
	1. Negative cycles can manifest themselves in many ways
	
	```
	o -> 1 -> 2 ...
	    / \
		---
		 -1
	```
	
		1. -ve subloop
			1. Infinite cycle
	2. Negative cycle with net-gain < 0
	
	```
	1 -4-> 3
	^      |
	|     -6
	|      |
	+--1---2
	```
	
		1. Net-change = -1
3. BF Algorithm Steps
	1. Let's define a few variables
		1. Let E be the number of edges
		2. Let V be the number of vertices
		3. Let S be the id of the starting node
		4. Let D be an array of size V that tracks the best distance from S to each node
	2. Set every entry in D to +inf
	3. Set D[S] = 0
	4. Relax each edge V-1 times:
	
	```
	for (i = 0; i < V - 1; i = i + 1):
	  for edge in graph.edges:
	    // Relax edge (update D with shorter path)
		if (D[edge.from] + edge.cost < D[edge.to])
		  D[edge.to] = D[edge.from] + edge.cost
	```
	
	5. Repeat to find nodes caught in a negative cycle (run the algorithm a second time)
	
	```
	// Repeat to find nodes caught in a negative cycle
	for (i = 0; i < V - 1; i = i + 1):
	  for edge in graph.edges:
	    if (D[edge.from] + edge.cost < D[edge.to])
		  D[edge.to] = -inf
	```
	
		1. Edges can be processed in any order
	
	6. Example:
4. GitHub repo: Source code

### Floyd-Warshall All Pairs Shortest Path Algorithm ###
1. FW algorithm overview
	1. In graph theory, the Floyd-Warshall (FW) algorithm is an All-Pairs Shortest Path (APSP) algorithm. This means it can find the shortest path between all pairs of nodes.
	2. The time complexity to run FW is `O(V^3)` which is ideal for graphs no larger than a couple hundred nodes.
2. Shortest Path (SP) Algorithms
	1. BFS
		1. Complexity: `O(V + E)`
		2. Recommended graph size: **Large**
		3. Good for APSP? Only works on unweighted graphs
		4. Can detect negative cycles? No
		5. SP on graph with weighted edges: Incorrect SP answer
		6. SP on graph with unweighted edges: **Best algorithm**
	2. Dijkstra's
		1. Complexity: `O((V + E) log(V))`
		2. Recommended graph size: **Large/Medium**
		3. Good for APSP? Ok
		4. Can detect negative cycles? No
		5. SP on graph with weighted edges: Best algorithm
		6. SP on graph with unweighted edges: Ok
	3. Bellman Ford
		1. Complexity: `O(EV)`
		2. Recommended graph size: Medium/Small
		3. Good for APSP? Bad
		4. Can detect negative cycles? Yes
		5. SP on graph with weighted edges: Works
		6. SP on graph with unweighted edges: Bad
	4. Floyd Warshall
		1. Complexity: `O(V^3)`
		2. Recommended graph size: Small
		3. Good for APSP? **Yes**
		4. Can detect negative cycles? **Yes**
		5. SP on graph with weighted edges: Bad in general
		6. SP on graph with unweighted edges: Bad in general
3. Graph Setup
	1. With FW, the optimal way to **represent our graph s with a 2D adjacency matrix m** where cell `m[i][j]` represents the edge weight of going from node `i` to node `j`
	2. Note: In the graph above, it is assumed that **the distance from a node to itself is zero**. This is why the diagonal is all zeros.
	3. If there is no edge from node i to node j then set the edge value for `m[i][j]` to be positive infinity.
	4. Important: If your programming language does not support a special constant for +inf such that inf + inf = inf and x + inf = inf, then **avoid using `2^31 - 1` as infinity!** This will cause integer overflow; prefer to use a large constant such as `10^7` instead
	5. The main idea behind the Floyd-Warshall algorithm is to gradually **build up all intermediate routes between nodes i and j** to find the optimzal path.
		1. Suppose our adjacency matrix tells us that the distance from a to b is: `m[a][b]` = 11
		2. Suppose there exists a third node, c. If `m[a][c] + m[c][b] < m[a][b]`, then it's better to route through c
	6. The goal of Floyd-Warshall is to eventually consider going through all possible intermediate nodes on paths of different lengths
		1. We can get longer and longer paths with more intermediate nodes betwen a and b
4. The Memo Table
	1. Let 'dp' (short for Dynamic Programming) be a 3D matrix of size n x n x n that acts as a memo table.
	
	```
	dp[k][i][j] = shortest path from i to j routing through nodes {0, 1, ... , k-1, k}
	```
	
	2. Start with k = 0, then k = 1, then k = 2, ... This gradually builds up the optimal solution routing through 0, then all optimal solutions routing through 0 and 1, then all optimal solutions routing through 0, 1, 2, etc... up until n-1 which stores to APSP solution.
		1. Specifically `dp[n-1]` is the 2D matrix solution we're after.
	3. In the beginning the optimal solution from i to j is simply the distance in the adjacency matrix.
	
	```
	dp[k][i][j] = m[i][j] if k = 0
	```
	
	4. Otherwise:
	
	```
	dp[k][i][j] = min(dp[k - 1][i][j], dp[k - 1][i][k] + dp[k - 1][k][j])
	```
	
		1. Reuse the best distance from i to j with values routing through nodes {0, 1, ... , k-1} (partial solution)
		2. Find the best distance from i to j through node k reusing best solutions from {0, 1, ... , k - 1}
		3. The right side of the main function in English essentially says: "go from i to k" and then "go from k to j"
5. Currently we're using `O(V^3)` memory since our memo table 'dp' has one dimension for each of k, i, and j.
	1. Notice that we will be looping over k starting from 0, then 1, 2, ... and so fourth. The important thing to note here is that previous result builds off the last since we need state k - 1 to compute state k. With that being said, it is possible to **compute the solution for k in-place** saving us a dimension of memory and reducing the space complexity to `O(V^2)`
	2. The new recurrence relation is:
	
	```
	dp[i][j] = m[i][j] if k = 0
	dp[i][j] = min(dp[i][j], dp[i][k] + dp[k][j]) if k > 0
	```
	
6. Pseudocode:

```
# Global/ class scope variables
n = size of the adjacency matrix
dp = the memo table that will contain APSP soln
next = matrix used to reconstruct shortest paths

function floydWarshall(m):
  setup(m)
  
  # Execute FW all pairs shortest path algorithm.
  for (k := 0; k < n; k++):
    for (i := 0; i < n; i++):
	  for (j := 0; j < n; j++):
	    if (dp[i][k] + dp[k][j] < dp[i][j]):
		  dp[i][j] = dp[i][k] + dp[k][j]
		  next[i][j] = next[i][k]
  # Detect and propagate negative cycles.
  propagateNegativeCycles(dp, n)
  
  # Return APSP matrix
  return dp
```

```
function setup(m):
  dp = empty matrix of size n x n
  
  # Should contain null values by default
  next = empty integer matrix of size n x n
  
  # Do a deep copy of the input matrix and setup
  # the 'next' matrix for path reconstruction.
  for (i := 0; i < n; i++):
    for (j := 0; j < n; j++):
	  dp[i][j] = m[i][j] # k = 0 case
	  if m[i][j] != +inf:
	    next[i][j] = j 
```

7. Negative Cycles
	1. What do we mean by a negative cycle?
		1. They can manifest themselves in many ways
			1. Self-loop with -ve weights
			2. Groups of nodes:
				1. The important thing to ask ourselves is does the optimal path from node i to node j go through a red node? If so the path is affectd by the negative cycle and is compromised.
					1. Some paths avoid red-nodes
8. Re-run the Floyd-Warshall algorithm the second time

```
function propagateNegativeCycles(dp, n):

  # Execute FW APSP algorithm a second time but
  # this time if the distance can be improved
  # set the optimal distance to be -inf.
  # Every edge (i, j) marked with -inf is either
  # part of or reaches into a negative cycle.
  for (k := 0; k < n; k++):
    for (i := 0; i < n; i++):
	  for (j := 0; j < n; j++):
	    if (dp[i][k] + dp[k][j] < dp[i][j]):
		  dp[i][j] = -inf
		  next[i][j] = -1 # indicator
```

9. Reconstructing the shortest paths

```
#  Reconstructs the shortest path between nodes
# 'start' and 'end'. You must run the
# floydWarshall solver before calling this method.
# Returns null if path is affected by negative cycle.
function reconstructPath(start, end):
  path = []
  # Check if there exists a path between
  # the start and the end node.
  if dp[start][end] == +inf: return path 
  
  # Reconstruct path from next matrix
  for (at := start; at != end; at = next[at][end]):
    if at == -1: return null
	path.add(at)
	
  if next[at][end] == -1: return null
  path.add(end)
  return path
```

### Floyd-Warshall All Pairs Shortest Path Algorithm | Source Code ###
1. `FloydWarshallSolver` class
	1. `constructGraph` - initializes matrix with +inf and 0 of i = j
	2. `solver.getApspMatrix()`
	3. Print all shortest path values
	4. Reconstruct paths
		1. Loop through all pairs of nodes
		2. Pretty-format the output
		3. `reconstructShortestPath(int start, int end)`

### Bridges & Articulation Points ###
1. What are bridges & articulation points?
	1. A bridge / cut edge is any edge in a graph whose removal increases the number of connected components.
	2. Example:
	
	```
	  0           6
	 /  \        / \
	1 -- 2 ---- 5   7
	    /        \ /
		3 -- 4    8
	```
	
		1. 2-5 - bridge
		2. 2-3 - bridge
		3. 3-4 - bridge
		
	3. An articulation point / cut vertex is any node in a graph whose removal increases the number of connected components.
		1. 2
		2. 3
		3. 5
2. Bridges and articulation points are important in graph theory because they often hint at weak points, bottlenecks or vulnerabilities in a graph. Therefore, it's important to be able to quickly find/detect when and where these occur.
3. Both problems are related so we will develp and algorithm to find bridges and then modify it slightly to find articulation points.
4. Bridges algorithm
	1. Start at any node and do a Depth First Search (DFS) traversal labeling nodes with an increasing id value as you go. Keep track the id of each node and the smallest low-link value. During the DFS, bridges will be found where the id of the node your edge is coming from is less than the low link value of the node your edge is going to.
	2. Note: The low-link value of a node is defined as the smallest [lowest] id reachable from that node when doing a DFS (including itself).
5. Example:

```
  0           6
 /  \        / \
1 -- 2 ---- 5   7
	/        \ /
	3 -- 4    8
```

	1. Mark undirected edges as directed edges as we visit nodes
	2. Incement id of each node visited
	3. The low-link value is defined as the smallest [lowest] id reachable from that node using forward and backward edges
		1. Initialize low-link values of each node to be equal to the node's id
			1. The low-link value of node 1 is 0 since node 0 is reachable from node 1.
				1. node 0 has an id of 0
				2. We update node 1's low-link value to 0
			2. The low-link value of node 2 is also 0 (node 0 is reachable)
			3. Cannot update low-link values for nodes 3, 4, and 5
			6. Node 6's low-link value can be updated to 5 since node 5 is reachable from node 6
			7. Node 7 and 8 also have a low-link value of 5
		2. Now notice that the condition for a directed edge 'e' to have nodes that belong to a bridge is when the `id (e.from) < lowlink(e.to)`
			1. Where `e.from` is the node the directed edge starts at and `e.to` is the node the directed edge ends at.
			2. Why?
				1. There was no edge connecting back to the component (single directed edge exists)
6. Complexity
	1. What's the runtime of our algorithm to find bridges? Right now we're doing one DFS to lable all the nodes plus V more DFSs to find all the low-link values, giving us roughtly: `O(V(V + E))`
	2. Fortunately, we are able to do better by updating the low-link values in one pass for `O(V + E)`
7. Psuedocode

```
id = 0
g = adjacency list with undirected edges
n = size of the graph

# In these arrays index i represents node i
ids = [0, 0, ... , 0, 0] # length n
low = [0, 0, ... , 0, 0] # length n
visited = [false, ... , false] # length n

function findBridges():
  bridges = []
  # Finds all bridges in the graph across
  # various connected components.
  for (i = 0; i < n; i = i + 1):
    if (!visited[i]):
	  dfs(i, -1, bridges)
  return bridges
```

```
# Perform Depth First Search (DFS) to find bridges.
# at = current node, parent = previous node. The
# bridges list is always of even length and indexes
# (2*i, 2*i + 1) form a bridge. For example, nodes at
# indexes (0, 1) are a bridge, (2, 3) is another etc...
function dfs(at, parent, bridges):
  visited[at] = true
  id = id + 1
  low[at] = ids[at = id
  
  # For each edge from node 'at' to node 'to'
  for (to : g[at]):
    if to == parent: continue
	if (!visited[to]):
	  dfs(to, at, bridges)
	  low[at] = min(low[at], low[to])
	  if (ids[at] < low[to]):
	    bridges.add(at)
		bridges.add(to)
	else:
	  low[at] = min(low[at], ids[to])
```

8. Example:
	1. If we visit an already visited node, we can update the low[at] value
	2. If we visit and return, we can update the low[at] value
9. Articulation points
	1. Articulation points are related very closely to bridges. It won't take much modification to the finding bridges algorithm to find articulation points.
	2. Simple observation about articulation points:
		1. On a connected component with three or more vertices if an edge `(u, v)` is a bridge, then either u or v is an articulation point.
			1. Example:
			
			```
			      2
			     /|
			0 - 1 |
			     \|
				  3
			```
			
				1. 1 is the articulation point
	3. However, this condition alone is not sufficient to capture all articulation points. There exist cases where there is an articulation point without a bridge:
		1. There are no bridges but node 2 is an articulation point since its removal would cause the graph to split into two components.
		
		```
		0   3
		|\ /|
		| 2 |
		|/ \|
		1   4
		```
		
		2. When do these cases occur?
			1. Clue: cycles
				1. All nodes recive the low-link value of a node
					1. This indicates that there is a cycle
						1. If a node that started the cycle is removed, it severs the graph in two
							1. Exception:
								1. The only time id(e.from) == lowLink(e.to) fails is when the starting node has 0 or 1 outgoing directed edges. This is because either the node is a singleton (standalone node) (0 case) or the node is trapped in a **cycle** (1 outgoing edge case).
								2. Here the condition is met, but the starting node only has 1 outgoing edge. Therefore, the start node is not an articulation point.
								
								```
								1
								|\
								0 2
								|/
								3
								```
								
									1. If we add another edge to the starting node, it becomes an articulation point
									
									```
									   1
									   |\
									4--0 2
									   |/
									   3
									```
									
										1. However, when there are more than 1 outgoing edges the starting node can escape the cycle and thus becomes an articulation point!
10. Pseudocode:

```
id = 0
g = adjacency list with undirected edges
n = size of the graph
outEdgeCount = 0 # change

# In these arrays index i represents node i
low = [0, 0, ... , 0, 0] # Length n
ids = [0, 0, ... , 0, 0] # Length n
visited = [false, ... , false] # Length n
isArt = [false, ... , false] # Length n

function findArtPoints():
  for (i = 0; i < n; i = i + 1):
    if (!visited[i]):
	  outEdgeCount = 0 # Reset edge count
	  dfs(i, i, -1)
	  isArt[i] = (outEdgeCount > 1)
  return isArt
```

```
# Perform DFS to find articulation points.
function dfs(root, at, parent):
  if (parent == root): outEdgeCount++
  visited[at] = true
  id = id + 1
  low[at] = ids[at] + 1
  
  # For each edge from node 'at' to node 'to'
  for (to : g[at]):
    if to == parent: continue
	if (!visited[to]):
	  dfs(root, to, at)
	  low[at] = min(low[at], low[to])
	  # Articulation point found via bridge
	  if (ids[at] < low[to]):
	    isArt[at] = true
	  # Articulation point found via cycle
	  if (ids[at] == low[to]):
	    isArt[at] = true
	else:
	  low[at] = min(low[at], ids[to])
```

### Bridges & Articulation Points | Source Code ###
1. `BridgesAdjacencyList`
	1. `constructGraph`
		1. `List<List<Integer>> constructGraph(int n)`
	2. `addEdge(List<List<Integer>> graph, int from, int to)`
	3. `List<Integer> bridges = solver.findBridges()`
	4. `dfs(int at, int parent, List<Integer> bridges)`
2. `ArticulationPointsAdjacencyList`
	1. `isArticulationPoint = new boolean[n]`;

### Tarjan's Strongly Connected Components Algorithm (UPDATED) ###
1. What are SCCs?
	1. Strongly Connected Components (SCCs) can be thought of as **self-contained cycles** within a **directed graph** where every vertex in a given cycle can reach every other vertex in the same cycle.
	
	```
	o <-> o <-- o <-- o
	^     |     |\    ^ \  /|
	|     |     | \   |  o  | 
	v     v     v  v  | /  \|
	o --> o <-> o <-- o
	```
	
		1. There are 4 SCCs
		2. For each component, there is no way to find a path that leaves a component and comes back
2. Low-Link Values
	1. The low-link value of a node is the smallest [lowest] node id reachable from that node when doing a DFS (including itself)
		1. The low-link of node 1 is 0, since node 0 is node with the lowest id reachable from node 1
	2. If we assign all the low-link values to all the nodes, we get the following:
		1. All nodes that have the same low-link value belong to the same SCC
	3. Flaw:
		1. It is highly dependent on the traversal order of the DFS 
			1. Started DFS on the rightmost node, resumed DFS on node 2, and then resumed DFS on node 4 to finish labelling all nodes in the graph
				1. Node 6 will have a low-link value of 0
					1. This is wrong
		2. Important: Depending on where the DFS starts, and the order in which nodes/edges are visited, the low-link values for identifying SCCs could be wrong. In the context of Tarjan's SCC algorithm, we maintain an invariant that prevents SCCs to interfere with the low-link value of other SCCs

### Tarjan's Strongly Connected Components Algorithm | Source Code ###
### Travelling Salesman Problem ###
### Travelling Salesman Problem | Source Code ###
### Existence of Eulerian Path and Circuit ###
### Eulerian Path Algorithm ###
### Eulerian Path Source Code ###

## Network Flow ##
### Max Flow Ford Fulkerson | Network Flow ###
### Max Flow Ford Fulkerson | Source Code ###
### Unweighted Bipartite Matching | Network Flow ###
### Bipartite Matching | The Mice and Owls Problem | Network Flow ###
### Bipartite Matching | The Elementary Math Problem | Network Flow ###
### Edmonds Karp | Network Flow ###
### Edmonds Karp | Network Flow | Source Code ###
### Capacity Scaling | Network Flow ###
### Capacity Scaling | Network Flow | Source Code ###
### Dinic's Algorithm | Network Flow ###
### Dinic's Algorithm | Network Flow | Source Code ###

## Bonus Topics ##
### Union Find Data Structure ###
### Kruskal's Minimum Spanning Tree Algorithm ###
### Prim's Minimum Spanning Tree (Lazy Version) ###
### Prim's Minimum Spanning Tree (Eager Version) ###
### Prim's Minimum Spanning Tree Source Code ###
### The Sparse Table Data Structure ###
### Sparse Table Source Code ###
### Lowest Common Ancestor (LCA) Problem ###