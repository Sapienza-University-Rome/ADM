# Homework 5 - Exploring StackOverflow!

![Alt Text](https://www.linuxadictos.com/wp-content/uploads/stack-overflow-1024x244.jpg.webp)

# VERY VERY IMPORTANT!

1. !!! Read the entire homework before coding anything!!!

2. My solution it's not better than yours, and yours is not better than mine. In any data analysis task, there is not a unique way to solve a problem. For this reason, it is crucial (necessary and mandatory) that you describe any single decision you take and all the steps you do.

3. Once performed any exercise, comments about the obtained results are mandatory. We are not always explicit about where to focus your comments, but we will always want some brief sentences about your discoveries and decisions.


In this homework, you will build a system that provides users with information about our beloved *StackOverflow*. Specifically, the implementation of the system consists of two parts. 

* __Backend:__ where you need to develop efficient algorithms that define the *functionalities of the system*
* __Frontend:__ where you provide *visualization for queries entered by the user*

__IMPORTANT:__ In order to deal with visualization of graphs you can freely use libraries such as `networkx` or any other tool you choose, but when you are writing algorithm, they have to be implemented by yourself using proper data structures, __without any library that computes some steps of the algorithm for you__.


## 1. Data

The first step, as always, is to download the data you will be working on. You can download the data to build the system [here](https://snap.stanford.edu/data/sx-stackoverflow.html). Please download the **3 files** which can be found under the description ['Answers to questions', 'Comments to questions', 'Comments to answers']
  
  In particular, each file will contain the following information:
  * __Answers to questions__ - User u answered user v's question at time t
  * __Comments to questions__ - User u commented on user v's question at time t
  * __Comments to answers__  - User u commented on user v's answer at time t

Unless specified differently we will handle the 3 graphs together, therefore as a first step please think about a nice and appropriate manner to merge them. You are free to merge them as you prefer, but we do expect the output graph to be a weighted gragh. For instance, imagine you have a user X has answered to a question and comment from user Y. In the combined graph we expect you to have a weighted link between these two users. How you construct this weight is fully up to you :). If the algorithm we request you does not have a weighted variant please mention it clearly and convert the weighted graph into an unweighted one.

Some recommendations that might be helpful for dealing with the data is:

 - The date is provided with a very high precision, please round it to a reasonable value (e.g. day, hours, etc. whatever you feel makes more sense)
 - You might also see that there are several answers/comments which the user answer do to themselves... please deal with these accordingly and explain what you have decided to do. 
 - We are aware that the data is a lot. For this reason we typically ask you to only focus on a smaller intrerval of time. Please test all your implementations on a sufficiently large interval of time, and use this in your benefit to get the best possible results. 

## 2. Implementation of the backend

The goal of this part is the implementation of a unique system that has ... different functionalities. The program takes in input always a number _i_ in [1,...]: given the input, the program has to run Functionality _i_,  applied to the graph you create from the downloaded data. 

 ### Functionality 1 - Get the overall features of the graph

 It takes in input:
 
 - One of the 3 graphs
    
 The output should return:

 - Whether the graph is directed or not
 - Number of users
 - Number of answers/comments
 - Average number of links per user
 - Density degree of the graph
 - Whether the graph is sparse or dense

 ### <i> Functionality 2 - Find the best users! </i>

 It takes in input:
 
 - A user/node
 - An interval of time
 - One of the following metrics: _Betweeness_ [1](https://www.tandfonline.com/doi/abs/10.1080/0022250X.2001.9990249), _PageRank_, _ClosenessCentrality_ [3](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.centrality.closeness_centrality.html#networkx.algorithms.centrality.closeness_centrality), _DegreeCentrality_

 The output should return:

 - The value of the given metric applied over the complete graph for the given interval of time

Give an explanaition regarding the features of the user based on all of the metrics (e.g. if the betweeness metric is high, what does this mean in practice, what if the betweeness is low but it has a high PageRank value, etc.)

 ### <i> Functionality 3  - Shortest Ordered Route </i>
 
  It takes in input:
 
 - An interval of time
 - A sequence of users _p = [p\_2, ..., p\_n-1]_
 - Initial user p_1 and an end user p_n

Implement an algorithm that returns the shortest __walk__ that goes from user p\_j to _p\_n_, and that visits **in order** the nodes in _p_. The choice of p\_j and p\_n can be done randomly (or if it improves the performance of the algorithm you can also define it in any other way) 

Consider that:
- The algorithm needs to handle the case that the graph is not connected, thus not all the nodes in _p_ are reachable from p_1. In such scenario, it is enough to let the program give in output the string "Not possible".
- That the graph is weighted
- Since we are dealing with walks, you can pass more than once on the same node _p\_i_, but you have to preserve order. E.g.: if you pass through _p\_2_ and you are going to _p\_3_, you can pass through _p\_10_, but once you will be in _p\_9_, you will have to go back to _p\_10_ as well.

 ### <i> Functionality 4 - Disconnecting graphs </i>
   
   It takes in input:
 
 - Two different intervals of time (disjoint or not), which will lead to two different graphs, _G\_1_ (associated to interval 1) and _G\_2_ (associated to interval 2) 
 - Two users which are unique to each interval of time (_user\_1_ only appears in interval 1, while _user\_2_ only appears in interval 2)
 
 The function should return the minimum number of links (considering their weights) required to disconnect the two users.

## 3. Implementation of the frontend

In this section, we ask you to build the visualizations for users’ queries results. We also expect you to showcase plots which can give us the most insight as possible and comment them accordingly.

 ### <i> Visualization 1 - Visualize the overall features of the graph </i>
 
 Output a table with all of the information requested. The visualization should also generate a plot of the density distribution of the graph provided as input. 

 ### <i> Visualization 2  - Visualize the best user! </i>
 
 Plot the input node and a subset of its neighbouring nodes such that the user can get a grasp of the importance of this input node. Also split the interval of time into equidistant ranges of time and show the metric evolution over time.

 ### <i> Visualization 3 - Visualize the Shortest Ordered Route </i>

 Once the user runs Functionality 3, we want the system to show in output the Shortest Ordered Route.

 ### <i> Visualization 4 - Visualize disconnecting graphs </i>
 
Show a visualization of the links needed to be removed in order to disconnect both graphs.

For each of the visualization, you can add more 'fancy' stuff. Therefore, you can go deeper, adding more features, and making the visualization even more detailed! But, the important thing is that there are **at least the requested features**.

**Good luck!** 


# 4. Algorithmic question 

A number ***n*** of kids are in a camp. Between some ***k*** pairs of them (a kid can be part of more than one pairs) there are often fights. At night there are two dormitories where the kids can sleep. We want, if possible, to assign each kid in one of the two dormitories in such a way that each pair of kids that fights often is assigned to a different dormitory. (There are no space problems and the two dormitories can have different number of kids.)

Give an algorithm that is linear in ***n*** and ***k*** that is able to answer whether such an assignment is possible and, if so, return one.
