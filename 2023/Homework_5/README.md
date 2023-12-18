# Homework 5 -  The eternal significance of publications and citations!

<p align="center">
<img src="https://filelist.tudelft.nl/Library/Themaportalen/Research%20Analytics/C12.png" width = 800>
</p>

Citation networks, intricately woven through references in scholarly papers, play a pivotal role in mapping the evolution of knowledge in academic research. Analyzing these networks is essential for identifying influential works, tracking idea development, and gauging the impact of research. Leveraging graph analysis enhances our ability to uncover hidden patterns, predict emerging trends, and comprehend the intricate relationships within these networks. 

This time, you and your team have decided to dive deep into the citation realm. Now, you will deal with graphs to determine relevant characteristics and highlights from the relations among those publications.

Let's hands-on this!

# VERY VERY IMPORTANT!

1. **!!! Read the entire homework before coding anything!!!**
2. *My solution is not better than yours, and yours is not better than mine*. In any data analysis task, there **is no** unique way to answer. For this reason, it is crucial (**necessary and mandatory**) that you describe any single decision you take and all your steps.
3. Once solving an exercise, comments about the obtained results are **mandatory**. We are not always explicit about where to focus your comments, but we will always want brief sentences about your discoveries.
4. We encourage using chatGPT (Bard, Bing, or any other Large Language Models (LLM) chatbot tool) as allies to help you solve your homework, and we were hoping you could learn how to use them properly. However, **using such tools when not explicitly allowed will be considered plagiarism and strictly prohibited**. 


In this Homework, you will explore the paper citation universe, exploring relations among multiple academic publications!

* __Backend:__ where you need to develop efficient algorithms that define the *functionalities of the system*
* __Frontend:__ where you provide *visualization for queries entered by the user*

__IMPORTANT:__ To deal with the visualization of graphs, you can freely use libraries such as `networkx` or any other tool you choose. Still, when writing an algorithm, it must be implemented yourself using proper data structures, __without any library that computes some algorithm steps for you__.


