# Tutorial No. #1

## Search Problems
What is the fastest route from Tel-Aviv to Haifa? In this course, we'll represent problems with graphs. So the first step will be to represent the problem, then we'll run an algorithm on that graph to solve the problem.

### Definitions:

**Defining the Search Model:**
A search Model is a tuple of four:
1. S - set of states in the Search Space.
2. O - set of Operators, from one state to the following state.
3. I in S - Initial State.
4. G subset of S - Goal states.

**Domain:** 
Domain: O -> P(S) is an Operator(Function) that defines for each Operator op in O, which states we can apply op on. Domain(op) = {s in S | op(s) != empty set }
**Succ:** 
Succ: S -> P(S) is an Operator(Function) that defines for each state s in S, which states we can get to from s by applying an Operator from O on s. (Successors set of s)

### What are we searching for?
We search for a goal state Sg in G, that has a path from an Initial State, but wait a second, is that it ? NO! We can have variations of search problems, e.g. not all paths have the same "price", which leads to the following 
**definition:** 
* A Cost function is defined as follows: Cost: { <s1, s2> | s1 in S & s2 in Succ(s1)} -> R

Now that we have a cost for each "step" of our choice, we can ask the following question:

### What can be considered as a good path ?
* We can define a fixed value, and a path with a cost less than that value is considered "Good enough".
* We can declare an "anytime algorithm", that finds better routes the more time it runs.
* We can search for the path with the minimal path cost!

## Search Tree VS States Graph
### Definitions:

**Search Tree:**
Given a states Graph G=(S,E), where S is States Set and E are the Edges Set, we define a Search Tree as follows:
* State s in S is a vertex in a States Graph, which is a configuration that we can get to in "any" search.
* Vertex v in V in a Search Tree represents a state but with context, (e.g. which choices led us to this state? or which path did we choose?), thus, in a Search Tree, a single state can appear more than once in different contexts.

## Intro to advanced graph search!

### Definitions:

**Complete algorithm:** An algorithm is called complete, (Shalem in Hebrew), if it guarantees to return a solution if one exists.
**Optimally efficient algorithm:** An algorithm is called optimally efficient, (Kabeel in Hebrew), if it guarantees to return the solution with minimal cost, if a solution exists.

NOTE: An optimally efficient algorithm is a complete algorithm. (Kabeel -> Shalem, Not Shalem -> Not Kabeel).

**Graph Search Algorithm:** Usually complicated but we don't need to visit the same vertex (state) twice.
**Tree Search Algorithm:** Easy to implement, memory/time efficient.

**Expanded vertex:** A vertex s is introduced if in the algorithm run, we applied succ function in it.
**Created vertex:** A vertex s is created if in the algorithm run, there was a vertex s' that was expanded.

**Branching Factor - b:** Maximum number of children of a vertex v.
**Solution Depth - d:** The maximum depth of a target state (vertex) in the Tree.
**Tree Depth - D:** Height of the Search Tree.

## Uninformed/exploratory search algorithms:
In the case of uninformed search algorithms, the algorithm must explore the problem space and learn about it while searching for a solution. This is common in many real-world situations where all the information about the problem is not available upfront, and the problem space is not fully known or understood in advance.


### BFS on Tree:

'''python
def BFS(probelm):
	node = make_node(problem.init_state, None)
	if problem.goal(node.state): return solution(node)
	Open = {node}
	while Open is not empty:
		node = Open.pop()
		for is in expand(node.state):
			child = make_node(s, node)
			if problem.goal(child.state): return solution(child)
			Open.insert(child)
	return -1
'''

**Is the algorithm complete?** if the branching factor is finite, then yes!
**Is the algorithm optimally efficient?** yes, becuase the solution is always the closest answer.
**Time and Space Complexity:** O(b^d) wher b is the branching factor and d is the depth of the solution

## DFS on Tree:

'''python
def DFS(probelm):
	node = make_node(problem.init_state, None)
	Open = {node}
	return DFS-recursive(problem, Open)

def DFS-recursive(probelm, Open):
	node = Open.pop()
	if problem.goal(node.state): return solution(node)
	for is in expand(node.state):
		child = make_node(s, node)
		Open.insert(child)
		result = DFS-recursive(problem, Open)
		if result != -1: return result
	return -1
'''

**Is the algorithm complete?** no, depth might be infinte, also, there might be circles!
**Is the algorithm optimally efficient?** no, it's not complete :)
**Time Complexity:** O(b^D) wher b is the branching factor and D is the depth of the solution
**Space Complexity:** O(bD) wher b is the branching factor and D is the depth of the solution


## Backtracking on Tree:

same as DFS, but a state is created before expanding it! we don't creat all the nodes, only the one we need.

'''python
def DFS(probelm):
	node = make_node(problem.init_state, None)
	Open = {node}
	return Backtracking-recursive(problem, Open)

def Backtracking-recursive(probelm, Open):
	node = Open.pop()
	if problem.goal(node.state): return solution(node)
	for is in lazy_expand(node.state):
		child = make_node(s, node)
		Open.insert(child)
		result = DFS-recursive(problem, Open)
		if result != -1: return result
	return -1
'''

**Is the algorithm complete?** no, depth might be infinte, also, there might be circles!
**Is the algorithm optimally efficient?** no, it's not complete :)
**Time Complexity:** O(b^D) wher b is the branching factor and D is the depth of the solution
**Space Complexity:** O(D) wher b is the branching factor and D is the depth of the solution
 

## DFS-L on Tree:

same as DFS, but we allow it to run until a specific depth, if that depth was reached, we do not go forward with that path.

'''python
def DFS-L(probelm, depth):
	node = make_node(problem.init_state, None)
	Open = {node}
	return DFS-L-recursive(problem, Open,depth)

def DFS-L-recursive(probelm, Open):
	node = Open.pop()
	if problem.goal(node.state): return solution(node)
	if depth == 0: return -1
	for is in expand(node.state):
		child = make_node(s, node)
		Open.insert(child)
		result = DFS-recursive(problem, Open, depth-1)
		if result != -1: return result
	return -1
'''

**Is the algorithm complete?** no, we may not reach the solution.
**Is the algorithm optimally efficient?** no, it's not complete :)
**Time Complexity:** O(b^l) wher b is the branching factor and l is the depth we supplied
**Space Complexity:** O(bl) wher b is the branching factor and l is the depth we supplied






