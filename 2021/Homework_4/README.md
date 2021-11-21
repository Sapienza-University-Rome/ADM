# Homework 4 - Hard coding

![alt text](https://scontent-fco2-1.xx.fbcdn.net/v/t1.6435-9/p640x640/184205866_309950770525058_7072329262818108856_n.jpg?_nc_cat=101&ccb=1-5&_nc_sid=e3f864&_nc_ohc=NV-BDW8fI68AX-nKfZT&_nc_ht=scontent-fco2-1.xx&oh=d9a93541fee5ec4b8999dcaac221d921&oe=61AE1128)

# VERY VERY IMPORTANT!

1. !!! Read the entire homework before coding anything!!!

2. My solution it's not better than yours, and yours is not better than mine. In any data analysis task, there is not a unique way to solve a problem. For this reason, it is crucial (necessary and mandatory) that you describe any single decision you take and all the steps you do.

3. Once performed any exercise, comments about the obtained results are mandatory. We are not always explicit about where to focus your comments, but we will always want some brief sentences about your discoveries and decisions.


## 1. Implementing your own Shazam 

[Shazam](https://www.shazam.com/) is a great application that can tell you the title of a song by listening to a short sample. For this task, you will implement a simplified copy of this app by dealing with hashing algorithms. In particular, you will implement your [**LSH algorithm**](https://www.learndatasci.com/tutorials/building-recommendation-engine-locality-sensitive-hashing-lsh-python/) that takes as input an audio track and finds relevant matches.

![myshazam](https://www.codeproject.com/KB/WPF/duplicates/conceptialoverview.png)

### 1.1 Getting your data!

1) Download the [dataset](https://www.kaggle.com/dhrumil140396/mp3s32k) from Kaggle. 

2) We have prepared some query songs which we would like to know the title of. You can download them from here:
- [query1](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/queries/track1.wav)
- [query2](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/queries/track2.wav)
- [query3](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/queries/track3.wav)
- [query4](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/queries/track4.wav)
- [query5](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/queries/track5.wav)
- [query6](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/queries/track6.wav)
- [query7](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/queries/track7.wav)
- [query8](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/queries/track8.wav)
- [query9](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/queries/track9.wav)
- [query10](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/queries/track10.wav)

3) Now you can convert the tracks in the dataset from mp3 format to wav format. We have prepared some utility functions for this. Read the instructions in point 1.2.

### 1.2 Fingerprint hashing
We want to create a representation of our audio signal that allows us to characterize it with respect to its peaks. If you are new to audio signal processing, we recommend that you read [this introductory article](https://willdrevo.com/fingerprinting-and-audio-recognition-with-python/). It will allow you to understand this task much better. Once this process is complete, we can adopt a hashing function to get a fingerprint of each song.

To help you in the extraction phase of the audio signal we have written some utility functions for you that you can find in `AudioSignals.ipynb`. To use them you will need to install (FFMPEG)[https://www.ffmpeg.org/] and [Librosa](https://librosa.org/doc/latest/index.html) in your environment. Of course, you are free to experiment and try any other audio representation you think is best. Now it's your turn!

1) Implement your minhash function  **from scratch**. *No ready-made hash functions are allowed*. Read the class material and search the internet if you need to. As a reference, it may be useful to look at the description of hash functions in the [book](http://infolab.stanford.edu/~ullman/mmds/ch3n.pdf).

2) Read the dataset sequentially and add it to your MinHash. The aim is to make your minhash function map the same song to the same bins. You can define a threshold to control the accuracy of these matches. For example, if you want your app to suggest songs similar to the query one, you can vary the threshold accordingly. Experiment with at least 3 different values and report the results.

3) You are given 10 *query tracks*, report their title!


## 2. Grouping songs together!

We play with a dataset gathering songs from the International Society for Music Information Retrieval Conference. The tracks (songs) include much information. We focus on the **track information**, **features** (extracted with [librosa](https://librosa.org/)  library from Python) and **audio variables** provided by Echonest (now Spotify). 

*The final goal is to group songs into similar genres, therefore **DO NOT** use the feature genre in your k-means anaylsis*

To solve this task, you must accomplish the next stages:

### 2.1 Getting your data!

1) Access to the data can be found here:

 - [echonest.csv](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/echonest.csv)
 - [features.csv](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/features.csv)
 - [tracks.csv](https://sapienza2021adm.s3.eu-south-1.amazonaws.com/hw4/tracks.csv)

2) Data Scientists are often challenged to do Data Wrangling. The latter is a process of cleaning and unifying messy and complex data sets for easy access and analysis ([see more info here](https://www.altair.com/what-is-data-wrangling/)). You are supposed to create one single data set by merging **tracks.csv**, **features.csv** and **echonest.csv**. It's your job to find the correct *key* to join your data sets together. You should end up with a data set of ~13K rows.

### 2.2 Choose your features (variables)!

As you may notice, you have plenty of features to work with. So, you need to find a way to reduce the dimensionality (reduce the number of variables to work with). You can follow the next directions to achieve it:

1) Select **one** method for dimensionality reduction and apply it to your data. Some suggestions are Principal Component Analysis, Multiple Correspondence Analysis, Singular Value Decomposition, Factor Analysis for Mixed Data, Two-Steps clustering. Make sure that the method you choose is applicable for the features you have or modify your data to be able to use it. Explain why you chose that method and the limitations it may have.

HINT: We don't want to miss relevant variables like song's duration, language, etc., after the dimensionality reduction. To keep those variables, you can apply the dimensionality reduction method(s) on features coming from the same file. Later you can stack them with the variables selected from another file.

2) Apply the selected method(s) to your data. Make sure that the chosen method retains > 70% of the total variance. 

### 2.3 Clustering!

1) Implement the K-means clustering algorithm (**not** ++: random initialization). We ask you to write the algorithm from scratch following what you learned in class. 

2) Find an optimal number of clusters. Use at least two different methods. In case that your algorithms provide different optimal K's, select one of them and explain why you chose it.

