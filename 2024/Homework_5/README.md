# Homework 5 - USA Airport Flight Analysis 

<p align="center">
  <img src="https://gtm-24.de/wp-content/uploads/2019/11/GTM-24-55.jpg">
</p>


Air travel connects cities across the United States, forming a dense and dynamic network of routes that play a critical role in transportation, commerce, and connectivity. In this assignment, you will analyze the USA Airport Dataset, which includes detailed information about airports, routes, and traffic patterns. Your task is to uncover meaningful insights such as identifying the busiest hubs, analyzing flight routes. Additionally, you will explore the network structure to detect communities of interconnected airports, evaluate their centrality, and assess the impact of disruptions. This analysis will require the application of data visualization, network analysis, and optimization techniques to deliver actionable findings.

---

## VERY IMPORTANT

1. **!!! Read the entire homework before coding anything!!!**
2. *My solution is not better than yours, and yours is not better than mine*. In any data analysis task, there **is no** unique way to answer. For this reason, it is crucial (**necessary and mandatory**) that you describe every decision you make and all your steps.
3. Once solving an exercise, comments about the obtained results are **mandatory**. We are not always explicit about where to focus your comments, but we will always want brief sentences about your discoveries.
4. We encourage using chatGPT (Claude AI, Gemini, Perplexity, or any other Large Language Models (LLM) chatbot tool) to help you solve your homework, but we expect you to learn how to use them responsibly. **Using such tools when not explicitly allowed will be considered plagiarism and strictly prohibited**.

Now that it is all well settled, let's get on with it!

---

## 1. Flight Network Analysis (Q1)

