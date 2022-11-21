# Homework 4 - Getting to know your customers

<p align="center">
<img src="https://www.leaders-in-law.com/wp-content/uploads/2021/10/BANKING.png" width = 600>
</p>

Over time, the Banking sector has dabbled into plenty of Data Science applications. The latter includes topics such as Fraud detection, risk modelling for investment, personalized marketing, managing customer data and customer segmentation, among others. The latter is a crucial topic for a bank since they can offer their products more accurately and tailor-made depending on their clients' characteristics and how probable they will consume more services from the bank. 

Now, you and your team have been hired by a bank to get to know their customers. In other words, you will implement hashing and clustering techniques to extract relevant information and highlights from those clients and their transactions.

Then, let's get started!

# VERY VERY IMPORTANT!

1. !!! Read the entire homework before coding anything!!!

2. My solution is not better than yours, and yours is not better than mine. A data-driven analysis does not have a unique way of solving a problem. For this reason, it is crucial (necessary and mandatory) that you describe any single decision you take and all the steps you follow.

3. Once performed any exercise, comments about the obtained results are mandatory. We are not always explicit about where to focus your comments, but we will always want brief sentences about your discoveries and decisions.


## 1. Finding Similar Costumers

Companies nowadays are implementing product suggestions to provide users with things they are likely to buy. The process often starts by finding similar behaviours among consumers; for this task, we will focus on this part in the specific.  
Here you will implement an algorithm to find the most similar match to a consumer given his bank account information. In particular, you will implement your version of the [**LSH algorithm**](https://www.learndatasci.com/tutorials/building-recommendation-engine-locality-sensitive-hashing-lsh-python/) that takes as input information about a consumer and finds people similar to the one in the study.  

### 1.1 Set up the data  

1) To start working download the [banking dataset](https://www.kaggle.com/datasets/shivamb/bank-customer-segmentation) on Kaggle.  

2) For the sake of this first part, not all columns are necessary since comparing each field single handedly can be quite time-expensive. Then, carefully read the linked guide above and try to understand which features will be appropriate for this task (An heads up: some users have more than one transaction record, make sure to handle them all). Once you have finished, project a version of the dataset to work with.

### 1.2 Fingerprint hashing

Using the previously selected data with the features you found pertinent, you have to:

1) Implement your minhash function  **from scratch**. *No ready-made hash functions are allowed*. Read the class material and search the internet if you need to. For reference, it may be practical to look at the description of hash functions in the [book](http://infolab.stanford.edu/~ullman/mmds/ch3n.pdf).

2) Process the dataset and add each record to the MinHash. The subtask's goal is to try and map each consumer to its bin; to ensure this works well, be sure you understand how MinHash works and choose a matching threshold to use. Before moving on, experiment with different thresholds, explaining your choice.

### 1.3 Locality Sensitive Hashing

Now that you prepared your algorithm, it's query time!  
We have prepared some dummy users for you to work with. Download [this csv](...) and report the most similar users (comparing them against the dataset provided in Kaggle). Did your hashing method work properly, and how long did it take to run? Provide information and analysis about the results.


## 2. Grouping customers together!

Now we will deal with clustering algorithms that will provide groups of clients which are similar among them. 

To solve this task, you must accomplish the following stages:

### 2.1 Getting your data + feature engineering

1) Access to the data found in [this dataset](https://www.kaggle.com/datasets/shivamb/bank-customer-segmentation) (it is the same dataset from the previous question 1.1).

2) Sometimes, the features (variables, fields) are not given in a dataset but can be created from it. The previous step is known as *feature engineering*. For example, the original dataset has several transactions done by the same customer. Then, we ask you to group data by the client (using CustomerId) and, based on it, create the following new features **for each** CustomerId: 

      a) Number of transactions

      b) Number of transactions with a balance bigger than 100 USD 

      c) Average amount of the transactions 

      d) Average balance

      e) Average difference between the balance and the transaction amount for each customer (this is mainly known in the banking world as utilisation).

      f) Gender of the customer

      h) Most frequent location of the customer


So, in the end, you should have for each CustomerID seven features.

3) Consider at least 20 additional features that can be generated for each CustomerId. Describe each of them and why you believe they will be helpful. Moreover, add it to the previous dataset (the one with seven features). In the end, you should have for each CustomerID at least 27 features (7 recommended + 20 suggested by you).

      *Hints for feature engineering*:
      
       - Instead of only using the average, you could use other functions such as minimum, maximum, percentiles, etc.
       - Think of adding filters to your features. For instance, in "Number of transactions with balance bigger than 100 USD”, 
         the filter was "bigger than 100 USD". Can you think about other filters, even including other variables?
       - Think of including the information given by the fields transaction date and time in your calculations.
       - Think about getting information from a customer’s birthday, even comparing it to other fields.
       - You could also calculate percentages in your features. Think of a plausible set of percentages worth to be calculated.


### 2.2 Choose your features (variables)!

As you may notice, you have plenty of features to work with now. So, you need to find a way to reduce the dimensionality (reduce the number of variables to work with). You can follow the subsequent directions to achieve it:

