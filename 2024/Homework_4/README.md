# Homework 4 - Movie Recommendation System

<p align="center">
<img src="https://movielens.org/images/site/main-screen.png" width = 600>
</p>

Understanding user preferences is essential for recommendation systems in the entertainment industry, especially in movies. The MovieLens dataset is a rich source of user behavior data, including movie ratings, that can help explore trends and preferences. Hashing and clustering techniques can be implemented to analyze and segment users to provide personalized recommendations.

You and your team were hired to help hired to work on a recommendation system. Your tasks are to apply hashing techniques to improve data retrieval speed and to use clustering to group users by similar movie preferences. 

---

## VERY IMPORTANT

1. **!!! Read the entire homework before coding anything!!!**
2. *My solution is not better than yours, and yours is not better than mine*. In any data analysis task, there **is no** unique way to answer. For this reason, it is crucial (**necessary and mandatory**) that you describe every decision you make and all your steps.
3. Once solving an exercise, comments about the obtained results are **mandatory**. We are not always explicit about where to focus your comments, but we will always want brief sentences about your discoveries.
4. We encourage using chatGPT (Claude AI, Gemini, Perplexity, or any other Large Language Models (LLM) chatbot tool) to help you solve your homework, but we expect you to learn how to use them responsibly. **Using such tools when not explicitly allowed will be considered plagiarism and strictly prohibited**.

Now that it is all well settled, let's get on with it!

---

## 1. Recommendation System with LSH

