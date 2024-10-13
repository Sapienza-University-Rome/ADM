# Homework 2 - Videogames Reviews

<img src="https://mmos.com/wp-content/uploads/2021/07/steam-logo-welcome-banner.jpg" alt="drawing" width="1000"/>

Video games have evolved into a major form of entertainment, leaving a lasting impression on many people’s childhoods and continuing to captivate audiences well into adulthood. In recent years, gaming has transcended from a simple hobby into a global phenomenon, influencing culture and technology. As the internet grew, numerous digital distribution platforms offered a vast array of content, including music, videos, e-books, and video games. [Steam](https://store.steampowered.com/), one of the most prominent platforms, not only offers digital rights management and server hosting but also provides services like video streaming and social networking. Steam's features include game installation, automatic updates, and various community elements, such as friends lists, groups, cloud storage, and in-game voice and chat functions. Beyond just a store, Steam serves as a hub where gamers can connect and share their experiences, fostering a global gaming community.

Imagine that you and your team have been hired as a data scientist by a leading Game Development Company, where your primary mission is to harness the power of data. Along with your team, you're tasked with analyzing the vast pool of game reviews on Steam, where users (Authors) share their thoughts and feedback about various games. Each row in your dataset corresponds to a review, representing a unique interaction between a player and a game.

Your **objective** is to answer research questions (RQs) to uncover meaningful patterns in the data, helping the company understand what players value in a video game.



____

## Before starting
Among all the numerous things and good practices a data scientist needs to do before running any analysis, there is one of uttermost importance: **get data and understand it**! 


Here, you find the list of tasks you need to perform before digging into the world of Steam.

* **Get your data!** Go to [this website](https://www.kaggle.com/najzeko/steam-reviews-2021) and download the files **steam_reviews.csv**.
* **Understand your data.** Read the name of each column to understand what it refers to. Additional information about the variables can be found in the description of the data section on the web page. Please, be sure that you've understood the data before start coding.
* **Handling data.** The data are provided in one `.csv` file. For this reason, to answer the RQs, we kindly suggest you import the `.csv` files as `pandas DataFrame` object and then, based on what you want to analyze, perform the necessary operations. 

Friendly reminder: The Internet is your friend, and it may be the source of the answer you may have along this and many other projects!


____


# VERY VERY IMPORTANT
1. **!!! Read the entire homework before coding anything!!!**
2. *My solution it's not better than yours, and yours is not better than mine*. In any data analysis task, there **is not** a unique way to answer to RQs. For this reason, it is crucial (**necessary and mandatory**) that you describe any single decision you take and all the steps you do.
3. Once performed any exercise, comments about the obtained results are **mandatory**. We are not always explicit about where to focus your comments, but we will always want some brief sentences about your discoveries.
4. We encourage using chatGPT (Claude AI, Gemini, Perplexity, or any other Large Language Models (LLM) chatbot tool) as allies to help you solve your homework, and we were hoping you could learn how to use them properly. However, using such tools when not explicitly allowed will be considered plagiarism and strictly prohibited.

____

# Research questions (RQs)

1. [**RQ1**]  Before diving deep into the dataset provided, it's crucial to understand its structure and main features. Data scientists usually take the first step of performing an Exploratory Data Analysis (EDA). What can you say about our dataset? Please perform an EDA and summarize the dataset's key characteristics using visualizations and tabular summaries.

2. [**RQ2**] *Let's explore the dataset by analyzing the distribution of reviews across different applications.*
   - Identify which applications have the highest and lowest number of reviews.
   - Plot the number of reviews for each application in descending order. What insights can you draw from the plot?
   - For the top 5 applications by number of reviews, how many reviews came from users who purchased the application versus those who received it for free? Provide a percentage breakdown and highlight any similarities.
   - Which applications have the most and the least user recommendations? Summarize your findings.
   - Is there a correlation between the number of recommendations and the applications' review scores? Use a statistical test to confirm the significance of the relationship.

3. [**RQ3**] *Understanding when users are most active in submitting reviews can help identify peak engagement periods.*
   - Plot the number of reviews submitted each month and describe any trends.
   - Identify any seasonal patterns or trends in review activity. Explain any seasonal impact you notice.
   - Determine if certain times of the year have higher engagement rates. Describe noticeable peaks in user activity.
   - What is the most common time of day users write reviews? For example, users might typically write reviews at 17:44. Explain how this time distribution could influence your analysis.
   - Create a function that accepts a list of time intervals and plots the number of reviews for each interval.
   - Use the function to plot the number of reviews for the following time intervals:

| Initial Time | Final Time |
|--------------|------------|
| 00:00:00     | 02:59:59   |
| 03:00:00     | 05:59:59   |
| 06:00:00     | 10:59:59   |
| 11:00:00     | 13:59:59   |
| 14:00:00     | 16:59:59   |
| 17:00:00     | 19:59:59   |
| 20:00:00     | 23:59:59   |

   - Summarize your findings from the time interval analysis.

4. [**RQ4**] *Investigating whether users who spend more time using an application give higher or lower ratings.*
   - Analyze the relationship between the amount of time a user has spent on an application and their review score.
   - Do more experienced users (who have used the application longer) tend to give higher or lower ratings? Comment on any trends you observe.
   - Plot the distribution of review scores based on different user experience levels (e.g., new users vs. veteran users). Is there a statistical difference in the score distributions? Use an appropriate statistical test to validate your hypothesis.
   - Ask an LLM tool (ChatGPT, Claude AI, etc.) to interpret the statistical results of the analysis and provide potential explanations for the trends. Does the LLM suggest additional factors that could explain why users who spend more time on the app give higher or lower ratings? How can you validate the interpretations provided by the LLM?

5. [**RQ5**] *It is interesting to explore the top reviewers to gain insight into their demographic location, the quality of their reviews, and the applications they tend to review most frequently.*
   - Determine the ten reviewers with the highest number of reviews in the dataset.
   - What is the percentage of each language used by these top 10 reviewers when submitting a review?
   - Let's examine whether other users found the reviews from these top 10 reviewers helpful or if they were simply spamming. Calculate the average number of valuable votes these reviewers received for their submitted reviews. Elaborate on the results you see.
   - Create a plot showing the distribution of the number of reviews each application received from the top 10 reviewers, arranged in descending order.

6. [**RQ6**] *Let's investigate the behavior of specific groups, specifically focusing on English and Spanish reviewers*
    - Which group is more likely to edit or update their review after submitting it? “English or Spanish!”?
    - Provide the average number of games that reviewers from each group have on their Steam accounts and the average number of games for which they write reviews. What can you say about the number you just calculated?

7. [**RQ7**] *Certainly, calculating probabilities and conducting statistical tests are essential skills for any data scientist. Let's calculate some intriguing figures.*
   - What is the probability of submitting a review and receiving at least one helpful vote from other users?
   - What is the probability of submitting a review and receiving at least one helpful vote from other users, given that you don’t recommend the app?
   - Is the probability of “a review receiving at least one helpful vote” independent of the probability that “the reviewer has submitted at least five reviews before the current review”? Elaborate on it.
   - We hypothesize that “reviewers who own a larger number of games are likely to leave fewer reviews on the platform.” Please validate or refute this statement through statistical analysis.
   - Ask an LLM tool (such as ChatGPT, Claude AI, Gemini, Perplexity, etc.) to understand the purposes of histograms, bar plots, scatterplots, and pie charts and what kind of insights they offer that might be useful for statistical analysis. Are those results trustworthy, or can you do something to improve somehow the confidence in the suggestions given by the LLM?

____

# Bonus

Beyond just looking at the numerical ratings, the words users write in their reviews give us valuable insights into how they feel about the application. Let's analyze these review texts using sentiment analysis.

- Perform sentiment analysis on the review texts in the top 3 languages and classify them as **positive**, **negative**, or **neutral**.
- What is the distribution of sentiment across all reviews? 
- Does the sentiment analysis align with whether the application is recommended or not? Explain any insights from this comparison.
- Is there a correlation between the sentiment of a review and the number of helpfulness votes it receives? Provide an analysis of the results and discuss potential trends.
____

# Algorithmic Question (AQ)
You are given two positive integers, $n$ (where $1\le n \le 10^9$) and k (where $q \le k \le 100$). Your task is to express $n$ as the sum of $k$ positive integers, all having the same parity (i.e., all have the same remainder when divided by 2, meaning they are either all even or all odd).
In other words, find $a_1, a_2, ..., a_k$ each $a_i \gt 0, n = a_1 + a_2 + ... + a_k$, and all $a_i$ simultaneously are either even or odd.
If it's impossible to represent $n$ in this way, report that no such representation exists.

**Input**

In the first input line, you will receive a number t (where $1 \le t \le 100$), representing the number of test cases. The following $t$ lines will contain two values, $n$ and $k$, corresponding to each test case.

**Output**

For each test case, if it is possible to represent $n$ as the sum of $k$ positive integers, all of the same parity (either all even or all odd), print "YES" and provide the corresponding values of $a_i$ in the next line. If there are multiple valid solutions, you can print any of them. If such a representation is not possible for a given test case, print "NO".

**Examples**
---

**Input**
```
8
10 3
100 4
8 7
97 2
8 8
3 10
5 3
```
**Output**
```
YES
4 2 4
YES
55 5 5 35
NO
NO
YES
1 1 1 1 1 1 1 1
NO
YES
3 1 1
```
1. Implement a Python program to solve the problem above.
2. Please provide an analysis of your code's time complexity using Big O notation.
3. Ask an LLM tool (such as ChatGPT, Claude AI, Gemini, Perplexity, etc.) to evaluate the time complexity of your code using Big O notation. Is the assessment accurate? If it differs from your previous analysis, which would be correct? Please explain your reasoning.
  

Have fun!