1) *To normalise or not to normalise? That's the question*. Sometimes it is worth normalising (scaling) the features. Explain if it is a good idea to perform any normalisation method. If you think the normalisation should be used, apply it to your data (look at the available normalisation functions in the `scikit-learn` library).

2) Select **one** method for dimensionality reduction and apply it to your data. Some suggestions are Principal Component Analysis, Multiple Correspondence Analysis, Singular Value Decomposition, Factor Analysis for Mixed Data, Two-Steps clustering. Make sure that the method you choose applies to the features you have or modify your data to be able to use it. Explain why you chose that method and the limitations it may have.


2) Apply the selected method(s) to your data. Ensure the chosen method retains > 70% of the total variance.

### 2.3 Clustering!

1) Implement the K-means clustering algorithm (**not** ++: random initialization). We ask you to write the algorithm from scratch following what you learned in class. **!!** We also ask you to use MapReduce in your K-means algorithm.

2) Find an optimal number of clusters. Use at least two different methods. If your algorithms provide diverse optimal K's, select one of them and explain why you chose it.

3) Run the algorithm on the data. 

4) Then, use the already implemented version of K-means++ (from the `scikit-learn` library). Explain the differences (if there are any) in the results.

### 2.4 Analysing your results!

You are often encouraged to explain the main characteristics that your clusters have. This is called the *Characterizing Clusters* step. Thus, follow the next steps to do it:

1) Select 2-3 variables you think are relevant to identify the cluster of the customer. For example, CustGender, Number of transactions, etc.

2) Most of your selected variables will be numerical (continuous or discrete), then categorise them into four categories.

3) With the selected variables, perform pivot tables. On the horizontal axis, you will have the clusters, and on the vertical axis, you will have the categories of each variable. Notice that you have to do one pivot table per variable.

4) Calculate the percentage by column for each pivot table. The sum of each row (cluster) must be 100. The sample example for clustering with K = 4 and Gender variable:
<p align="center">
<img src="Pivot.png" width = 200>
</p>

5) Interpret the results for each pivot table.

6) Use any known metrics to estimate clustering algorithm performance (how good are the clusters you found?).




**IMPORTANT NOTE:**

- We know you may consult the internet for information about implementing the requested algorithms. However, the final code must be yours! So please, do not search and copy-paste the code.

- Since we know that some of the previous points can raise many questions, opening a thread on Slack is recommended and welcomed.

- Unfortunately, there are no explicit descriptions of the features in the data sets. Nevertheless, the names are usually self-explanatory. In case you have any doubt, Google will help you better understand the characteristics of a bank's customer.


## Bonus

We remind you that we consider and grade the bonuses only if you complete the entire assignment. 

1) Think about any two other clustering algorithms that you would like to use for the dataset (of course, you can use implemented version of them, e.g. from the `scikit-learn` library). Compare the results of chosen two algorithms with K-means implemented by you and K-means++ (from the scikit-learn library). Explain the differences (if there are any) in the results. Which one is the best, in your opinion, and why?



## Command Line Question
Here is another command line question to enjoy. We previously stated that using the command line tools is a skill that Data Scientists must master.

In this question, you should use any command line tools that you know to answer the following questions using the same dataset that you have been using so far: 
1. Which location has the maximum number of purchases been made?
2. In the dataset provided, did females spend more than males, or vice versa?
3. Report the customer with the highest average transaction amount in the dataset.


__Note:__ You may work on this question in any environment (AWS, your PC command line, Jupyter notebook, etc.), but the final script must be placed in CommandLine.sh, which must be executable.

## Algorithmic Question
An imaginary university wants to restrict its student’s entrance to the campus. Suppose that there are N entrances, M students and G guards. Due to the security measures, each student is known to be assigned a gate through which they should enter the university.

The N entrances will be numbered from 1 to N. Regarding one entry, the entrance will be opened right before the first student’s arrival and closed right after the arrival of the last student that should enter through that specific entrance. We will assume that two students can not enter the university simultaneously. For an entry to be protected, a guard should be assigned to it. Notice that a guard cannot leave his post until the door he was given is closed.

Assume that the university's head of the guards knows the order in which the students are coming to the university (yeah, they know you more than you know about yourself!). He wants you to help him if having only G guards is enough to address the restrictions they wish to apply (in other words, whether there will be a moment when more than G entrances should be opened or not). 

**Input:**

In the first line, you will be given the values of N, M and G, which correspond to the number of entrances to the university, the number of students in the university and the number of guards that the head of the guards intends to use to apply these restrictions respectively.
$$1 \le N \le 10^6$$
$$1 \le M \le 10^3$$
$$1 \le G \le 100$$
In the second line, you will be given M integers which the ith integer corresponds to the entrance that has been assigned to the ith student to enter the university. 

**Ouptut:**

Output “YES” if having G guards is enough to respect the restrictions, and “NO” if it is not enough. 

**Examples:**

__Input 1__
```
4 5 1
1 1 3 3 3
```
__Output 2__
```
YES
```
In this example, we only have one guard in the university. Initially, the guard will be assigned to protect entrance 1'. After the second student arrives, the guard will close access ‘1' and go to entrance '3'. In this case, having only one guard is enough to address the restrictions. 
___

__Input 2__
```
2 5 1 
1 2 1 2 2
```
__Output 2__
```
NO
```





