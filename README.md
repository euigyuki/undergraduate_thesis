# undergraduate_thesis

# Di An's Final Report

## Team Member : Di An ( USC ID : 8566513464 )


## Content

1.  Autocomplete the location name
2.  Find the place's Coordinates in the Map
3.  CalculateShortestPath between two places
4.  The Traveling Trojan Problem
5.  Cycle Detection
6.  Topological Sort
7.  Find K closest points
8.  Learinig Experience


## TrojanMap

This project focuses on using data structures in C++ and implementing various graph algorithms to build a map application.


- Please clone the repository, look through [README.md](README.md) and fill up functions to finish in the project.
- Please make sure that your code can run `bazel run/test`.
- In this project, you will need to fill up [trojanmap.cc](src/lib/trojanmap.cc) and add unit tests in the `tests` directory.

---

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



```shell
2
**************************************************************
* 2. Find the position                                        
**************************************************************

Please input a location:66
-1-1
*************************Results******************************
No matched locations.
**************************************************************
Time taken by function: 838 microseconds
```

From the result we can also see that the time complexity is O(n).







### 4.3 3-opt
Similar to 2-opt, this is how the 3-opt works:

In the 3-opt, instead of choosing part of the path, I choose 2 parts of the path, and do the 2-opt seperately, and I keep doing this until there is no improvement can be made. This 2 algotithms' core ideas are all the same.
```cpp
while(true){
    double delta = 0;
    for(auto it: combinations){
      delta += reverse_segment_if_better(path2, it[0], it[1], it[2], results);
    }

    if(delta >= 0){
      break;
    }
  }
```
And below is how I reverse the path
```cpp
double d0 = CalculateDistance(a,b) + CalculateDistance(c,d) + CalculateDistance(e,f);
double d1 = CalculateDistance(a,c) + CalculateDistance(b,d) + CalculateDistance(e,f);
double d2 = CalculateDistance(a,b) + CalculateDistance(c,e) + CalculateDistance(d,f);
double d3 = CalculateDistance(a,d) + CalculateDistance(e,b) + CalculateDistance(c,f);
double d4 = CalculateDistance(f,b) + CalculateDistance(c,d) + CalculateDistance(e,a);
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




These lines are very important for reading csv files. As we all know, csv file is one kind of excel file, using "," to seperate each column. \
And after reading all the dependencies and location_names, we can work on our algorithm. \
Here I given each location with a indegree number. I calculate the indegree number using the dependecies vector. Each time a pointer is pointing to the location name, its indegree wii increase by one.\
And once we have finish initalizing the indegree counting. What we need to do is keep pushing the location into the results while it's indegree equal to "0", and each time we push the location in, we need to update the indgree for each location. And we keep doing that until the result size reaches to the location name size.

```cpp
while(result.size() < locations.size()){

    std::cout<<"current count "<<count<<std::endl;

    for(auto it : indegree){
      if(it.second == 0 and std::find(result.begin(), result.end(), it.first) == result.end()){
        std::cout<<"current "<<it.first<<"  with indegree "<<count<<"  it pushed in"<<std::endl;
        result.push_back(it.first);

        //make the current id's neighbor indegree - 1;
        for(auto i : dependencies){
          if(i[0] == it.first){

            for(int j = 1; j < i.size(); j++){
              indegree[i[j]] -= 1;
            }

          }
        }


      }
    }
```
Besides get the correct order, another thing we need to make sure is that once there is a loop inside, there is no feasible answer for that.\
How I achieve that is making a counter inside, once I push a location name in, I reset the counter, once the counter exceed the threshold, I believe there is a cycle inside.

### 6.2 Results
Here I ues the example given from the csv files to prove that it can work in reading the csv file.
```cpp
Please input the locations filename:/Users/kk9912/Desktop/github/EE538FINAL/final-project-Mightyall/input/topologicalsort_locations.csv
Please input the dependencies filename:/Users/kk9912/Desktop/github/EE538FINAL/final-project-Mightyall/input/topologicalsort_dependencies.csv*************************Results******************************
Topological Sorting Results:
Cardinal Gardens
Coffee Bean1
CVS
**************************************************************
Time taken by function: 67246 microseconds

```

Secondly, I enlarge the dependency tree and to test the algothrim.
```cpp
location_names = {"Cardinal Gardens", "Coffee Bean1","CVS", "Tap Two Blue", "Target", "Ralphs", "ChickfilA"};
dependencies = {{"Cardinal Gardens", "Coffee Bean1"}, {"Cardinal Gardens", "CVS"}, {"Coffee Bean1", "CVS"},  {"Coffee Bean1", "Ralphs"},
      {"Tap Two Blue", "CVS"}, {"Tap Two Blue", "Target"}, {"Target", "ChickfilA"}, {"ChickfilA", "CVS"}};
      *************************Results******************************
Topological Sorting Results:
Cardinal Gardens
Coffee Bean1
Ralphs
Tap Two Blue
Target
ChickfilA
CVS
**************************************************************
Time taken by function: 135780 microseconds
```

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
```c++
std::vector<std::string> FindKClosestPoints(std::string name, int k);
```
This one is very easy, it's a test of the priority queue's implementation. \
Fisrt we need to get the name list, still like before, we just travel all the nodes. \
Then we create a priority queuewith with length k to store the k results. Then one by one we push the location into the results before the queue is full\
After the queue is full, by the time we need to push an element, we needto compare it with the top of the queue since it's a priority queue, the top is the max.
```cpp
else if(ans.size() == k){
      if(ans.top().first > tempDist){
        // pop the first ele in queue and push the new result
        ans.pop();
        ans.push(temp);
      }
    }
```

### 7.2 Result

```cpp
Please input the locations:Ralphs
Please input k:6

Find K Closest Points Results:
1 St Agnes Church
2 Saint Agnes Elementary School
3 Warning Skate Shop
4 Menlo AvenueWest Twentyninth Street Historic District
5 Vermont Elementary School
6 MC39s Barber Shop
**************************************************************
Time taken by function: 6451 microseconds
```

```cpp
Please input the locations:Ralphs
Please input k:7

*************************Results******************************
Find K Closest Points Results:
1 St Agnes Church
2 Saint Agnes Elementary School
3 Warning Skate Shop
4 Menlo AvenueWest Twentyninth Street Historic District
5 Vermont Elementary School
6 MC39s Barber Shop
7 Anna39s Store
```

```cpp
Please input the locations:Ralphs
Please input k:8

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
**************************************************************
Time taken by function: 6178 microseconds
```

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


```cpp
Please input the locations:Ralphs
Please input k:10

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
10 Vermont 38 29th Metro 204 Northbound
**************************************************************
Time taken by function: 6866 microseconds
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

