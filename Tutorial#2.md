# Tutorial 2: Uninformed and Informed Search Algorithms

## Recap:
In the first tutorial, we discussed Uninformed Search algorithms: BFS, DFS, Backtracking, and DFS-L. We'll continue this discussion here.
* BFS - Breadth First Search, explores breadth-wise.
* DFS - Depth First Search, explores depth-wise.
* Backtracking - Similar to DFS, but expands only the next node to visit.
* DFS-L - DFS variant that operates up to a depth 'l'.

## Uninformed Search Algorithms Continued

### ID-DFS:

ID-DFS is a DFS variant that behaves like a breadth-first version of DFS. It runs DFS-L with increasing depth (starting from 1) until it finds a solution or time runs out.

'''python

def Iterative-Deeping-DFS(problems):
	L = 0
	while not Interuupted:
		result = DFS-L(problem, l)
		if result != failure: return result
		L = L+1 
	return result
'''

**Is the algorithm complete?** Yes, if a solution exists at a finite depth, the algorithm will find it.
**Is the algorithm optimally efficient?** Yes, it finds the shallowest solution first.
**Time Complexity:** O(b^d), where 'b' is the branching factor and 'd' is the depth of the tree.
**Space Complexity:** O(bd), where 'b' is the branching factor and 'd' is the depth of the tree.


### Definitions
**Cost of a vertex:**
The cost of a vertex 'v', denoted as g(v), is the sum of the edge values on the path from the initial state 's' to 'v'.

### Uniform Cost Search (UCS):

UCS is similar to Dijkstra's algorithm. It initializes the cost of each vertex as infinite and updates it during the algorithm's execution. The algorithm works as follows:

* Initialize a priority queue 'Open' of expanded vertices, sorted by g(v) value (the cost of the vertex).
* Select the vertex with the minimal g value in 'Open' for the next expansion.

**Can we find a better path to a vertex 'y' that is already expanded and out of 'Open'?**
No, because when 'y' was expanded, it had the minimal cost in 'Open'. Therefore, we can't visit 'y' from a new vertex 'x' in 'Open' with a lower cost since g(x) will be greater than g(y).

**Can we find a better path to a vertex 'y' that hasn't been expanded yet?**
Yes, even if 'y' is still in 'Open'.

**When do we check if a state is a goal/target state?**
We check when we remove a state from the 'Open' priority queue.