The dataset contains information about flights between airports in the United States. You can download and explore the dataset [here](https://www.kaggle.com/datasets/flashgordon/usa-airport-dataset). In this task, you will analyze the basic features of the flight network graph, such as its size, density, and degree distribution.

---

### **Your Task:**

1. Implement a function `analyze_graph_features(flight_network)` that takes the flight network as input and computes the following:
    - Count the number of airports (nodes) and flights (edges) in the graph.
    - Compute the density of the graph using the formula:  $Density = \frac{2 \cdot E}{N \cdot (N - 1)}$
    - Calculate both in-degree and out-degree for each airport and visualize them using histograms.
    - Identify airports with degrees higher than the 90th percentile and list them as "hubs."
    - Determine if the graph is sparse or dense based on its density.

2. Write a function `summarize_graph_features(flight_network)` that generates a detailed report of the graph's features. A summary report needs to include:
    - The number of nodes and edges.
    - The graph density.
    - Degree distribution plots for in-degree and out-degree.
    - A table of identified hubs.

3. Now let's dive deeper into the analysis of the dataset. Do the following:
    - Compute total passenger flow between origin and destination cities.
    - Identify and visualize the busiest routes by passenger traffic.
    - Calculate the average passengers per flight for each route and highlight under/over-utilized connections.
    - Create an interactive map visualizing the geographic spread of the flight network.


### **Expected Output:**

Once you have created and tested the previous functions, the results should be presented in a tidy way. Your summary report should contain:
- The number of nodes and edges.
- The graph density.
- Degree distribution plots for in-degree and out-degree.
- A table of identified hubs.
- Top routes by passenger flow (table and bar chart).
- Top routes by passenger efficiency (table and bar chart).
- An interactive map showing flight routes.

### **Questions to Address:**

After completing the analysis, answer the following questions:
- Is the graph sparse or dense?
- What patterns do you observe in the degree distribution?
- Which airports are identified as hubs, and why?
- What are the busiest routes in terms of passenger traffic?
- Which routes are under/over-utilized?

## 2. Nodes' Contribution (Q2)

In any network, certain nodes (airports, in this case) play a critical role in maintaining connectivity and flow. Centrality measures are used to identify these nodes.

### **Your Task:**

1. Implement a function `analyze_centrality(flight_network, airport)` that computes the following centrality measures for a given airport:
    - _Betweenness centrality_: Measures how often a node appears on the shortest paths between other nodes.
    - _Closeness centrality_: Measures how easily a node can access all other nodes in the network.
    - _Degree centrality_: Simply counts the number of direct connections to the node.
    - _PageRank_: Computes the "importance" of a node based on incoming connections and their weights.
2. Write a function `compare_centralities(flight_network)` to:
    - Compute and compare centrality values for all nodes in the graph.
    - Plot centrality distributions (histograms for each centrality measure).
    - Return the top 5 airports for each centrality measure.

3. Ask LLM (eg. ChatGPT) to suggest alternative centrality measures that might be relevant to this task. How can you check that the results given by the LLM are trustable?
4. Implement one of these measures suggested by the LLM, compare its results to the centralities you've already computed, and analyze whether it adds any new insights.


## 3. Finding Best Routes (Q3)
Whenever you plan to fly to a specific city, your goal is to find the most efficient and fastest flight to reach your destination. In the system you are designing, the best route is defined as the one that minimizes the total distance flown to the greatest extent possible.

- In this task, you need to implement a function that, given an origin and destination city, determines the best possible route between them. To simplify, the focus will be limited to flights operating on a specific day.

__Note__: Each city may have multiple airports; in such cases, the function should calculate the best route for every possible airport pair between the two cities. For example, if city $A$ has airports $a_1, a_2$ and  city B has $b_1, b_2$, the function should compute the best routes for $a_1 \rightarrow b_1$, $a_1 \rightarrow b_2$, $a_2 \rightarrow b_1$ and $a_2 \rightarrow b_2$. If it’s not possible to travel from one airport in the origin city to another airport in the destination city on that date, you must report it as well.

The function takes the following inputs: 
1. Flights network 
2. Origin city name
3. Destination city name
4. Considered Date (in yyyy-mm-dd format)

The function output: 
1. A table with three columns: 'Origin_city_airport', 'Destination_city_airport', and the 'Best_route'.

__Note__: In the "Best_route" column, we expect a list of airport names connected by $\rightarrow$, showing the order in which they are to be visited during the optimal route. If no such route exists, the entry should display "No route found."

## 4. Airline Network Partitioning (Q4)
Imagine all these flights are currently managed by a single airline. However, this airline is facing bankruptcy and plans to transfer the management of part of its operations to a different airline. The airline is willing to divide the flight network into two distinct partitions, $p_1 $and $p_2$, such that no flights connect any airport in $p_1$ to any airport in $p_2$. The flights in $p_1$ will remain under the management of the original airline, while those in $p_2$ will be handed over to the second airline. Any remaining flights needed to connect these two partitions will be determined later.

- In graph theory, this task is known as a graph disconnection problem. Your goal is to write a function that removes the minimum number of flights between airports to separate the original flight network into two disconnected subgraphs.

The function takes the following inputs: 
1. Flight network

The function outputs: 
1. The flights removed to disconnect the graph.
2. Visualize the original flight network.
3. Visualize the graph after removing the connections and highlight the two resulting subgraphs.

__Note:__ In this task, airline only concerned with the flights between airports, and the flight times are not relevant.

## 5. Finding and Extracting Communities (Q5)
Airlines can optimize their operations by identifying communities within a flight network. These communities represent groups of airports with strong connections, helping airlines pinpoint high-demand regions for expansion or underserved areas for consolidation. By analyzing these communities, airlines can improve resource allocation, reduce costs, and enhance service quality.

1. In this task, you are asked to analyze the graph and identify the communities based on the flight network provided. For the airline, the primary focus is on the cities, so your communities should reflect the connectivity between cities through the flights that link them.

The function takes the following inputs:
1. Flight network
2. A city name $c_1$
3. A city name $c_2$

The function outputs:
1. The total number of communities and the cities that belong to each community
2. Visualize the graph highlighting the communities within the network (each community with different color)
3. If city $c_1$ and $c_2$ belong to the same community or not

__Note:__ To understand the community detection task and a method for accomplishing it, you can refer to [this](https://www.analyticsvidhya.com/blog/2020/04/community-detection-graphs-networks/)

2. Ask a LLM (ChatGPT, Claude AI, Gemini, Perplexity, etc.) to suggest an alternative algorithm for extracting communities and explain the steps required to implement it. Then, implement this algorithm and compare its results with the current method you've chosen. Discuss the differences in the outcomes and analyze which approach you think is better, providing reasons for your choice.

## Bonus Question - Connected Components on MapReduce 
MapReduce is ideal for network analysis as it enables parallel processing of large graph datasets, making it scalable and efficient. By breaking tasks into map and reduce steps, it allows for distributed analysis of networks, which is essential for handling large-scale graph problems like connected components.

1. In this task, you are required to use PySpark and the MapReduce paradigm to identify the connected components in a flight network graph. The focus should be on airports rather than cities. As you know, a connected component refers to a group of airports where every pair of airports within the group is connected either directly or indirectly.

The function takes the following inputs: 
1. Flight network
2. A starting date
3. An end date

The function outputs: 
1. The number of the connected components during that period
2. The size of each connectd componenet
3. The airports within the largest connected component identified.

__Note:__ For this task, you should check if there is a flight between two airports during that period.
__Note:__ You are not allowed to use pre-existing packages or functions in PySpark; instead, you must implement the algorithm from scratch using the MapReduce paradigm.

2. Compare the execution time and the results of your implementation with those of the GraphFrames package for identifying connected components. If there is any difference in the results, provide an explanation for why that might occur.

## Algorithmic Question (AQ)

Arya needs to travel between cities using a network of flights. Each flight has a fixed cost (in euros), and she wants to find the cheapest possible way to travel from her starting city to her destination city. However, there are some constraints on the journey:

1. Arya can make at most `k` stops during her trip (this means up to `k+1` flights).
2. If no valid route exists within these constraints, the result should be `-1`.

Given a graph of cities connected by flights, your job is to find the minimum cost for Arya to travel between two specified cities (`src` to `dst`) while following the constraints. 

### Your Task

- **a)** Write a pseudocode that describes the algorithm to find the cheapest route with at most `k` stops. 
  
- **b)** Implement the algorithm in Python and simulate the given test cases.

