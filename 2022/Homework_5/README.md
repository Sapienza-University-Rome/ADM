# Homework 5 - The Marvel Universe! 

<p align="center">
<img src="https://dunesjedi.files.wordpress.com/2018/10/marvel-banner.png" width = 800>
</p>

Superheroes and abilities have always existed in the human imagination. Marvel has one of the largest superhero comic book franchises. Famous superheroes, including Spider-Man, Iron Man, Captain America, and Thor, are among its cast, as are well-known superhero teams like the Avengers, X-Men, Fantastic Four, and Guardians of the Galaxy. Additionally, it has famous supervillains, including Doctor Doom, Magneto, Ultron, and Thanos, in its stable. Most of Marvel's fictional characters function in a single reality known as the Marvel Universe, with many of their headquarters located in New York City. These comics are well-known today because of their use in movies. If you do not know who we are talking about, [give this link a look](https://www.marvel.com/explore) and learn more about the characters.

This time, you and your team have decided to dive deep into Marvel's social network. Now, you will deal with graphs to determine relevant characteristics and highlights from the relations among those superheroes.

Let's hands-on this!

# VERY VERY IMPORTANT!

1. !!! Read the entire homework before coding anything!!!

2. My solution it's not better than yours, and yours is not better than mine. In any data analysis task, there is not a unique way to solve a problem. For this reason, it is crucial (necessary and mandatory) that you describe any single decision you take and all the steps you do.

3. Once performed any exercise, comments about the obtained results are mandatory. We are not always explicit about where to focus your comments, but we will always want brief sentences about your discoveries and decisions.

In this Homework, you will explore the Marvel Comics Universe, exploring relations between heroes and villains in the comics!

* __Backend:__ where you need to develop efficient algorithms that define the *functionalities of the system*
* __Frontend:__ where you provide *visualization for queries entered by the user*

__IMPORTANT:__ The **main functions** for each functionality should be written from scratch in the backend part. Nevertheless, you can use the data structures provided by networkx (such as closeness_centrality, betweenness_centrality, pagerank, or any other function that can help you as an intermediate step for your main functionalities).


In the visualization part, you can use any available function (networkx functions are highly recommended).

## 1. Data

