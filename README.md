# Derrick Kim's undergraduate thesis


## Content

1.  Autocomplete the location name
2.  Find the place's Coordinates in the Map
3.  CalculateShortestPath between two places
4.  The Traveling Trojan Problem
5.  Cycle Detection
6.  Topological Sort
7.  Find K closest points
8.  Learinig Experience




## The data Structure

Each point on the map is represented by the class **Node** shown below and defined in [trojanmap.h](src/lib/trojanmap.h).





```shell
Torjan Map
**************************************************************
* Select the function you want to execute.                    
* 1. Autocomplete                                             
* 2. Find the position                                        
* 3. CalculateShortestPath                                    
* 4. Travelling salesman problem                              
* 5. Cycle Detection                                          
* 6. Topological Sort                                         
* 7. Find K Closest Points                                    
* 8. Exit                                                     
**************************************************************
```


## Step 1: Autocomplete the location name

### 1.1 Function
```c++
std::vector<std::string> TrojanMap::Autocomplete(std::string name);
```

In this function, we need to autocomplete the words the user searching for. 
It's just a easy comparision while traverse all the nodes inside the graph. Here what's the main idea of this function is below:

```shell
std::string temp = it->second.name.substr(0, name.length());
```

### 1.2 Result
In this function, we need to make sure that if the input is invalid, the output should also be invalid.

```shell
1
**************************************************************
* 1. Autocomplete                                             
**************************************************************

Please input a partial location:ch
*************************Results******************************
ChickfilA
Chipotle Mexican Grill
**************************************************************
Time taken by function: 1904 microseconds
```

```shell
**************************************************************
* 1. Autocomplete                                             
**************************************************************

Please input a partial location:66
*************************Results******************************

**************************************************************
Time taken by function: 1748 microseconds
```
We can see from the result, each result comes with almost the same time, because the algorithem is traveling all the points, and check the validation of the name. So the runtime Compelexity is O(n).

## Step 2: Find the place's Coordinates in the Map

```c++
std::pair<double, double> GetPosition(std::string name);
```
### 2.1 Function

In this function, the main idea is same as before, we travell all the nodes, and compare the name with the input.

### 2.2 Results

```shell
2
**************************************************************
* 2. Find the position                                        
**************************************************************

Please input a location:Target
*************************Results******************************
Latitude: 34.0257 Longitude: -118.284
**************************************************************
Time taken by function: 1215 microseconds
```





And below is how I reverse the path
```python
def getX1Cord(w1,w2,b,x2Cord):
    x1Cord = []
    for i in range(len(x2Cord)):
      x1Cord.append((-w2*x2Cord[i]-b)/w1)
    return x1Cord
```
And one thing important, for d3, instead of reverse the path, we need to swap the order of 2 parts of the path.
No matter it is 2-opt or 3-opt, the path we put inside should be the loop, where "end" == "start", only in this way can we make sure we will not miss anything.



### 4.5 Results
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


## Step 5: Cycle Detection

### 5.1 Function
```c++
bool CycleDetection(std::vector<double> &square);
```

In this function, we need to detect whether there contains cycle in the given area. \
First we need to get all the points inside the squre, the way to do this is travel all the nodes in data, and then compare the latitude and longtitude with the given area value.  \
After we get all the node inside, the only thing we need to do is using DFS to travel all the nodes inside, with the condition if once the current children meet their parents, we regard there is a cycle inside.

```cpp
if(DFS_helper(location_ids[i], marks, parent, res) == true){
        PlotPointsandEdges(res, square);
        return true;
```

Inside the dfs_helper, we use follows to decide whether the children can meet their parents

### 5.2 Results
First we define the square as the whole map, and it must have a cycle, and here is the result:

And then we can try to find part of the map, the square is [-118.287, -118.260, 34.020, 34.017], and here is the resuls

What's more, if we use the test number square = [-118.290919, -118.282911, 34.02235, 34.019675], the ouptput should be false.

