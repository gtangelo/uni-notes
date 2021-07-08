## Greedy Method

- Setup
- Algorithm
- Time Complexity
- Optimality
- https://edstem.org/au/courses/5966/discussion/522057

https://edstem.org/au/courses/5966/discussion/522916

**Proving optimal solution**

Show that any optimal solution can be transformed into the greedy solution with equal number of activities: 

- Find the first place where the chosen activity violates the greedy choice. 
- Show that replacing that activity with the greedy choice produces a non conflicting selection with the same number of activities. 
- Continue in this manner till you “morph” your optimal solution into the greedy solution, thus proving the greedy solution is also optimal.

## Dynamic Programming

### General Approach

- Setup
- Subproblem
- Base cases
- Recursion
- How to obtain the final solution - How to obtain the final solution should really just be a call to your recursive function with the initial values provided (e.g. call opt(n) for the final solution)
  - Recuse and memoize OR build DP table bottom up
  - Relate subproblem solutions
- Time complexity
  - number of subproblems * (average cost of solving each subproblem)

### Notes

Dynamic Programming = recursion + memoization

- memoize (remember) and re-use solutions to subproblems that help solve the problem

## Maximum Flow

### General Approach

- Define the network graph (either a graph or bipartite graph)
- Define the vertices and edges
  - Let the vertices be ...
  - Let the edges be ... with a capacity...
    - Some cases, **directed edges have to be two way in opposite directions**. When problem has "undirected graph", you need to include directed edges in both direction for max flow.
    - define directed edge and capacity
  - Insert a super source that connects all of ...
  - Insert a super sink that connects ...
- Define the algorithm (either Ford Fulkerson Algorithm and Edmonds-Karp Max Flow Algorithm)
- Find max flow or minimum cut
- How to find the final solution
- Time complexity

### Notes

- **Residual flow network** for a flow network with some flow in it is the network with the leftover capacities
- An augmenting path is a **path of edges in the residual graph with unused capacity** greater than 0 from the source to sink.
- The **Ford Fulkerson method** is used to find maximal flow in a flow network. We keep **adding flow through new augmenting paths** for as long as it is possible. When there are no more augmenting paths, we have achieved the largest possible flow in the network.
  - Time complexity: $O(|E|f)$
- Minimum Cut gives us the maximal flow, the **total capacity of the edges** that crosses the cut must be minimal. **TLDR - minimal cut does not add up all flow but rather is a cut where the edges flow = capacity**
- Edmonds-Karp Max Flow Algorithm: $O(|V| \times |E|^2)$​
- Super Source/Sinks
- Bipartite Matching
- Vertex Capacities and Splitting
  - Split the vertex into two vertex $v_{in}$ and $v_{out}$ and redirect the edges and construct an edge from $v_{in}$ to $v_{out}$​​​ and define the edge capacity to the vertex capacity
  - When you have intersecting of paths problem, set the vertex capacity to 1 and use the vertex splitting method. If you dont specify the vertex capacity and two path intersect at a vertex, you would have atleast a flow of 2.
- Unit capacity edges can be used to count the number of edges in the minimum cut. Infinite capacity edges on the other hand, ensure that the edge will never be included in the minimum cut which is useful if we want to introduce our own edges (e.g. super sink/source) or effectively remove some edges.