To get started, you have to download the data, as always, from [here](https://www.kaggle.com/datasets/csanhueza/the-marvel-universe-social-network?select=hero-network.csv). Make sure you downloaded all files because we will work with them all.

In particular, the files contain the following:  
- __nodes.csv__ - Contains two columns (node, type), indicating the nodes' name and type (comic, hero).
- __edges.csv__ - Contains two columns (hero, comic), indicating which comics the heroes appear in.
- __hero-network.csv__ - Contains the network of heroes who have appeared together in the comics.

### Graphs setup

For this homework, we are going to build two different graphs:  

1. __First graph__: Will be constructed using the data stored in the __'hero-network.csv'__ file, in which an edge between two heroes can be found if they have appeared in the <ins> same comic together</ins>. The <ins>number of edges</ins> between two heroes represents the <ins>number of times they have collaborated</ins> in different comics. The graph should be considered __weighted__ and __undirected__. It is up to you to decide which metric to use to calculate the weights, but we anticipate that the cost will be __lower__ for heroes with __more collaborations__. Please specify which metric you used to select the weights in the report.

2. __Second graph__: The data in 'nodes.csv' and 'edges.csv' will be used to construct the second graph. The type of node (hero/comic) can be found in __'nodes.csv'__, and an edge between a hero node and a comic node can be found in __'edges.csv'__ when the <ins>hero has appeared in that specific comic</ins>. This graph is assumed to be __undirected__ and __unweighted__.

### Data Preprocessing

As always, in the data science area, you can find some inconsistencies in the provided data. Therefore, some modifications should be made to the data to make it consistent across all of the datasets you have. To ensure consistency in the data, keep the following in mind:

1. Some of the heroes' names in 'hero-network.csv' are not found in 'edges.csv'. This inconsistency exists for the following reasons:
   
   - Some heroes' names in 'hero-netowrk.csv' have __extra spaces__ at the end of their names compared to their names in 'edges.csv'.
   - Some heroes' names in 'hero-netowrk.csv' have an __extra '/'__ at the end of their names compared to their names in 'edges.csv'.
   - The hero name __'SPIDER-MAN/PETER PARKER'__ in 'edges.csv' has been changed to __'SPIDER-MAN/PETER PAR'__ in 'hero-network.csv' due to a string length limit in 'hero-network.csv'.
 
2. Some entries in the 'hero-network.csv' have the same hero in <ins>both columns</ins>. In the graph, these entries form a __self-loop__. Because a self-loop makes no sense in this network, you can safely remove those from the dataset.
  
## 2. Backend Implementation

The goal of this part is the implementation of a controller system that has different functionalities. 
The controller should take as input an identifier "i" and run the associated function_i applied to the graph you create from the downloaded data. 

__Definition__: As the number of nodes and edges grows, we may request to work on a subset of the data to <ins>reduce computation time</ins> and <ins>improve network visualization</ins>. In this case, we will ask you only to consider the data for __top N heros__. We define the top N heroes as follows: 
- __Top N heroes__: The __top N heroes who have appeared in the most number of comics__. The 'edges.csv' file, which represents the comics in which each hero has appeared, can be used to filter these N heroes.

__Note__: When the value of __N__ is <ins>not set</ins> by the user, the function should consider <ins>the whole data</ins>. 

### Functionality 1 - extract the graph's features

Input:  
- The graph data 
- The graph type (ex., number 1 or number 2)
- N: denoting the top N heroes that their data should be considered

Output:  
- The number of nodes in the network (if type 2, report for both node types)
- The number of collaborations of each superhero with the others (<ins>only if type 1</ins>)
- The number of heroes that have appeared in each comic (<ins>only if type 2</ins>)
- The network's density
- The network's degree distribution
- The average degree of the network
- The network's Hubs (hubs are nodes having degrees more extensive than the 95th percentile of the degree distribution)
- Whether the Network is sparse or dense

__Note__: For this case, it makes sense to differentiate operations between the two graphs: for example, when computing hubs for the second graph, we likely care only about comics. 

### Functionality 2 - Find top superheroes!  

Input:  
- The graph data 
- A node (hero or comic)
- One of the given metrics : _Betweeness_ [1](https://www.tandfonline.com/doi/abs/10.1080/0022250X.2001.9990249), _PageRank_, _ClosenessCentrality_ [3](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.centrality.closeness_centrality.html#networkx.algorithms.centrality.closeness_centrality), _DegreeCentrality_
- N: denoting the top N heroes that their data should be considered

Output:  
- The metric's value over the considered graph
- The given node's value 

__Note__: Give an explanation regarding the features of the user based on all of the metrics (e.g. if the betweenness metric is high, what does this mean in practice, what if the betweenness is low but has a high PageRank value, etc.).

### Functionality 3 - Shortest ordered Route  

Input:  
- The graph data 
- A sequence of superheroes _h = [h\_2, ..., h\_n-1]_
- Initial node h_1 and an end node h_n
- N: denoting the top N heroes that their data should be considered
 
Output: 
- The shortest walk of comics that you need to read to get from hero_1 to hero_n
 
Considerations: 
For this functionality, you need to implement an algorithm that returns the shortest __walk__ that goes from node h\_j to _h\_n_, which visits **in order** the nodes in _h_. The choice of h\_j and h\_n can be made randomly (or if it improves the performance of the algorithm, you can also define it in any other way) 

__Important Notes:__
- This algorithm should be run only on the second graph.
- The algorithm needs to handle the case that the graph is not connected. Thus, only some of the nodes in _h_ are reachable from h_1. In such a scenario, it is enough to let the program give in the output the string "There is no such path".
- Since we are dealing with walks, you can pass on the same node _h\_i_ more than once, but you have to preserve order. E.g., if you start from __Spiderman__ to reach __deadpool__, and your path requires you to visit __iron-man__ and __colossus__, you can go back to any comics any time you want, assuming that the order in which you visit the heroes is still the same. 

### Functionality 4 - Disconnecting Graphs

Input: 
- The graph data 
- heroA: a superhero to which will relate sub-graph G_a
- heroB: a superhero to which will relate sub-graph G_b
- N: denoting the top N heroes that their data should be considered

Output:
- The minimum number of links (by considering their weights) required to disconnect the original graph in two disconnected subgraphs: G_a and G_b.
 
### Functionality 5 - Extracting Communities

Input: 
- The graph data 
- N: denoting the top N heroes that their data should be considered
- Hero_1: denoting the name of one of the heroes 
- Hero_2: denoting the name of one of the heroes

Output:
- The minimum number of edges that should be removed to form communities
- A list of communities, each containing a list of heroes that belong to them.
- If the Hero_1 and Hero_2 belongs to the same community 

Important Notes:  
This functionality should only be run on the first graph.  
To comprehend this functionality better, we suggest you take a good look at this [article](https://www.analyticsvidhya.com/blog/2020/04/community-detection-graphs-networks/)

## 3. Frontend Implementation 
In this section, we ask you to build the visualizations for users' query results. We also expect you to showcase plots that can give us the most insight possible and comment accordingly.

### Visualization 1 - Visualize some features of the network
We anticipate seeing the Functionality 1 report in Visualization 1. To be more specific, we expect you to have the following report format:
 - A table containing the following general information about the graph: 
      - Number of nodes in the network
      - Density of the network 
      - Average degree of the network 
      - Whether the network is sparse or dense 
 - A table that lists the network's hubs
 - A plot depicting the number of collaborations of each hero in descending order (if the graph is type 1) 
 - A plot depicting the number of heroes who appeared in each comic, sorted in descending order (if the graph is type 2)
 - A plot depicting the degree distribution of the network
 
 - __Note__: You can do the plot on a limited number of heroes/comic books to have a better visualization for the charts that ask for some insights about all of the comics/heroes (e.g. for the first 50)
 
 ### Visualization 2 - Visualize centrality measure 
 We anticipate seeing the Functionality 2 report in Visualization 2. To be more specific, we expect you to have the following report format:
 - A table containing the information related to the requested centrality measure for: 
      - The average of the requested centrality measure for all of the network's nodes
      - The requested centrality measure's value for the given node
      
 ### Visualization 3 - Visualize the shortest-ordered route 
 We anticipate seeing the Functionality 3 report in Visualization 3. To be more specific, we expect you to have the following report format:
 - Print the comics in the shortest walk in order 
 - Plot the graph and identify the nodes and edges that appear in the shortest walk (please put an identifier on each edge in the shortest walk to determine the order that we should have the walk)
 
 ### Visualization 4 - Visualize the disconnected graph 
 We anticipate seeing the Functionality 4 report in Visualization 4. To be more specific, we expect you to have the following report format:
 - Print the number of the links that should be disconnected 
 - Plot the original graph 
 - Plot the graph after removing the links and identify the two nodes 

 ### Visualization 5 - Visualize the communities
 We anticipate seeing the Functionality 5 report in Visualization 5. To be more specific, we expect you to have the following report format:
 - Print the number of links that should be removed to have the communities
 - A table depicting the communities and the heroes that belong to each community
 - Plot the original graph 
 - Plot the graph showing the communities in the network 
 - Plot the final graph and identify the community/communities of Hero_1 and Hero_2

__Notes:__ 
   - For the final output of your function, please set the __Hero_1 to <ins>'Captain America'</ins>__ and __Hero_2 to <ins>'Ironman'</ins>__ and show the results
   - If Hero_1 and Hero_2 belong to the same community, identify that community; otherwise, identify those two communities that these heroes belong to.

## 4. Command Line Question
In this question, you should use any command line tools that you know to answer the following questions using the same datasets that you have been using so far: 

1. What is the most popular pair of heroes (often appearing together in the comics)?
2. Number of comics per hero.
3. The average number of heroes in comics.

__Note:__ You may work on this question in any environment (AWS, your PC command line, Jupyter notebook, etc.), but the final script must be placed in CommandLine.sh, which must be executable.

## 5. Bonus - PageRank on MapReduce 
__IMPORTANT:__ This is a bonus step, so it's <ins>not mandatory</ins>. You can get the maximum score also without doing this. We will take this into account, __only if__ the rest of the homework has been completed.

1. PageRank and MapReduce go well together, and this synergy was essential for Google's growth and the MapReduce paradigm's proliferation. Therefore, for the bonus section of this homework, we ask that you __implement the PageRank algorithm using the MapReduce paradigm__.

__Hint:__ 
[Here](https://www.cs.utah.edu/~jeffp/teaching/cs5140-S15/cs5140/L24-MR+PR.pdf) are __two approaches__ to implementing the PageRank algorithm using the MapReduce paradigm that you can use as a reference for your bonus part.

## 6. Algorithmic Question

Alex and Sarah have been together for two years, and Alex is now thinking about proposing to her. But, to surprise her, he wants to install an app on her phone that asks her if she will marry him at the right time.

However, to install the application secretly, he needs her phone's password, which he does not have. He knows her password is __a poly-line made up of vertical or horizontal line segments__. In a __3*3__ grid, each line segment connects the centres of __two cells__. Alex learned the <ins>direction of each line segment</ins>  by looking at her hand while unlocking her phone. He didn't pay much attention to the length of each line segment, but he is sure that her phone's operating system __does not allow__ the poly-line __to intersect with itself even at one point__.

Alex wants to distract Sarah's attention long enough to test all possible patterns based on the directions of the line segments he has learned. Therefore, he needs you to assist him in calculating <ins>how many possible patterns</ins> he has to try based on those directions to estimate how much time he needs to check all of those possibilities. Given that the line segments were directed right, down, left, and up, the following figure depicts __two valid__ and __one invalid__ (as the poly-lines should <ins>not intersect</ins> even in one point) patterns.

<p align=center>
<img src="https://github.com/lucamaiano/ADM-TA/blob/master/2022/Homework_5/img/Examples.png">
</p>

**Input:**

The input is a __single string__ that shows the direction of the segment lines and contains only the characters R, L, U, and D, which correspond to the Right, Left, Up, and Down directions. The string's <ins>maximum length</ins> is __10__. It is also guaranteed that <ins>two consecutive characters will be different</ins>.

**Ouput:**

We expect to see only __1 number__ in the output, corresponding to the <ins>number of different patterns</ins> that can be generated based on the line segments Alex learned. In some cases, this number __may be 0__, indicating that no patterns can be generated using the learned line segments.

**Examples:**

__Input 1__
```
DRU
```
__Output 1__
```
15
```
___
__Input 2__
```
R
```
__Output 2__
```
9
```
___
__Input 3__
```
LDRDRUL
```
__Output 3__
```
0
```

