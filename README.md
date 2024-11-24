# CI2024_lab3
Repository for the 3rd lab of the Computational Intelligence course

# General overview and problem description
This third laborarory aims to implement both uninformed an informed path-search algorithms for the **Sliding Tile Puzzle** fro a general dimension of the grid $n*n$.
## Structure
The puzzle consists of a grid of tiles, one of which is empty (coded with symbol '0'). The other tiles are labeled with numbers, often starting from 1 up to $n^2−1$.
The objective is to rearrange the tiles to match a specific target configuration called the "solved state", starting from a random initial configuration.
## Rules
+ Only tiles adjacent to the blank space can be moved
+ Moves are made by sliding a tile into the blank space, thereby changing its position with the blank.
## Mathematical properties
+ State space: For a $n*n$ puzzle, there are $n^{2}!$ possible arrangements of tiles, however only half of these configurations are solvable due to the puzzle's *parity* property determined by the number of the inversions.
+ Complexity: The complexity of the puzzle grows exponetially with the dimension of the grid.
+ Solvability: A puzzle configuration is solvable if certians conditions are met (see bottom of this section for more details).


### Notes on the mathematical properties:
#### *Manhattan Distance* 
Definition of distance betweeen two points (in or case in a 2D space), as: <br>$d = |P_{x_2} - P_{x_1}|+|P_{y_2} - P_{y_1}|$  
In our problem the Manhattan Distance measures how far each tile is from its goal position. For a puzzle configuration, the total Manhattan Distance is the sum of the Manhattan distances for all tiles from their respective target positions.  
It also represent the perfect candidate for the *admissible fuction* for an A* algorithm, since it is both **admissible** since it does not overestimate the cost, and **consistent**, as it satisfies the triangular inequality.  
#### *Solvability of the sliding puzzle*
Not all configurations of the sliding tile puzzle are solvable. The solvability of a configuration depends on its inversion count and the dimensions of the puzzle grid.  
An *inversion* occurs when a larger numbered tile precedes a smaller numbered tile in the row-major order of the puzzle (ignoring the blank tile). This particular definition is the core of the sule of sovability for this problem, as depending on the even-ness / odd-ness of the dimension of the grid, the puzzle is solvable if:
+ Case *n* is even: the total number of inversions is even, and the blank tile is in an odd row from the bottom, or the total number of inversions is odd, and the blank tile is in an even row from the bottom.
+ Case *n* is odd: the total number of inversions is even.<br>
Or, as mentioned in the main subsection, if the number of inversions (pairs of tiles in the wrong order) has the same parity as the *Manhattan distance* of the blank space from its goal position

# Proposed solutions
## Uninformed strategies
### BFS
The sliding puzzle can be solved via BFS (Breadth-First-Search) uninformed startegy. This strategy is implemented with attention at previous states to not repeat itself, capable of acheiving always the best solution.  
However it is very computationally expensive both in terms of time and space, since it keeps track of all visted spaces and it will eventually explore nearly all of the possible states of the problem (remember that their number has been defined in the *Mathemaical prperties* in the prevoius section).  
Therefore I suggest using this only for puzzles with dimension 3x3.


### DFS
The second uninformed strategy is the DFS (Depth-First-Search).  
This solution always solves the prboblem if a solution exists, but does not guarantee the optimal one. This implementation is very resource-consuming in terms of space since it does store the found states in order to avoid repetitions or loops, but it explores all the solutions space only in the worst-case scenario.
Unfortunatly, due to limited resources the recursive implementation presented is not viable as it reaches the recursion limit preatty soon.

## Informed strategy
### A*
**A*** Is the is a search algorithm used to find the shortest path in a graph or grid. It uses a combination of two costs for evaluating nodes:
+ g(n): The cost to reach the current node (from the starting point).
+ h(n): The estimated cost to reach the goal (from the current node). This is provided by a heuristic function.

A* evaluates each node using the formula: $f(n)=g(n)+h(n)$.  
By using the *Manahattan cost* as heuristic function, I present an A* implementation capable of solving nxn general problem within reasonable time.
I also credit Stefano Fumero for path representation and the idea of using bytes as representation of the state inside the open_list and visited set, since it is hashable. 

# Experiments and conslusions
## Experiments
In this section I report all the experiments with all the proposed solutions described above
| Strategy           | Puzzle Dimension                         | Quality         | Cost | Efficiency |
|--------------------|---------------------------------------|-----------------|------|------------|
| BFS                | 3               | 24 (Optimal)    |   $(4^{24}$-1)/3| close to 0           |
| DFS                | [Not considered]                      |        /        |  /    |     /       |
| A*                 |  3                                     |  16               |  508    |    0.03        |

in the following table i report only the experiments done with the A* algorithm
|Puzzle Dimension | Quality | Cost | Efficiency |
|-----------------|---------|------|------------|
|4                |    44   |   212928  |    0       |
|5                |    /    |   /  |    /       |
|6                |    /    |   /  |    /       |
|7                |    /    |   /  |    /       |

Overall the A* algorithm with the manhattan distance as heurisitc is the most efficient algorithm to solve the sliding puzzle problem, assuring the optimal solution.
The exponentially growing complexity of the problem in relation to its size, however, make it unfeasible to solve at puzzle dimensions major to 5, and the efficiency of the algorithm using this heuristic is close to 0, since it considers all the neighbor states, suggesting that for this very problem there might be more suited 'h' functions for this problem.
Another possibility might be using a 'h' function which overestimates the distance to the solution, but in this case the A* algorithm will not provide the best path anymore, since it is necessary to *h* to be **admissible**.
## Conclusions
N-sliding puzzzle is a very challenging problem even to informed algorithms, and it results unapproachable in reasonable time for uninformed ones.  
This is mainly attribuited to the difficulty to find a good admissible heuristic for the problem, since the distance from the solution 






