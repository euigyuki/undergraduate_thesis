# Derrick Kim's undergraduate thesis


## Content

1.  Quadratic Programming
2.  Karush-Kuhn Tucker Conditions
3.  Newton's Method
4.  Interior Point Method
5.  Support Vector Machines Quadratic Program Formulation 
6.  Primal Log Barrier Problem
7.  Final Formulation
8.  Final thoughts



## Part 1: Quadratic Programming

A linearly-constrained quadratic programming problem is a constrained optimization problem where we
minimize a convex quadratic function subject to linear constraints.

In this paper, I try to add a variety of conditions and techniques to uniquely formulate a higher dimension problem, and attempt to solve it.




## Part 2: Karush-Kuhn Tucker Conditions

Given a general function that we want to minimize, the optimal solution necessarily has to follow the KKT
conditions. The KKT conditions are derived from the standard Lagrangian multiplier approach with stationarity, primal feasibility, dual feasibility, and complementary slackness conditions.





## Part 3: Newton's Method


Newton’s method is an iterative method that helps us find the root of a function. We start with an initial
guess that is a good approximation of the root, and use multiple iterations by using the Jacobian matrix instead of the traditional tangent line.


## Part 4: Interior Point Method

Unlike previous methods, Interior Point Methods are not restricted by linearity, and we use a barrier function to encode the convex feasible region.

With the iterations, we traverse within the feasible region.  


Here is the part of the results.
11 points:
| Algorithm        | value    |  time taken  | min value
| --------         | -----:   | ----:        |  :----: |
| br               | 5.0079   |   937691     |  5.0079 |
| bt               | 5.0079   |   273147     |  5.0079 |
| 2opt             | 5.0079   |   1133       |  5.0079 |
| 3opt             | 5.0079   |   3201       |  5.0079 |
| GA               | 7.3151   |   1034483    |  5.0079 |

50 points:
| Algorithm        | value    |  time taken  | min value
| --------         | -----:   | ----:        |  :----:  |
| br               | 0        |   0          |  8.95889 |
| bt               | 0        |   0          |  8.95889 |
| 2opt             | 9.79278  |   30754      |  8.95889 |
| 3opt             | 8.95889  |   1193881    |  8.95889 |
| GA               | 19.8612  |   6499453    |  8.95889 |

The runtime compexity of Bruteforce is O(n!), and the worst case for backtracking is O(n!).
In the results part. I seperately run 11, 12, 13, 20, 30, 40, 50 points for these algorithms with the same input. But the brute force and backtracking can not handle so much of hte points, so they stop at 13. So for 20 -50 parts, I can't get the best answer, so I just draw the comparision for each method. From the results we can see:


## Part 5: Support Vector Machines Quadratic Program Formulation 

### Step 5.5



After we get all the node inside, the only thing we need to do is using DFS to travel all the nodes inside, with the condition if once the current children meet their parents, we regard there is a cycle inside.

```python
if(DFS_helper(location_ids[i], marks, parent, res) == true){
        PlotPointsandEdges(res, square);
        return true;
```





And each time i push in the node, i need to update the indegree for all of them, so the time complexity is O(n^2).

## Part 6:  Primal Log Barrier Problem



## Part 7:  Final Formulation

## Part 8:  Final Thoughts





And below is how I reverse the path
```python
def getX1Cord(w1,w2,b,x2Cord):
    x1Cord = []
    for i in range(len(x2Cord)):
      x1Cord.append((-w2*x2Cord[i]-b)/w1)
    return x1Cord
```






