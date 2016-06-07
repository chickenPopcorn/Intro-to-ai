# AI_HW
homework for Artificial Intelligence W4701

To run hw1_rx2119.py
`usage: python hw1_rx2119.py [-help] [-random N-size R-num | -test -method LIST]`
Eg. to generate 5 random 8-pzzle(n=3) for all methods to solve   
`python hw1_rx2119.py -r 3 5`
Eg. to test solver for a specific configuration like the one show below
```
5 8 1
6 3 2
0 4 7
```
`python hw1_rx2119.py -t -a 5,8,1,6,3,2,0,4,7`
or just test it with one method like A*
`python hw1_rx2119.py -t -astar 5,8,1,6,3,2,0,4,7`


I also attached an output.txt file which a set of randomly generated
solvable 8-puzzle game for BFS, DFS, and A*. Because the DSF solution is too long
I didn't print out its solution, however, if did implement a `validate()` method, that
validate the correctness of the solution when it's done

1. BFS is implemented according to the specification
2. DFS is implemented according to the specification
3. A* is implemented according to the specification

4. Smmmarize and compare
```
initializing for BFS
 4 2 3
 7 6 1
 5   8
--- 179.074048996 milliseconds --
n = 3
path to solution is ['UP', 'UP', 'RIGHT', 'DOWN', 'LEFT', 'LEFT', 'DOWN', 'RIGHT', 'UP', 'LEFT', 'UP', 'RIGHT', 'RIGHT', 'DOWN', 'LEFT', 'LEFT', 'UP']
Cost of path = 17
nodes expanded = 10674
max stack/queue size = 5883
max depth of the stack/ queue 18

initializing for DFS
 4 2 3
 7 6 1
 5   8
--- 1917.3719883 milliseconds --
n = 3
Cost of path = 66491
nodes expanded = 91946
max stack/queue size = 42440
max depth of the stack/ queue 66492

initializing for ASTAR
 4 2 3
 7 6 1
 5   8
--- 8.06093215942 milliseconds --
n = 3
path to solution is ['UP', 'LEFT', 'DOWN', 'RIGHT', 'UP', 'UP', 'RIGHT', 'DOWN', 'LEFT', 'LEFT', 'UP', 'RIGHT', 'RIGHT', 'DOWN', 'LEFT', 'LEFT', 'UP']
Cost of path = 17
nodes expanded = 120
max stack/queue size = 69
max depth of the stack/ queue 18
```

  a. cost of the path
    BFS: It always returns the shortest which is also the optimal solution, in this case 17
    DFS: Unusually returns some deep and long solution in this case 66491
    A*: Return the shortest solution like BFS in this case also it's 17

  b. number of nodes expanded
    BFS: It expands nodes layer by layer, in this case it transversed 10,674 nodes which is almost half of all configuration, theoretical speaking it has to transverse B**M but since I implemented duplicate check, it just have to find check all unique configurations up until level 17.
    DFS: It goes straight down which expanded 91,946 nodes before reached goal state
    A*: Using rules of thumb it is able to find the optimal solution only expanding 120 nodes, because it expands the promising direction first because on it's distance from origin and manhattan distance to goal state.

  c. max depth of the stack/queue
    As the TA explained it on Piazza, it is the depth of the tree when a solution is found. It's related to the tree path.
    BFS: the depth of the tree 18
    DFS: the depth of the tree 66,492
    A*: the depth of the tree 18

  d. memory requirements of each approach

  e. running time

    BFS: Since the solution is not every deep in the tree and branch factor is controlled through a set for duplicated states, the runtime as below.
    --- 179.074048996 milliseconds --
    DFS: Because it charges straight down, regardless of the direction that will lead to optimal results. It is slower that all other methods
    --- 1917.3719883 milliseconds --
    A*: Because it's using rule of thumb and duplicated check it will run in shortest time
    --- 8.06093215942 milliseconds --

5. Justify your choice of a heuristic
I chose to calculate manhattan distance for each element in the table from its current position to the its goal state position except the empty cell as the heuristic class. This heuristic is admissible because, The to reach the goal state this is the least number of move we have to make, and in most cases we have to make more move that this, because we can only swap empty cell and it's adjacent cell to change configuration. This mean it underestimate the cost to reach goal state and thus lead to optimal solution by A* search

1. IDA* is implemented according to the specification
But it's kind of slow because I don't use duplicate check