In this section, you will implement a recommendation system by identifying users with similar preferences and suggesting movies based on their behavior. 
Specifically, you will implement your version of the [**LSH algorithm**](https://www.learndatasci.com/tutorials/building-recommendation-engine-locality-sensitive-hashing-lsh-python/).

### 1.1 Data Preparation

Download the MovieLens dataset from [here](https://www.kaggle.com/datasets/grouplens/movielens-20m-dataset?select=rating.csv). After downloading, explore the dataset to understand the structure and identify any preprocessing steps needed.

### 1.2 Minhash Signatures

Using the `userId` and `movieId` columns, implement your own MinHash function. This function will hash each user's watched movie list, creating a representation that allows for quick comparisons of user similarities.

- **Important:** Implement your MinHash function from scratch—**do not use any pre-built hash functions.**
- Use your MinHash function to generate signature vectors for each user based on their rated movies.
- Experiment with different hash functions and threshold values to find the most effective configurations. Report these results.
- Read the class materials and, if necessary, conduct an internet search. The description of hash functions in the [book](http://infolab.stanford.edu/~ullman/mmds/ch3n.pdf) may be helpful as a reference.

### 1.3 Locality-Sensitive Hashing (LSH)

Now that you have generated MinHash user signatures, apply Locality-Sensitive Hashing (LSH) to cluster similar users.

1. **Bucket Creation:** For each user, divide the MinHash signature into bands and hash each band to form buckets. Users with similar bands should fall into the same buckets.
   - **Debugging Tip:** After creating buckets, check a few bucket contents to verify that multiple users are being grouped in the same buckets.
   
2. **Query:** For a given user, identify the **two most similar users** based on their bucket placement. If a user doesn’t have any similar users in their bucket, adjust the parameters until similar users are found.

3. **Movie Recommendation Logic:**
   - If both similar users have rated a movie, recommend this movie based on the **average rating**.
   - If there are no commonly rated movies, recommend the top-rated movies of the most similar user.

4. **Final Recommendation:** Provide **at most five movies** to the user. 

Example recommendation logic for a user:

| User | Movie Title         | Rating |
|------|----------------------|--------|
| A    | Inception           | 4.5    |
| A    | Titanic             | 4.2    |
| A    | Avatar              | 2.8    |
| B    | Inception           | 4.6    |
| B    | The Matrix          | 3.9    |
| B    | Toy Story           | 4.7    |
| C    | Titanic             | 3.8    |
| C    | Avatar              | 4.3    |
| C    | Shrek               | 4.1    |

If User A and User B are identified as the two most similar users to User X, the recommended movies would be:
1. **Common Movies:** "Inception" (average rating: 4.55).
2. **Top-rated from Most Similar User:** "Toy Story" (4.7) from User B and "Titanic" (4.2) from User A.
3. If fewer than 5 movies are found, complete the list using other high-rated movies by the most similar users.

## 2. Grouping Movies Together! 
In this section, you will explore clustering algorithms to group the movies you have based on specific features you choose to consider for them.

### 2.1 Feature Engineering 
As you know, the dataset provided isn’t particularly clean or well-structured to represent the features of the movies. Therefore, your first step is to create a more suitable set of attributes (variables, features, covariates) to represent the movies based on the available information. Here are some variables or features you might consider for clustering:

1. ```movieid``` id of each movie 
2. ```genres``` list of genres attached to the movie (given that a movie may have several genres, it’s essential to devise a method to accurately represent the genres for each movie)
3. ```ratings_avg``` the average ratings provided by users for the movie
4. ```relevant_genome_tag``` the most relevant tag to the movie given in the genome set
5. ```common_user_tag``` the most common tag given to the movie by the users 

In addition to the above features, include **at least three additional** features for clustering.

__Note__: If you have accurately identified and applied the methods for representing the features, you should have __more than eight features__! How could this happen? Take a moment to think about it.

### 2.2 Choose your features (variables)!
With multiple features available for the movies, you need to consider the following two questions: 1. Should you normalize the data or leave it as is? 2. Should you include all these features, or can you reduce the dimensionality of the data?

1. What is the importance of normalizing the data in your analysis, and how does it impact the effectiveness of the clustering algorithms you plan to use?
2. If you find that normalizing the values is beneficial, please proceed to normalize the data. To simplify this task, refer to the [scikit-learn](https://scikit-learn.org/stable/modules/preprocessing.html) package for tools and functions that facilitate data normalization.
3. Could you provide some insights on dimensionality reduction? What techniques would be effective for reducing the number of features in the dataset, and why might this be beneficial for the analysis?
4. If you believe dimensionality reduction would be advantageous, please select a method to reduce the dimensionality of the data.

### 2.3 Clustering 
Now that you have prepared the data, you can create the clusters.

1. How can you determine the optimal number of clusters for your data? Please use at least two methods and provide their results.
2. Implement the K-means clustering algorithm (not K-means++) through MapReduce. We request that you develop the algorithm from scratch based on what you've learned in class and run the algorithm on your data.
3. Implement the K-means++ algorithm from scratch and apply it to your data. Do you notice any differences between the results obtained using random initialization and those achieved with K-means++? Please explain your observations and discuss why these differences might occur.
4. Ask an LLM (ChatGPT, Claude AI, Gemini, Perplexity, etc.) to recommend another clustering algorithm. Use that LLM to describe the workings of the algorithm, as well as its advantages and disadvantages compared to K-means and K-means++. Additionally, ask to implement the algorithm for you or utilize an existing version from a package. Apply that algorithm to your data and explain any differences you observe in the results compared to those obtained previously.

 ### 2.4 Best Algorithm
Clustering helps identify natural groupings within data, but no single algorithm works best for every dataset. In this section, you’ll learn how to choose the most suitable clustering method based on your data’s unique characteristics. By analyzing patterns and comparing results, you’ll uncover which algorithm provides the most meaningful insights and clusters.


1. Set the number of clusters to the optimal number $k_{opt}$ based on any of the methods previously.
2. Select three distinct metrics to assess the quality of the clusters. Describe each metric in detail, including the specific aspects they evaluate to determine the effectiveness of the clustering model.
3. Apply the three clustering algorithms used in the prior section to partition the data into $k_{opt}$ clusters. Then, evaluate each model's clustering quality using the selected metrics. Summarize your findings by comparing the results of each algorithm based on the metric evaluations.

## 3. Bonus Question
K-means is an iterative algorithm, meaning that with each iteration, it refines the clusters by adjusting them based on the distance of each data point relative to the center of each cluster. This process continues until it reaches a point of convergence or hits a set limit on the number of iterations. You might want to track the progress of forming your clusters.

1. Select two variables* from your instances to display them on a 2D plot. Then, illustrate the progression of the clusters as they change at each iteration. We expect a plot for each iteration, displaying the instances and the clusters they belong to. Select the two features that most effectively separate visual instances belonging to different clusters. Explain the method you used to determine these features.

__*Note:__ Depending on the variables you want to use for clustering, whether they are the original movie features or the components derived from PCA, you may select two features/components that best help to visually display the clusters.

## 4. Algorithmic Question

Two brilliant strategists, Arya and Mario, are about to play a game with a sequence of numbers. Arya, as player 1, begins the game, while Mario, player 2, plays 2nd. Their goal is clear: to collect the highest possible score by taking numbers from either end of the sequence, one at a time. They will play in perfect synchronicity, each seeking the advantage.

The sequence represented as an array of `nums,` is laid out in front of them. Arya will start by selecting either the number at the beginning (`nums[0]`) or the end (`nums[nums.length - 1]`) of the array, adding that value to her score. This value is then removed from the beginning or the end of `nums`. Then, it’s Mario’s turn to do the same with the remaining sequence. The game proceeds this way, with each player taking numbers from either end until no numbers are left to claim. The player with the highest score wins.

However, if they end in a tie, Arya, as the first to act, will claim victory by default.

Arya is now before you, asking for help to predict her chances. She wants to know, with her best possible choices, whether she can guarantee a win, assuming both players play with perfect skill.

- a) Help Arya by providing a pseudocode for finding an optimal playing strategy, that is, a strategy that maximizes her value. (Hint: Use recursion, assuming that both players play optimally).

- b) Write a Python program implementing her game strategy. Try different array lengths to test the algorithm.

- c) Is the algorithm efficient? Prove that it is polynomial and provide an asymptotic time complexity bound, or show that it requires exponential time.

- d) If the algorithm is exponential, explain how to make it polynomial and provide a pseudocode for it. Recompute the computational complexity of the updated algorithm.

- e) Implement the algorithm in Python. Compare your result values with the previous algorithm. Also compare the running times.

- f) Finally, consult LLM (ChatGPT, Claude AI, Gemini, Perplexity, etc.) to craft a third, optimized implementation and analyze its time complexity. Also, explain if the LLM is doing a good job and how you can evaluate whether the suggested solution works properly.

**Examples**

__Input 1__  
```
nums = [1, 5, 2]
```

__Output 1__  
```
false
```

__Explanation__: Arya’s optimal choices still lead her to a lower score than Mario’s, so she cannot guarantee victory.

__Input 2__  
```
nums = [1, 5, 233, 7]
```

__Output 2__  
```
true
```

__Explanation__: Arya, by playing perfectly, can ensure she ends up with the highest score.

---

Break a leg!