3) Run the algorithm on the data that you got from the dimensionality reduction. 

4) Then, use the already implemented version of k-means++ (from the scikit-learn library). Explain the differences (if there are any) in the results.

### 2.4 Analysing your results!

You are often encouraged to explain what are the main characteristics that your clusters have. This is called the *Characterizing Clusters* step. Thus, follow the next steps to do it:

1) Select 5-10 variables (from the ones that you had before doing the dimensionality reduction step) you think are relevant to identify the genre of a song. For example, Duration, Language, Country, etc.

2) If any of your selected variables are numerical (continuous or discrete), then categorize them into 4 categories.

3) With the selected variables, perform pivot tables. On the horizontal axis, you will have the clusters, and on the vertical axis, you will have the categories of each variable. Notice that you have to do one pivot table per variable.

4) Calculate the percentage by column for each pivot table. It means that the sum of each column (cluster) must be 1. See the next example for the variable "*Song's Continent*" with a hypothetical K = 4:

![cross_table](img/cross_table.jpeg)

5) Interpret the results for each pivot table.

6) Now, it's time to compare the obtained clusters to the reality genre. Us it to answer what is the most representative genre for each one of the clusters?. You can answer this using the same methodology proposed in step 4th.

7) Execute your K-means++ Analysis again, but don't use the variables from **echonest.csv**. It will leave you with ~100K songs. Focus on getting the following results:
    - Perform the dimensionality reduction.
    - Find the optimal number of clusters.
    - Characterize your clusters using 5-10 variables.
	- Compare your results with those of the previous exercise. If you could choose, would you rather collect more observations (with fewer features) or fewer observations (with more features) based on the previous analyses?


**IMPORTANT NOTE:**

- We are aware that you may consult the internet for information about implementing the requested algorithms. However, the final code must be yours! So please, do not search and copy-paste the code.

- Since we know that some of the previous points can raise many questions, opening a thread on Slack is recommended and welcomed.

- Unfortunately, there are no explicit descriptions of the features included in the data sets. Nevertheless, the names are usually self-explanatory. In case you have any doubt, Google will help you a lot to better understand the features of a song.

## Bonus

We remind you that we consider and grade the bonuses only if you complete the entire assignment. 

1) Implement the K-means algorithm using MapReduce.

## 3. Algorithmic questions

You are given a list of integers, *A*, and another integer *s*. Write an algorithm that outputs all the pairs in *A* that equal *x*.

For example, if
```
A = [7, -2, 8, 2, 6, 4, -7, 2, 1, 3, -3] and s = 4
```
the algorithm should output: `(7, -3), (-2, 6), (2, 2), (3, 1)`.
