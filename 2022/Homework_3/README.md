# Homework 3 - Places of the world
<p align="center">
<img src="img/places.png" width = 600>
</p>

Travelling is a pleasant activity which has increased since the end of the COVID-19 pandemic. Nowadays, people look for places to visit which are attractive, affordable, with a rich history and which have recommended activities. Using user-generated content, [Atlas Obscura](https://www.atlasobscura.com/), an American online magazine and travel firm, catalogues unusual and obscure tourist locations. The website's articles span many subjects, including history, science, cuisine, and unique places.

You and your team have been hired to provide your *Data Science knowledge* to create a **search engine** which will facilitate specific searches towards a *topic* related to the most popular places to visit. **Important:** All the functions must be implemented from scratch unless differently specified.

Then, let's get started!

## 1. Data collection

For this homework, there is no provided dataset. Instead, you have to build your own. Your search engine will run on text documents. So, here
we detail the procedure to follow for the data collection. 

### 1.1. Get the list of places

We start with the list of places to include in your corpus of documents. In particular, we focus on the [Most popular places](https://www.atlasobscura.com/places?sort=likes_count). Next, we want you to **collect the URL** associated with each site in the list from this list.
The list is long and split into many pages. Therefore, we ask you to retrieve only the URLs of the places listed in **the first 400 pages** (each page has 18 places, so that you will end up with 7200 unique place URLs).

The output of this step is a `.txt` file whose single line corresponds to the place's URL.

### 1.2. Crawl places

Once you get all the URLs in the first 400 pages of the list, you:

1. Download the HTML corresponding to each of the collected URLs.
2. After you collect a single page, immediately save its `HTML` in a file. In this way, if your program stops for any reason, you will not lose the data collected up to the stopping point.
3. Organize the entire set of downloaded `HTML` pages into folders. Each folder will contain the `HTML` of the places on page 1, page 2, ... of the list of locations.

__Tip__: Due to a large number of pages you should download, you can use some methods that can help you shorten the time it takes. If you employed a particular process or approach, kindly describe it.
 
### 1.3 Parse downloaded pages

At this point, you should have all the HTML documents about the places of interest, and you can start to extract the places' information. The list of the information we desire for each place and their format is as follows:

1. Place Name (to save as `placeName`): String.
2. Place Tags (to save as `placeTags`): List of Strings.
3. \# of people who have been there (to save as `numPeopleVisited`): Integer.
4. \# of people who want to visit the place(to save as `numPeopleWant`): Integer.
5. Description (to save as `placeDesc`): String. Everything from under the first image up to "know before you go" (orange frame on the example image).
6. Short Description (to save as `placeShortDesc`): String. Everything from the title and location up to the image (blue frame on the example image).
7. Nearby Places (to save as `placeNearby`): Extract the names of all nearby places, but only keep unique values: List of Strings.
8. Address of the place(to save as `placeAddress`): String.
9. Altitude and Longitude of the place's location(to save as `placeAlt` and `placeLong`): Floats
10. The username of the post editors (to save as `placeEditors`): List of Strings.
11. Post publishing date (to save as `placePubDate`): datetime.
12. The names of the lists that the place was included in (to save as `placeRelatedLists`): List of Strings.
13. The names of the related places (to save as `placeRelatedPlaces`): List of Strings.
14. The URL of the page of the place (to save as `placeURL`):String
<p align="center">
<img src="img/last_version_place.png" width = 1000>
</p>


For each place, you create a `place_i.tsv` file of this structure:

```
placeName \t placeTags \t  ... \t placeURL
```

If an information is missing, you just leave it as an empty string.


## 2. Search Engine

Now, we want to create two different Search Engines that, given as input a query, return the places that match the query.

First, you must pre-process all the information collected for each place by:

1. Removing stopwords
2. Removing punctuation
3. Stemming
4. Anything else you think it's needed

For this purpose, you can use the [nltk library](https://www.nltk.org/).

### 2.1. Conjunctive query
For the first version of the search engine, we narrow our interest to the __description__ of each place. It means that you will evaluate queries only concerning the place's description.

__Note__: You should use the longer description `placeDesc` column and not the short description `placeShortDesc`. 

### 2.1.1) Create your index!

Before building the index, 
* Create a file named `vocabulary`, in the format you prefer, that maps each word to an integer (`term_id`).

Then, the first brick of your homework is to create the Inverted Index. It will be a dictionary in this format:

```
{
term_id_1:[document_1, document_2, document_4],
term_id_2:[document_1, document_3, document_5, document_6],
...}
```
where _document\_i_ is the *id* of a document that contains that specific word.

__Hint:__ Since you do not want to compute the inverted index every time you use the Search Engine, it is worth thinking about storing it in a separate file and loading it in memory when needed.

#### 2.1.2) Execute the query
Given a query input by the user, for example:

```
american museum
```

The Search Engine is supposed to return a list of documents.

##### What documents do we want?
Since we are dealing with conjunctive queries (AND), each returned document should contain all the words in the query.
The final output of the query must return, if present, the following information for each of the selected documents:

* `placeName`
* `placeDesc`
* `placeURL`

__Example Output__:

<p align="center">
<img src="img/output1_ex.png" width = 800>
</p>

If everything works well in this step, you can go to the next point and make your Search Engine more complex and better at answering queries.


### 2.2) Conjunctive query & Ranking score

For the second search engine, given a query, we want to get the *top-k* (the choice of *k* it's up to you!) documents related to the query. In particular:

* Find all the documents that contain all the words in the query.
* Sort them by their similarity with the query.
* Return in output *k* documents, or all the documents with non-zero similarity with the query when the results are less than _k_. You __must__ use a heap data structure (you can use Python libraries) for maintaining the *top-k* documents.

To solve this task, you must use the *tfIdf* score and the _Cosine similarity_. The field to consider is still the `placeDesc`. Let's see how.


#### 2.2.1) Inverted index
Your second Inverted Index must be of this format:

```
{
term_id_1:[(document1, tfIdf_{term,document1}), (document2, tfIdf_{term,document2}), (document4, tfIdf_{term,document4}), ...],
term_id_2:[(document1, tfIdf_{term,document1}), (document3, tfIdf_{term,document3}), (document5, tfIdf_{term,document5}), (document6, tfIdf_{term,document6}), ...],
...}
```

Practically, for each word, you want the list of documents in which it is contained and the relative *tfIdf* score.

__Tip__: *TfIdf* values are invariant for the query. Due to this reason, you can precalculate and store them accordingly.

#### 2.2.2) Execute the query

In this new setting, given a query, you get the proper documents (i.e., those containing all the query's words) and sort them according to their similarity to the query. For this purpose, as the scoring function, we will use the Cosine Similarity concerning the *tfIdf* representations of the documents.

Given a query input by the user, for example:
```
american museum
```
The search engine is supposed to return a list of documents, __ranked__ by their Cosine Similarity to the query entered in the input.

More precisely, the output must contain:
* `placeName`
* `placeDesc`
* `placeURL`
* The similarity score of the documents with respect to the query (float value between 0 and 1)


__Example Output__:
<p align="center">
<img src="img/output2_ex.png" width = 800>
</p>




## 3. Define a new score!

Now it's your turn. Build a new metric to rank places based on the queries of their users.

In this scenario, a single user can give input more information than a single textual query, so you need to consider all this information and think of a creative and logical way to answer the user's requests.

Practically:

1. The user will enter a text query. As a starting point, get the query-related documents by exploiting the search engine of Step 3.1.
2. Once you have the documents, you need to sort them according to your new score. In this step, you won't have any more to take into account just the plot of the documents; you __must__ use the remaining variables in your dataset (or new possible variables that you can create from the existing ones). You __must__ use a heap data structure (you can use Python libraries) for maintaining the *top-k* documents.

    > __Q:__ How to sort them?
    __A:__ Allow the user to specify more information that you find in the documents and define a new metric that ranks the results based on the new request. You can also use other information regarding the place to score some places above others.
   
__N.B.:__ You have to define a __scoring function__, not a filter! 

The output, must contain:

* `placeName`
* `placeDesc`
* `placeURL`
* The  __new__ similarity score of the documents with respect to the query

Are the results you obtain better than with the previous scoring function? **Explain and compare results**.

## 4. Visualizing the most relevant places

Using maps can help people understand how far one place is from another so they can plan their trips more adequately. Here we challenge you to show a map with the places found with the score defined in point 3. Ensure you can at least identify and visualize the *name*, *city*, *country*, *address* and the *number of people who visited* each place. You can find some ideas on how to create maps in Python [here](https://plotly.com/python/maps/) and [here](https://towardsdatascience.com/visualizing-geospatial-data-in-python-e070374fe621) but don't limit yourselves, let your minds fly!!

## 5. BONUS: More complex search engine 

__IMPORTANT:__ This is a bonus step, so it's <ins>not mandatory</ins>. You can get the maximum score also without doing this. We will take this into account, **only if** the rest of the homework has been completed.

For the Bonus part, we want to ask you more sophisticated search engine. Here we want to let users issue more complex queries. The options of this new search engine are: 
1. Give the possibility to specify queries for the following features (the user should have the option to issue __none or all of them__): 
 - `placeName`
 - `placeDesc`
 - `placeAddress`
2. Specify a list of __usernames__ to only retrieve the posts that <ins>all</ins> of these users contributed to.
3. Specify a list of __tags__ which the search engine should only return the places that are tagged with <ins>all</ins> of those tags.
4. Filter based on the number of people who have already been there. The user should be able __to adjust__ the <ins>upperbound</ins>, <ins>lowerbound</ins> or only one of the two. 
5. Specify a list of the __list names__ that the engine should only filter the documents that have been included in <ins>all</ins> of the given list names.

__Note 1__: You should be aware that you should give the user the possibility <ins>to select any</ins> of the abovementioned options. How should the user use the options? We will accept __any manual__ that you provide to the user. 

__Note 2__: As you may have realized from __1st option__, you need to build <ins>inverted indexes</ins> for those values and return all of the documents that have the similarity <ins>more than 0</ins> concerning the given queries. Choose a __logical__ way to aggregate the similarity coming from each of them and explain your idea in detail.

__Note 3__: The options <ins>other than 1st</ins> one can be considered as __filtering criteria__ so the retrieved documents <ins>must respect all</ins> of those filters. 

The output must contain the following information about the places:

* `placeName`
* `placeURL`

## 6. Command line question 
As done in the previous assignment, we encourage using the command as a feature that Data Scientists must master. 

In this question, you should use command line tools such as ```grep``` (or any other commands) to answer the following question: 
- For the countries Italy, Spain, France, England, and the United States, report the following (using the information scraped in point 1.3): 
  1. How many places can be found in each country?
  2. How many people, on average, have visited the places in each country?
  3. How many people in total want to visit the places in each country? 

__Note:__ You may work on this question in any environment (AWS, your PC command line, Jupyter notebook, etc.), but the final script must be placed in CommandLine.sh, which must be executable.

## 7. Theoretical question
An imaginary university is interested in accepting some of the applicants for positions to study the Master of Data Science there. Unfortunately, only a few spots are available, so the university requires students to take some exams. Students are then admitted based on how well they perform on these exams. For students to determine whether they have been successfully accepted to the university, the university wants to create a ranking list that includes every student's first name, last name, and total average on its course webpage. Students should be ranked in the list based on their average points in descending order. For example, if two students have the same average punctuation, they should be sorted in ascending order using their first and last names. University will give you the students' information in __'ApplicantsInfo.txt'__ ([click here to download](https://adm2022.s3.amazonaws.com/ApplicantsInfo.txt)), and you should provide them with the ranking list in another *.txt* file and name it as __'RankingList.txt'__ . Kindly help this university in preparing this ranking list.

**Input:** 
__'ApplicantsInfo.txt'__ will have the following format: 
- In the first line, you will be given *n* as the number of applicants and *m* as the number of exams that students have taken (all of them have taken the same exams), where: 
$$0 \lt n \le 5 * 10^4$$
$$1 \le m \le 10^3$$
- In each following *n* lines, you will find the information related to one of the students. Their first name, last name and *m* integers as the grades they received in *m* courses. 
 
**Output:**
The output file should consist of __n__ lines, with each line representing one of the students and including the student's __first name, last name, and total average point__(setting the precision to 2 decimal points). As you know, they must be sorted in the order specified in the problem description. 

**Examples:** 

__Input 1__
```
10 3
Emily Morris 27 22 27
Maria Choute 24 18 21
Maura Lara 27 22 18
Daniel Falgoust 28 29 24
Henrietta Kaul 27 29 30
Devin Lee 23 21 27
Anne Ortega 21 24 23
Robert Wasserman 29 28 21
Sue Csaszar 21 25 25
Rebecca Lachner 23 30 30
```
__Output 1__
```
Henrietta Kaul 28.67
Rebecca Lachner 27.67
Daniel Falgoust 27.0
Robert Wasserman 26.0
Emily Morris 25.33
Devin Lee 23.67
Sue Csaszar 23.67
Anne Ortega 22.67
Maura Lara 22.33
Maria Choute 21.0
```
___

__Input 2__
```
5 6
Ralph Broadus 29 22 27 27 19 30
Patricia Melancon 18 22 30 25 23 27
Robert Watson 21 18 30 19 28 22
Matthew Longsdorf 26 19 28 30 21 30
Linda Allison 29 25 21 24 25 28
```
__Output 2__
```
Matthew Longsdorf 25.67
Ralph Broadus 25.67
Linda Allison 25.33
Patricia Melancon 24.17
Robert Watson 23.0
```
___

1. Try solving the problem mentioned above using three different sorting algorithms (do not use any MapReduce algorithm). (__Note:__ Built-in Python functions (like .mean, .sort, etc.) are not allowed to be used. You must implement the algorithms from scratch).
2. What is the time complexity of each algorithm you have used?
3. Evaluate the time taken for each of your implementations to answer the query stored in the __ApplicantsInfo.txt__ file and visualize them.
4. What is the most optimal algorithm, in your opinion, and why?
5. Implement a sorting algorithm using MapReduce and compare it against the three algorithms previously implemented using the __ApplicantsInfo.txt__ file.

**Have fun!**