```cpp
Please input the left bound longitude(between -118.299 and -118.264):-118.290919
Please input the right bound longitude(between -118.299 and -118.264):-228.282911
Please input the upper bound latitude(between 34.011 and 34.032):34.02235
Please input the lower bound latitude(between 34.011 and 34.032):34.019675
-118.291-228.28334.022434.0197
*************************Results******************************
there exist no cycle in the subgraph 
```
And the time cost for these three are:
```shell
Time taken by function: 142552 microseconds
Time taken by function: 44566 microseconds
Time taken by function: 1388 microseconds
```
It's true because the more nodes inside, the more we need to travel. The complexity of this algorithm is O(n)






Secondly, I enlarge the dependency tree and to test the algothrim.


What's more, I put the loop inside :{"Cardinal Gardens", "CVS"}, {"CVS", "Cardinal Gardens"}\
And the result fits that there is no feasible solution for that.
```cpp
location_names = {"Cardinal Gardens", "Coffee Bean1","CVS", "Tap Two Blue", "Target", "Ralphs", "ChickfilA"};
dependencies = {{"Cardinal Gardens", "Coffee Bean1"}, {"Cardinal Gardens", "CVS"}, {"CVS", "Cardinal Gardens"},  {"Coffee Bean1", "Ralphs"},
      {"Tap Two Blue", "CVS"}, {"Tap Two Blue", "Target"}, {"Target", "ChickfilA"}, {"ChickfilA", "CVS"}};
There is no feasible answer
*************************Results******************************
Topological Sorting Results:
```
And each time i push in the node, i need to update the indegree for all of them, so the time complexity is O(n^2).


## Step 7: Find K closest points
### 7.1 Function
In this function, what we need to achieve is finding the k points nearest to the given location, still we regards all the locations are directly conenected!


### 7.2 Result





```cpp
Please input the locations:Ralphs
Please input k:9

*************************Results******************************
Find K Closest Points Results:
1 St Agnes Church
2 Saint Agnes Elementary School
3 Warning Skate Shop
4 Menlo AvenueWest Twentyninth Street Historic District
5 Vermont Elementary School
6 MC39s Barber Shop
7 Anna39s Store
8 Vermont 38 29th Metro 204 Southbound
9 Driveway
**************************************************************
Time taken by function: 6574 microseconds
```



From the result we can see that each time with the growth of the results, our outcomes's orders are same, which means our results can be rely on.\
Then what's interesting is that, no matter how long the results are, the time are the same, which also corresponding to the results that we need to travel all the data inside the map, so the run time complexity is O(n).

## Step 8: Learning Experience

During this semester, what basically I have learnt is how to use CPP to achieve data structrue, e.g tress, heaps. This is a really good class, which fixs a lot about my bad habbit "theory beyond practice". I believe we all can suffer from this, we can think a question to be very easy with the professor's analysing, however when it comes a time for us to do it in practice alone, a lot of of troubles will show up.\
And at first, it will take me like a whole weekend to finish the homework, which it really killed me, a lot bugs showed up, a lot of errors that happens beyond my expectation. What's more, the horrible thing was that, the code could be comnpailed with no probelm, but the results is horrible, far away from I expected. And with practice and practice, I gradually figure out when each error occurs, I can fix the problem quickly and I can gradually "think like a computer", which means the rate of the unexpected outcome become less and less. I am very proud of it!\
When the time comes to do the final project, I decided to do it alone to test myself. Each time I finish a function, a great sence of satisfication will show up, which can motivate me to continue. What's amazing thing is that like this ,step by step, I gradually finsh the whole project, even with the bonus one, which I cannot imagine at the begining. What impressed me most is that when I do the genetic algorithm, at first I thought it's very difficult, but like before, I split it into pieces, slowly writing the helper functions one by one to achieve the whole body of the GA. By the time the results show, I couldn't believe I did it without any error! Though it is not perfect, still have the improvement space, I am still proud of myself have done such thing. It's true the converging rate of it is not perfect, but if I still have time, I will dig into that.\
At last, I really appreciate Mr.Arash for teaching us this lesson, and all this cannot be done without TA's hard work. They build the whole structure for us, which is the most difficult part of the project. I still have a long way to go.\
Again, I really like this lesson, and I am really glad to know such a great professor and the TA team. I appreciate it a lot

```
cpp
```

