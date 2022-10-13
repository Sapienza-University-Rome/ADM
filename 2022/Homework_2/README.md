# Homework 2 - Instagram Profiles & Posts 

Nowadays, social media is widely used, taking significant importance in people's lives and influencing how they live. Moreover, social media, which is here to stay, has substantially impacted how people communicate. Thus, available on iPhone and Android, **Instagram** is a free picture and video-sharing app. Their service allows users to post photographs and videos that they may then share with their followers or a small group of friends. In addition, they can also browse, comment on, and "like" the Instagram posts their friends have shared.

Imagine that you all have been hired as Data Scientists at Instagram. You and your team have to analyse the posts received by users worldwide. Each row in the datasets may represent a post, a profile or a location associated with the posts done.

Your **goal** is to answer some research questions (RQs) that may help them discover and interpret meaningful patterns in data and eventually understand how a user behaves on this social network.

![steam](http://pbsproracing.com/wp-content/uploads/2018/10/Instagram-Banner-Logo-de-Instagram-vector-logo-instagram-sin-fondo-1000x480.gif)
____

## Before starting
Among all the numerous things and good practices a Data Scientist needs to do before running any analysis, there is one of uttermost importance: **get data and understand it**! 


Here you find the list of tasks you need to perform before digging into the world of Instagram.

* **Get your data!** Go to [this website](https://www.kaggle.com/datasets/shmalex/instagram-dataset?select=instagram_profiles.csv) and download the whole dataset, make sure it includes the files **instagram_profiles.csv**, **instagram_posts.csv** and **instagram_locations.csv**.
* **Understand your data.** Read the name of each column to understand what it refers to. Additional information about the variables can be found in the description of the data section on the web page. Please, be sure that you've understood the data before starting coding.
* **Handling data.** The data are provided in many `.csv` files (tab separated). For this reason, to answer the RQs, we kindly suggest you import the `.csv` files as `pandas DataFrame` objects and then perform the necessary operations based on what you want to analyse.

Remember, **Google is your best friend!**


____


# VERY VERY IMPORTANT
1. **!!! Read the entire homework before coding anything!!!**
2. *My solution it's not better than yours, and yours is not better than mine*. In any data analysis task, there **is not** unique way to answer to RQs. For this reason, it is crucial (**necessary and mandatory**) that you describe any single decision you take and all your steps.
3. Once performed any exercise, comments about the obtained results are **mandatory**. We are not always explicit about where to focus your comments, but we will always want some brief sentences about your discoveries.

____


# Research questions

1. [__RQ1__] After collecting information, the Data Scientists have to know what dataset they are dealing with, so let's start with an **Exploratory Data Analysis (EDA)**. What can you say about our datasets? Please summarise its main characteristics with visual and tabular methods.
   
2. [**RQ2**]  *Let's explore the dataset by finding simple insights regarding the profile and posts.*
    - Plot the number of posts for each profile in descending order.
    - What posts have the highest number of "likes"?
    - What posts have the most and the least number of comments?
    - How many posts include tagged locations, and how many do not? Show it using an appropriate chart and comment your results.
    - How many posts include only photos? How many also have videos?
    - What's the percentage of business accounts vs non-business? What can you interpret regarding that percentage?

3. [**RQ3**] *Now it's important to understand the most common times in which users publish their posts*
    - What is the most common time in which users publish their posts? 
    - Create a function that receives a time intervals list as a parameter and returns a plot with the number of posts for each given interval.
    - Use the function that you created in the previous literal to plot the number of posts between the following time intervals:

<div align="center">

| Initial time | Final time |
| ----------- | ----------- |
|06:00:00 | 10:59:59|
|11:00:00 | 13:59:59|
|14:00:00 | 16:59:59|
|17:00:00 | 19:59:59|
|20:00:00 | 23:59:59|
|00:00:00 | 02:59:59|
|03:00:00 | 05:59:59|

</div>
	
4. [**RQ4**] *In most cases, we will not have a __consistent dataset__, and the one we are dealing with is not an exception (ex. in the given datasets, you may not find the information of the profiles for some of the posts). So let’s enhance our analysis.* 
    - Write a function that, given a profile_id, will be able to return the posts that belong to the given *profile_id*.
    - Write another function that, given an input n (an integer), will return the posts that belong to the n top posted profiles (top n profiles that have posted the highest number of posts) that their data is available in the *profile.csv* using the previously written function.
    - What is the average number of "likes" and comments of the top 10 profiles with the highest number of posts which their information is available in *profile.csv*?
    - Plot the number of posts that these top 10 profiles have sent on Instagram in the given interval in question RQ3. Interpret the resulting chart.

5. [**RQ5**] *The most influential users are the ones with the highest number of “followers", you can now look more into their activity.*
    - Plot the top 10 most popular users in terms of followers and their number of posts.
    - Who is the most influential user?
    - Have they posted anything with tagged locations? Extract the most frequent areas on their posts and plot the number of times each city has been visited.
    - How many pictures-only posts have they published? How many reels? (only videos) and how many with both contents? Provide the number as percentages and interpret those figures. 
    - How many "likes" and comments did posts with only pictures receive? How about videos and mixed posts? Try to provide the average numbers and confront them with their followers amount, explaining what you can say from that comparison.

6. [**RQ6**] *It's time to get information from the user posting effectiveness.*
    - What is the average time (days and minutes) a user lets pass before publishing another post?
    Plot the top 3 users that publish posts more frequently (calculate the average time that passes between posts), including their amount of followers and following. Provide insights from that chart.
    - Using the function you previously coded, plot the time intervals with the highest average number of “likes” and the ones with the highest average number of comments on posts.

7. [**RQ7**] *Of course, calculating probabilities is a job that any Data Scientist must know. So let's compute some engaging figures.*
    - What's the probability that a post receives more than 20% "likes" of the number of followers a user has?
    - Do users usually return to locations? Extract the probability that a user returns to a site after having posted it in the past. Does that probability make sense to you? Explain why or why not.

8. [**RQ8**]  *Every decision you take in a data-based environment should be reinforced with charts, statistical tests and analysis methods to check whether a hypothesis is correct or not.*
    - Does more “likes” also mean more comments? Plot a scatter plot of “likes” vs comments for posts.
    - Can you find any significant relationship between the time a user publishes a post and the number of comments and “likes”? Use an appropriate statistical test or technique and support your choice.
    - What’s the distribution of followers? Plot the empirical distribution of followers amongst all users and extract the mean, mode, and quantiles. Interpret those figures.
    - What are histograms, bar plots, scatterplots and pie charts used for?
    - What insights can you extract from a Box Plot?


### Bonus points
Up to this point, you probably have worked with one or two files simultaneously. Nevertheless, for the literals *a.* and *b.* of this section, you must work with the **three datasets at the same time**.
Note that performing some of these operations might be too complex for your pc specs. For this reason, we suggest you make use of AWS (yeah! only a suggestion). In case you need it, in the following links you can find the same three files already mounted into AWS for you to work with them easily ([instagram_posts](https://adm2022.s3.amazonaws.com/instagram_posts.zip), [instagram_profiles](https://adm2022.s3.amazonaws.com/instagram_profiles.zip), [instagram_locations](https://adm2022.s3.amazonaws.com/instagram_locations.zip)).

a. Sort the users in terms of number of followers and divide them into two groups: for the first group, take only the top 10% regarding "followers", and for the second one, take the rest. Now compare the mean of time intervals between posts for the two categories. Do you notice something relevant?

b. Assume users publish their posts the same day pictures or videos are taken:  Are there users that have visited the same location on the same day? How about the same week? Extract the results and explain them.

c. Implement a **text data analysis** (also known as **text mining**) of the field "description" from *instagram_posts.csv* for descriptions written in English. Use appropriate visualizations and statistics to highlight the words (and probably the topics) provided for the users in that field.

# Command Line Question 

Using the command line is a feature that Data Scientists must master. It is relevant since the operations there require less memory to use in comparison to other interfaces. It also does not use as much CPU processing time as other interfaces. In addition, it can be faster and more efficient and handle repetitive tasks quickly. 

In this question, you should use command line tools such as grep and possibly other commands to answer the following question: 
- Using the instagram_posts.csv, retrieve the first __ten posts__ with descriptions __longer than 100 characters__ and output the <ins>profiles that posted them</ins>. (Please keep in mind that the profile associated with some of those posts may not be found in the profiles. You can simply output __User was not found!__ for those posts.)

__Note:__ You may work on this question <ins>in any environment</ins> (AWS, your PC command line, Jupyter notebook, etc.), but the final script must be placed in __CommandLine.sh__, which must be executable.

# Algorithmic Question
1. [**AQ1**] Given the following pseudocode, answer the questions: 

<pre>
Input: 
    N : an integer 
    List : array of characters of length N without repetition
    
function f1(sequence, end): 
    For i=0 To end:
        OUTPUT sequence[i]
    EndFor
    Output "\n"
    
function f2(sequence, start, end): 
    If start = end: 
        f1(sequence, end)
    Else
        For i=start To end: 
            temp <-- sequence[start]
            sequence[start] <-- sequence[i]
            sequence[i] <-- temp
            f2(sequence, start+1, end)
            temp <-- sequence[start]
            sequence[start] <-- sequence[i]
            sequence[i] <-- temp
f2(List, 0, N)
</pre>
- What is the output of this algorithm? Describe the mechanism of the algorithm <ins>in detail </ins>. We __do not__ want to know only its final result. (Describe one example on your own)
- What is asymptotically (i.e., we are asking for big-O complexity) the algorithm's running time as a function of N? 
- Is this algorithm the __optimal__ one to produce this output? If not, can you suggest a <ins>better algorithm</ins> to perform the same task?

2. [**AQ2**] *Considering the following problem, answer the questions:* 

Alex has a ribbon of <ins>length N</ins>. He wants to cut the ribbon in a way that fulfils the following __three__ conditions:

- Each piece of the cut should have an <ins>integer length</ins> 
- He should <ins>at least</ins> cut the ribbon once
- The __multiplication__ of the length of all the pieces be the <ins>maximum possible</ins> 

1. Implement a __recursive algorithm__ to help Alex find the maximum possible value after multiplying the length of the pieces. Explain your algorithm in detail. 
2. Show that the algorithm has <ins>exponential</ins> running time. 
3. Now provide a <ins>polynomial solution</ins>, based on __dynamic programming__, and compute its running-time complexity.
4. Evaluate the <ins>running time</ins> of your algorithm for the sizes (Ns) in the __range of [2, 25]__, plot the results, and interpret it (if you have implemented <ins>two algorithms</ins>, please include both in the plot and compare them). 
5. (Optional, mini bonus) Is the algorithm of question 3 __optimal__? If you belive it, can you prove it? If not, can you find a __faster__ algorithm? In case you found a faster algorithm implement it and explain your algorithm in detail. 