- **c)** Analyze the algorithm's efficiency. Provide its time complexity and space complexity, and explain whether it is efficient for large graphs (e.g., `n > 100`).

- **d)** Optimize the algorithm to handle larger graphs. Provide an updated pseudocode and analyze the computational complexity of your optimization.

- **e)** Ask LLM (e.g., ChatGPT) for an optimized version of your algorithm. Compare its solution to yours in terms of performance, time complexity, and correctness.

### Examples

#### Example 1

**Input:**

```py
n = 4  
flights = [[0, 1, 100], [1, 2, 100], [2, 0, 100], [1, 3, 600], [2, 3, 200]]  
src = 0  
dst = 3  
k = 1  
```
**Output:**

```py
700  
```

**Explanation:**  
Arya's optimal path with at most 1 stop is `0 → 1 → 3`, costing 100 + 600 = 700 euros.  
The path `0 → 1 → 2 → 3` is cheaper but requires 2 stops, which violates the constraints.


#### Example 2

**Input:**
```py
n = 3  
flights = [[0, 1, 100], [1, 2, 100], [0, 2, 500]]  
src = 0  
dst = 2  
k = 1  
```
**Output:**
```py
200  
```
**Explanation:**  
Arya's optimal path with at most 1 stop is `0 → 1 → 2`, costing 100 + 100 = 200 euros.


#### Example 3

**Input:**
```py
n = 3  
flights = [[0, 1, 100], [1, 2, 100], [0, 2, 500]]  
src = 0  
dst = 2  
k = 0  
```
**Output:**
```py
500  
```
**Explanation:**  
Arya cannot make any stops. The only valid route is `0 → 2`, costing 500 euros.

#### Example 4

**Input:**
```py
n = 4  
flights = [[0, 1, 100], [0, 2, 200], [1, 3, 300], [2, 3, 300]]  
src = 0  
dst = 3  
k = 2  
```
**Output:**
```py
400  
```
**Explanation:**  
Arya can take `0 → 1 → 3` and `0 → 2 → 3`, however first one is cheaper, costing 400 euros.

#### Example 5

**Input:**
```py
n = 4  
flights = [[0, 1, 100], [0, 2, 200], [1, 3, 300], [2, 3, 200]]  
src = 0  
dst = 3  
k = 2  
```
**Output:**
```py
400  
```
**Explanation:**  
Arya can take `0 → 1 → 3` and `0 → 2 → 3` like last example. However we have a tie, so it does not matter the route we take, the cost is still 400.

Have a blast!
