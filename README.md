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
## Matematical properties
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


