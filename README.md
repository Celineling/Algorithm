## How to edit github readme/排版教程
https://blog.csdn.net/u012067966/article/details/50736647

Algorithm learning notes
===
Data structure and problems in LeetCode using Python3
-----
## 1. binary Search
### 1.1 Leetcode34. Find First and Last Position of Element in Sorted Array
#### 参考思路
https://blog.csdn.net/qq508618087/article/details/50448481

## 6. Dynamic programing
### 6.1 概念和思路认识：
https://www.zhihu.com/question/23995189
### 6.2 DP problems with comments:
https://github.com/Celineling/Algorithm/blob/master/6.%20Dynamic%20Programming.ipynb

## 7. Topological Sort
### 7.1 概念
>7.1.1 A topological ordering is an ordering of the nodes in a directed graph where for each directed edge form node A to node B, node A appears before node B in the ordering.<br> 

>7.1.2 Time complexity: O(V+E) <br> 

>7.1.3 The only type of graph which has a valid topological ordering is a Directed Acyclic Graph (DAG). There are graphs with directed edges and no cycles.<br> 
### 7.2 How to verify that my graph does not contain a directed cycle?
>7.2.1 One method is : Tarjan's strongly connected component algorithm Which can be used to find these cycles.<br>

>7.2.2 Every tree has a topological ordering, since, by definition, they do not contain any cycles.(checking from bottum)<br>

### 7.3 Topological sort algorithm
#### 7.3.1 Steps:
>Pick an unvisited node randomly, push in stack <br>

>Beginning with the selected node, do a DFS exploring only unvisited nodes, till the node has no path to go(outdegree is 0), then call the dfs back.<br>

>On the recursive callback of the dfs, pop the current node from stack and add it to the topological ordering in reverse order list.<br>
#### 7.3.2 Pseudocode in python:
```python3
#Assumption: graph is store as adjacency list
def function topsort(graph):
  N = graph.numberofNodes()
  V = [False for i in range(N)] # unvisited
  ordering = [0 for i in range(N)] #result returned from the function, top-ordering
  i=N-1 #index for ordering array, trace the insertion position of the next elem in the top-ordering, backward
  
  for at in range(N):
    if V[at]==False:
      visitedNodes=[] #initialize the unvisited node for dfs
      dfs(at, V, visitedNodes, graph)
      for nodeId in visitedNodes:
        ordering[i] = nodeId
        i -=1
  return ordering
  
 #Execute DFS
 def function dfs(at, V, visitedNodes, graph):
  V[at] = True
  edges = graph.getEdgesOutFromNode(at)
  for edge in edges:
    if V[edge.to] == False: # unvisited node
      dfs(edge.to, V, visitedNodes, graph)
  
  #the end of the for loop, the at index pointing node which has no edge to go
  visitedNodes.add(at)  
```
Optimization according to the space and time:
>Delete the visitedNodes, which store the visitedNodes temporarily
```python3
#Assumption: graph is store as adjacency list
def function topsort(graph):
  N = graph.numberofNodes()
  V = [False for i in range(N)] 
  ordering = [0 for i in range(N)] 
  i=N-1 
  
  for at in range(N):
    if V[at]==False:
      i = dfs(i, at, V, ordering, graph)

  return ordering
  
 #Execute DFS
 def function dfs(i, at, V, ordering, graph):
  V[at] = True
  edges = graph.getEdgesOutFromNode(at)
  for edge in edges:
    if V[edge.to] == False: # unvisited node
      dfs(i, edge.to, V, ordering, graph)
  
  #at the end of the for loop, at pointing the node which has no path to go
  ordering[i] = at #pass the node's id to ordering
  return i-1  
```

#### 7.3.3 Lahn's algorithm

while S is non-empty do:<br>
  remove node V from S <br>
  add v to tail of L <br>
  for each node W with an edge e form v to w do:<br>
    remove edge e from the graph<br>
    if w has `no other incoming edges`: #indegree is 0<br>
      add w into S
      
      
### 7.4 Practices problems