## 1. Data 
In this homework, you will work on a dataset that contains information about a group of papers and their citation relationships. You can find and download the dataset [here](https://www.kaggle.com/datasets/mathurinache/citation-network-dataset)

### Graphs setup 
Based on the available data, you will create two graphs to model our relationships as follows: 

1. __Citation graph__: This graph should represent the paper's citation relationships. We want this graph to be unweighted and directed. The citation should represent the citation given from one paper to another. For example, if paper A has cited paper B, we should expect an edge from node A to B.

2. __Collaboration graph__: This graph should represent the collaborations of the paper's authors. This graph should be weighted and undirected. Consider an appropriate weighting scheme for your edges to make your graph weighted.

### Data pre-processing 

The dataset is quite large and may not fit in your memory when you try constructing your graph. So, what is the solution? You should focus your investigation on a subgraph. You can work on the most connected component in the graph. However, you must first construct and analyze the connections to identify the connected components. 

As a result, you will attempt to approximate that most connected component by performing the following steps: 
1. Identify the __top 10,000__ papers with the <ins>highest number of citations</ins>.
2. Then the __nodes__ of your graphs would be as follows:

   __Citation graph__: you can consider each of the papers as your nodes

   __Collaboration graph__: the authors of these papers would be your nodes
    
4. For the __edges__ of the two graphs, you would have the following cases:
   
   __Citation graph__: only consider the citation relationship between these 10,000 papers and ignore the rest.
   
   __Collaboration graph__: only consider the citation relationship between these 10,000 papers and ignore the rest. 


# 2. Controlling system

Please keep the following in mind for both the backend and frontend components. The plan is to put in place a control system. You will provide the user with a menu from which he can select different functionalities. The user should be able to select from one of five different functionalities that you will implement in the following two sections. We want to have such a system so that the user can query different functionalities that he is interested in. 

Your function should be designed in such a way that it provides the most flexibility to the user. For example, when the user selects functionality 1, which provides some high-level information about the graph, you can allow him to pass an argument indicating which of the two types of graphs he wants to be analyzed (That is why the name of the graph is one of the arguments in the first functionality). 

You will implement the functionalities in the Backend section. The Frontend section primarily discusses the menu that you must provide to the user, as well as the expected results that should be displayed to the user after selecting each of the functionalities. 

## 2.1. Backend Implementation
This section describes what each of the functionalities should be. 

### Functionality 1 - Graph's features
This function should examine a graph and report on some of its features. The input and report that this function should produce are shown below. 

Input: 
- The graph
- The name of the graph

Output: 
- The number of the nodes in the graph
- The number of the edges in the graph
- The graph density
- The graph degree distribution
- The average degree of the graph
- The graph hubs (hubs are nodes having degrees more extensive than the 95th percentile of the degree distribution)
- Whether the graph is dense or sparse

### Functionality 2 - Nodes' contribution 
Using this functionality, you will identify the papers/authors who have significantly contributed to this field of study. For this analysis, focusing solely on the number of citations for the paper or the number of collaborations of the authors can be misleading. You will examine this using various centrality measurements. 

Input:
- The graph
- A node of the graph (paper/author)
- The name of the graph

Output: 
- The centrality of the node, calculated based on the following centrality measurements:
   - [Betweeness](https://www.tandfonline.com/doi/abs/10.1080/0022250X.2001.9990249)
   - [PageRank](https://courses.cs.washington.edu/courses/cse373/17au/project3/project3-3.html)
   - [ClosenessCentrality](https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.centrality.closeness_centrality.html#networkx.algorithms.centrality.closeness_centrality)
   - DegreeCentrality
     
### Functionality 3 - Shortest ordered walk  

Input:  
- The graph data 
- A sequence of authors\_a = [a\_2, ..., a\_{n-1}]
- Initial node a\_1 and an end node a\_n
- $N$: denoting the top $N$ authors whose data should be considered
 
Output: 
- The shortest walk of collaborations you need to read to get from author a\_1 to author a\_n and the papers you need to cross to realize this walk.
 
Considerations: 
For this functionality, you must implement an algorithm that returns the shortest __walk__ that goes from node a\_j to a\_n, which visits **in order** the nodes in _a_. The choice of a\_j and a\_n can be made randomly (or if it improves the performance of the algorithm, you can also define it in any other way) 

__Important Notes:__
- This algorithm should be run only on the collaboration graph.
- The algorithm needs to handle the case that the graph is not connected. Thus, only some nodes in _a_ are reachable from a\_1. In such a scenario, it is enough to let the program give in the output the string "There is no such path."
- Since we are dealing with walks, you can pass on the same node _a\_i_ more than once, but you must preserve order. It means you can go back to any author node any time you want, assuming that the order in which you visit the required nodes is still the same.
- Once you completed your implementation, ask chatGPT for a different one leveraging another approach in solving the shortest path and prove whether this implementation is correct. 

### Functionality 4 - Disconnecting Graphs

Input: 
- The graph data 
- authorA: a paper to which will relate sub-graph G\_a
- authorB: a paper to which will relate sub-graph G\_b
- $N$: denoting the top $N$ authors that their data should be considered

Output:
- The minimum number of edges (by considering their weights) required to disconnect the original graph in two disconnected subgraphs: G\_a and G\_b.

### Functionality 5 - Extracting Communities

Input: 
- The graph data 
- $N$: denoting the top $N$ papers that their data should be considered
- Paper\_1: denoting the name of one of the papers 
- Paper\_2: denoting the name of one of the papers

Output:
- The minimum number of edges that should be removed to form communities
- A list of communities, each containing a list of papers that belong to them.
- Whether the Paper\_1 and Paper\_2 belongs to the same community. 

Important Notes:  
To comprehend this functionality better, we suggest you take a good look at this [article](https://www.analyticsvidhya.com/blog/2020/04/community-detection-graphs-networks/)

## 2.2. Frontend Implementation 
This section describes how the final results for each functionality implemented in the backend section should be presented to the user. 

Please run __at least one query for each functionality__ in the final version of the notebook and __comment on the results__. 

### Visualization 1 - Visualize graph features 
We anticipate seeing the Functionality 1 report in Visualization 1. To be more specific, we expect you to have the following report format:

 - A table containing the following general information about the graph: 
      - Number of nodes in the graph
      - Number of the edges in the graph 
      - Density of the graph
      - Average degree of the graph
      - Whether the network is sparse or dense 
 - A table that lists the graph's hubs
 - A plot depicting the distribution of the citations received by papers (Citation graph)
 - A plot depicting the distribution of the given citations by papers (Citation graph) 
 - A plot depicting the number of collaborations of the author (Collaboration graph)

__Note:__ You can plot the features for a limited number of nodes (e.g., top 20) to improve the visualization of the plots. 


 ### Visualization 2 - Visualize the node's contribution
We anticipate seeing the Functionality 2 report in Visualization 2. To be more specific, we expect you to have the following report format:

   - A table containing the node's centrality value based on the four centrality measurements

 ### Visualization 3 - Visualize the shortest-ordered route 
 We anticipate seeing the Functionality 3 report in Visualization 3. To be more specific, we expect you to have the following report format:
 - Print the papers needed to be crossed in the shortest walk in order 
 - Plot the graph and identify the nodes and edges that appear in the shortest walk (please put an identifier on each edge in the shortest walk to determine the order that we should have the walk)
 
 ### Visualization 4 - Visualize the disconnected graph 
 We anticipate seeing the Functionality 4 report in Visualization 4. To be more specific, we expect you to have the following report format:
 - Print the number of the links that should be disconnected 
 - Plot the original graph 
 - Plot the graph after removing the links and identify the two nodes

### Visualization 5 - Visualize the communities
We anticipate seeing the Functionality 5 report in Visualization 5. To be more specific, we expect you to have the following report format:

 - Print the number of links that should be removed to have the communities
 - A table depicting the communities and the papers that belong to each community
 - Plot the original graph 
 - Plot the graph showing the communities in the network 
 - Plot the final graph and identify the community/communities of Paper_1 and Paper_2


## 3. Bonus - PageRank on MapReduce 

__IMPORTANT:__ This is a bonus step, so it's <ins>not mandatory</ins>. You can get the maximum score without doing this. We will consider this, __only if__ the rest of the homework has been completed.

Working with big data has become increasingly important in the modern era as the volume and complexity of data generated grows. In this part, we ask you to __implement the PageRank algorithm using MapReduce paradigm__ to compute the <ins>importance of papers</ins> based on the citation relationship. 

Since a large dataset is required to fully understand the power of this paradigm, when creating the Citation graph, consider the __top 1,000,000 papers__ that have received the most citations; then, make the graph exclusively for those papers. 

__Hint:__ 
[Here](https://www.cs.utah.edu/~jeffp/teaching/cs5140-S15/cs5140/L24-MR+PR.pdf) are __two approaches__ to implement the PageRank algorithm using the MapReduce paradigm that you can use as a reference for your bonus part.


## 4. Command Line Question (CLQ)
In this question, you should use any command line tools that you know to answer the following questions using the **directed** and **unweighted** graph that you have previously created: **Citation graph**: 

1. Is there any node that acts as an important "connector" between the different parts of the graph?
2. How does the degree of citation vary among the graph nodes? 
3. What is the average length of the shortest path among nodes?

__Important note:__ You may work on this question in any environment (AWS, your PC command line, Jupyter notebook, etc.), but the final script must be placed in CommandLine.sh, which must be executable. Please run the script and include a __screenshot__ of the <ins>output</ins> in the notebook for evaluation.  



## 5. Algorithmic Questions (AQ)

### Part A
A sports club hires you to create a team for the National Sports Championship. Every Italian Region sends its best $M$ athletes to compete in an intense 2-day sports event, and Rome is no exception!

The trainers of Team Rome need to carefully choose the best $M$ athletes from a pool of $N$ candidates. Each athlete is uniquely identified by a number from 1 to $N$ and possesses a set of $S$ sports skills. Each skill is represented by a 3-character string with only uppercase letters and a non-negative integer indicating the athlete's proficiency in that skill (always greater than 0).

The trainers have extensively studied the competition format and established an optimal set of (possibly repeated) skills the team should possess to ensure the best possible performance. Each of the ten selected athletes will be assigned one of these skills as their role within the team.

The team's overall score is the sum of the skill scores of its members in the roles they have been assigned. Other skills of each athlete do not contribute to the team's score.

Your task is to determine the maximum possible global score for Team Rome, given the list of candidates.

Note: Assigning an athlete to a role not listed in their skills is possible. In that case, that athlete's contribution to the global score will be 0.

__Input__
The input consists of $2 + N(S + 1)$ lines:
- Line 1: the numbers $N, M,$ and $S$, separated by a space.
- Line 2: the optimal set of skills required by the trainers, as a list of $M$ space-separated skill names.
- Lines 3, . . . , $N(S + 1) + 2$: every group of $S + 1$ lines is formatted as follows:
  - Line 1: the unique id of the athlete.
  - Lines 2, . . . , $S + 1$: one skill name and the corresponding skill score, separated by a space.

__Output__
Print the maximum global score that can be achieved with the available athletes.

__Input 1__
```
14 10 1 # N, M, S
SWM VOL ATH VOL VOL BSK HCK BSK SWM BSK #set of skills
1
BSK 98
2
ATH 14
3
HCK 82
4
HCK 9
5
FTB 90
6
ATH 52
7
HCK 95
8
TEN 85
9
RGB 46
10
SWM 16
11
VOL 32
12
SOC 41
13
SWM 59
14
SWM 34
```
__Output 1__
```
370
```
---
__Input 2__
```
14 10 1 # N, M, S
SWM VOL ATH VOL VOL BSK HCK BSK SWM BSK #set of skills
1
BSK 98
HCK 12
2
ATH 14
VOL 1
3
HCK 82
ATH 30
4
HCK 9
SWM 27
5
FTB 90
HCK 50
6
ATH 52
RGB 80
7
HCK 95
SWM 11
8
TEN 85
RGB 7
9
RGB 46
SWM 30
10
SWM 16
BSK 12
11
VOL 32
HCK 40
12
SOC 41
FTB 12
13
SWM 59
TEN 82
14
SWM 34
VOL 20
```
__Output 2__
```
399
```
__Your job__:
1. Implement an algorithm to solve the described mentioned problem. 

2. What is the __time complexity__ (the Big O notation) of your solution? Please provide a <ins>detailed explanation</ins> of how you calculated the time complexity.

3. Ask ChatGPT or any other LLM chatbot tool to check your code's time complexity (the Big O notation). Compare your answer to theirs. If the <ins>two differ</ins>, which one is right? (why?)
   
4. If you algorithm has exponential time complexity, can you provide a __polynomial-time version__? 

5. If $S=1$, how does the __time complexity__ of an optimal algorithm to solve this problem change?

### Part B

We will add another part of this exercise in the upcoming days. We will keep you posted.
