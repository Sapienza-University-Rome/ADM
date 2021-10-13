# Homework 2 - Steam Reviews 2021

Video games have become a relevant part of everybody's childhood and (in many cases) adulthood. Along with the Internet growth, multiple distribution services appeared to provide digital media content such as audio, video, e-books and video games. The latter is the case of **Steam**. It is a service that offers digital rights management (DRM), server hosting, video streaming, and social networking services. It also gives the user installation and automatic updating of games and community features such as friends lists and groups, cloud storage, and in-game voice and chat functionality.

Imagine that you have been hired as a data scientist from a top Game Development Company. You and your team have to perform an analysis of the reviews received for the applications (games) in Steam.  Each row in the dataset represents a review made by one user (Author) about a specific application.

Your **goal** is to answer some research questions (RQs) that may help them discover and interpret meaningful patterns in data and eventually understand what a user looks for in a video game.

![steam](https://www.vortez.net/contentteller.php?ct=news&action=file&id=18653)
____

## Before starting
Among all the numerous things and good practices a data scientist needs to do before running any analysis, there is one of uttermost importance: **get data and understand it**! 


Here you find the list of tasks you need to perform before digging into the world of Steam.

* **Get your data!** Go to [this website](https://www.kaggle.com/najzeko/steam-reviews-2021) and download the files **steam_reviews.csv**.
* **Understand your data.** Read the name of each column to understand what it refers to. Additional information about the variables can be found in the description of the data section on the web page. Please, be sure that you've understood the data before start coding.
* **Handling data.** The data are provided in one `.csv` file. For this reason, to answer the RQs, we kindly suggest you import the `.csv` files as `pandas DataFrame` object and then, based on what you want to analyze, perform the necessary operations. 

Remember, **Google is your best friend!**


____


# VERY VERY IMPORTANT
1. **!!! Read the entire homework before coding anything!!!**
2. *My solution it's not better than yours, and yours is not better than mine*. In any data analysis task, there **is not** a unique way to answer to RQs. For this reason, it is crucial (**necessary and mandatory**) that you describe any single decision you take and all the steps you do.
3. Once performed any exercise, comments about the obtained results are **mandatory**. We are not always explicit about where to focus your comments, but we will always want some brief sentences about your discoveries.

____


# Research questions

1. [__RQ1__] After collecting information, the Data Scientists have to know what dataset they are dealing with, so let's start with an **Exploratory Data Analysis (EDA)**. What can you say about our dataset? Please summarize its main characteristics with visual and tabular methods.
   
2. [**RQ2**] *Let's explore the dataset by finding simple insights into the reviews.*
    - Plot the number of reviews for each application in descending order.
    - What applications have the best Weighted Vote Score?
    - Which applications have the most and the least recommendations?
    - How many of these applications were purchased, and how many were given for free?

3. [**RQ3**] *Now it's important to understand the preferred time to do reviews.*
    - What is the most common time that authors review an application? For example, authors usually write a review at 17:44.
    - Create a function that receives as a parameter a list of time intervals and returns the plot the number of reviews for each of the intervals.
    - Use the function that you created in the previous literal to plot the number of reviews between the following time intervals: 
    
| Initial time | Final time |
| ----------- | ----------- |
|06:00:00 | 10:59:59|
|11:00:00 | 13:59:59|
|14:00:00 | 16:59:59|
|17:00:00 | 19:59:59|
|20:00:00 | 23:59:59|
|00:00:00 | 02:59:59|
|03:00:00 | 05:59:59|

5. [**RQ4**] *As Steam is a worldwide platform, the reviews can be done in many languages. Let's extract some information about it.*
    - What are the top 3 languages used to review applications?
    - Create a function that receives as parameters both the name of a data set and a list of languages’ names and returns a data frame filtered only with the reviews written in the provided languages.
    - Use the function created in the previous literal to find what percentage of these reviews (associated with the top 3 languages) were voted as funny?
    - Use the function created in the literal “a” to find what percentage of these reviews (associated with the top 3 languages) were voted as helpful?

5. [**RQ5**] *The reviews' authors are users from the game that provide their opinion on it. Now you can check how often they make reviews.*
    - Plot the top 10 most popular reviewers and the number of reviews.
    - What applications did the most popular author review? 
    - How many applications did he purchase, and how many did he get as free? Provide the number (count) and the percentage.
    - How many of the applications he purchased reviewed positively, and how many negatively? How about the applications he received for free?

6. [**RQ6**] *It's time to get information from the updates that a user does to his reviews.*
    - What is the average time (days and minutes) a user lets pass before he updates a review?
    - Plot the top 3 authors that usually update their reviews.

7. [**RQ7**] *Of course, calculating probabilities is a job that any Data Scientist must know. Let's compute Some interesting figures.*
    - What’s the probability that a review has a Weighted Vote Score equal to or bigger than 0.5?
    - What’s the probability that a review has at least one vote as funny given that the Weighted Vote Score is bigger than 0.5?
    - Is the probability that “a review has at least one vote as funny” independent of the “probability that a review has a Weighted Vote Score equal or bigger than 0.5”?

8. [**RQ8**] *Every decision you take in a data-based environment should be reinforced with charts, statistical tests and analysis methods to check if a hypothesis is correct or not.*
    - Is there a significant difference in the Weighted Vote Score of reviews made in Chinese vs the ones made in Russian? Use an appropriate statistical test or technique and support your choice.
    - Can you find any significant relationship between the time that a user lets pass before he updates the review and the Weighted Vote Score?  Use an appropriate statistical test or technique and support your choice.
    - Is there any change in the relationship of the variables mentioned in the previous literal if you include whether an application is recommended or not in the review?  Use an appropriate statistical test or technique and support your choice.
    - What are histograms, bar plots, scatterplots and pie charts used for?
    - What insights can you extract from a Box Plot?


### Bonus points

1. For this homework, you are required to work with all data in the **steam_reviews.csv**. An extension (two files) of the dataset is available in the next links: 

      a. If you want to download them from a Google Drive use [this link](https://drive.google.com/drive/folders/1dHbQ5mIENin5w03vH-3kSGMaZSczw4n7).
      
      b. If you want work with them from an wget-friendly environment (Terminal, Sagemakewr) use this link: [this link]().
    
    It is not necessary to use the extension for this homework, however, if you decide to use it, we will take it into account in the final evaluation. In summary, to get the bonus points you are required to work with [steam_reviews.csv + two files of extension] all together.


# Theoretical Questions
### TQ1
We are given the following algorithm.
```
Input: 
    A: array of length n
    k: integers between 1 and n
    
function alg(A, k):
  s <-- a random element of A
  set L = [all the elements of A with value <= s]
  set R = [all the elements of A with value > s]
  r = len(L)
  if k == r:
    return s
  else if k < r:  
    return alg(L, k)
  else:
    return alg(R, k - r)
```
1. What does the algorithm compute?
2. What is asymptotically (i.e., we are asking for big-O complexity) the running time of the algorithm in the worst case, as a function of n?
3. What is asymptotically the running time of the algorithm in the best case? 

### TQ2
You are given the recursive function *splitSwap*, which accepts an array *a*, an index *i*, and a length *n*.
```
function splitSwap(a, l, n):
  if n <= 1:
    return
  splitSwap(a, l, n/2)
  splitSwap(a, l+ n /2, n/2)
  swapList(a, l, n)
```
The subroutine swapList is described here:
```
function swapList(a, l, n):
  for i = 0 to n/2:
    tmp = a[l + i]
    a[l + i] = a[l + n/2 + i]
    a[l + n/2 + i] = tmp
```
1. How much running time does it take to execute *splitSwap(a, 0, n)*? (We want a Big O analysis.)
2. What does this algorithm do? Is it optimal? Describe the mechanism of the algorithm in details, we do not want to know only its final result.

**HINT:** Consider the scenario where len(a) and n are numbers that are a power of 2.

### TQ3
In the knapsack problem we are given n objects and each object *i* has a weight *w_i* and a value *v_i*. We are also given a weight budget *W*.
The problem is to select a set of objects with total weight bounded by *W* that maximized the sum of their values.
The following are three natural heuristics:
   - Order them in increasing order of weight and then visit them sequentially, adding them to the solution as long as the budget is not exceeded
   - Order them in decreasing order of values, and then visit them sequentially, adding them to the solution if the budget is not exceeded
   - Order them in decreasing relative value *(v_i / w_i)*, and then visit them sequentially, adding them to the solution if the budget is not exceeded

For each of the heuristics, provide a counterexample, that is, an example of a problem instance in which the heuristic fails to provide the optimal solution.
