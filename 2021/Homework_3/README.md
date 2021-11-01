# Homework 3 - What is the best anime in the world?

<p align="center">
<img src="https://ilovevg.it/wp-content/uploads/2020/05/anime-e-manga-generi.jpg">
</p>

**Goal of the homework**: Build a search engine over the "Top Anime Series" from the list of [MyAnimeList](https://myanimelist.net/). Unless differently specified, all the functions must be implemented from scratch.


## 1. Data collection

For this homework, there is no provided dataset, instead you have to build your own. Your search engine will run on text documents. So, here
we detail the procedure to follow for the data collection. 

### 1.1. Get the list of animes

We start from the list of animes to include in your corpus of documents. In particular, we focus on the [top animes ever list](https://myanimelist.net/topanime.php). From this list we want to **collect the url** associated to each anime in the list.
The list is long and splitted in many pages. We ask you to retrieve only the urls of the animes listed in the first 400 pages (each page has 50 animes so you will end up with 20000 unique anime urls).

The output of this step is a `.txt` file whose single line corresponds to an anime's url.

### 1.2. Crawl animes

Once you get all the urls in the first 400 pages of the list, you:

1. Download the html corresponding to each of the collected urls.
2. After you collect a single page, immediately save its `html` in a file. In this way, if your program stops, for any reason, you will not lose the data collected up to the stopping point. More details in **Important (2)**. 
3. Organize the entire set of downloaded `html` pages into folders. Each folder will contain the `htmls` of the animes in page 1, page 2, ... of the list of animes.


#### Important
*Due to the large amount of pages you need to download, follow the next tips that will help you speeding up several time-consuming operations.*

1. **[Save time downloading files]** You are asked to crawl a considerable number of pages, which will take plenty of time. To speed up the operation, we suggest you to work in parallel with your group's colleagues or even generate code that works in parallel with all the CPUs available in your computer. In particular, using the same code, each component of the group can be in charge of downloading a subset of pages (e.g., the first 100). **PAY ATTENTION:** Once obtained all the pages, merge your results into an unique dataset. In fact, the search engine must look up for results in the whole set of documents.

2. **[Save your data]** It is not nice to restart a crawling procedure, given its runtime. For this reason, it is extremely important that for every time you crawl a page, you **must** save it with the name `article_i.html`, where `i` corresponds to the number of articles you have already downloaded. In such way, if something goes bad, you can restart your crawling procedure from the *i+1*-th document.
 
### 1.3 Parse downloaded pages

At this point, you should have all the html documents about the animes of interest and you can start to extract the animes informations. The list of information we desire for each anime and their format is the following:

1. Anime Name (to save as `animeTitle`): String
2. Anime Type (to save as `animeType`): String
3. Number of episode (to save as `animeNumEpisode`): Integer
4. Release and End Dates of anime (to save as `releaseDate` and `endDate`): Convert both release and end date into datetime format.
5. Number of members (to save as `animeNumMembers`): Integer
6. Score (to save as `animeScore`): Float
7. Users (to save as `animeUsers`): Integer
8. Rank (to save as `animeRank`): Integer
9. Popularity (to save as `animePopularity`): Integer
10. Synopsis (to save as `animeDescription`): String
11. Related Anime (to save as `animeRelated`): Extract all the related animes, but only keep unique values and those that have a hyperlink associated to them. List of strings.
12. Characters (to save as `animeCharacters`): List of strings.
13. Voices (to save as `animeVoices`): List of strings
14. Staff (to save as `animeStaff`): Include the staff name and their responsibility/task in a list of lists.

![Example Anime](img/anime.jpg)


For each anime, you create an `anime_i.tsv` file of this structure:

```
animeTitle \t animeType \t  ... \t animeStaff
```

If an information is missing, you just leave it as an empty string.


__Example__:
  
```
animeTitle \t animeType \t  ... \t animeStaff
    
Fullmetal Alchemist: Brotherhood \t TV \t ... \t [['Cook, Justin', 'Producer'], ['Irie, Yasuhiro', 'Director, Episode Director, Storyboard'], ['Yonai, Noritomo', 'Producer'], ['Mima, Masafumi', 'Sound Director']]
```


## 2. Search Engine

Now, we want to create two different Search Engines that, given as input a query, return the animes that match the query.

First, you must pre-process all the information collected for each anime by:

1. Removing stopwords
2. Removing punctuation
3. Stemming
4. Anything else you think it's needed

For this purpose, you can use the [nltk library](https://www.nltk.org/).

### 2.1. Conjunctive query
For the first version of the search engine, we narrow our interest on the `Synopsis` of each anime. It means that you will evaluate queries only with respect to the anime's description.

#### 2.1.1) Create your index!

Before building the index, 
* Create a file named `vocabulary`, in the format you prefer, that maps each word to an integer (`term_id`).

Then, the first brick of your homework is to create the Inverted Index. It will be a dictionary of this format:

```
{
term_id_1:[document_1, document_2, document_4],
term_id_2:[document_1, document_3, document_5, document_6],
...}
```
where _document\_i_ is the *id* of a document that contains the word.

__Hint:__ Since you do not want to compute the inverted index every time you use the Search Engine, it is worth to think to store it in a separate file and load it in memory when needed.

#### 2.1.2) Execute the query
Given a query, that you let the user enter:

```
saiyan race
```

the Search Engine is supposed to return a list of documents.

##### What documents do we want?
Since we are dealing with conjunctive queries (AND), each of the returned documents should contain all the words in the query.
The final output of the query must return, if present, the following information for each of the selected documents:

* `animeTitle`
* `animeDescription`
* `Url`

__Example Output__:

| animeTitle | animeDescription | Url |
|:-----------------------------:|:-----:|:------------------------------------------------------------:|
| Fullmetal Alchemist: Brotherhood | ... | https://myanimelist.net/anime/5114/Fullmetal_Alchemist__Brotherhood |
| Gintama | ... | https://myanimelist.net/anime/28977/Gintama%C2%B0 |
| Shingeki no Kyojin Season 3 Part 2 | ... | https://myanimelist.net/anime/38524/Shingeki_no_Kyojin_Season_3_Part_2 |

If everything works well in this step, you can go to the next point, and make your Search Engine more complex and better in answering queries.


### 2.2) Conjunctive query & Ranking score

For the second search engine, given a query, we want to get the *top-k* (the choice of *k* it's up to you!) documents related to the query. In particular:

* Find all the documents that contains all the words in the query.
* Sort them by their similarity with the query.
* Return in output *k* documents, or all the documents with non-zero similarity with the query when the results are less than _k_. You __must__ use a heap data structure (you can use Python libraries) for maintaining the *top-k* documents.

To solve this task, you will have to use the *tfIdf* score, and the _Cosine similarity_. The field to consider it is still the synopsis. Let's see how.


#### 2.2.1) Inverted index
Your second Inverted Index must be of this format:

```
{
term_id_1:[(document1, tfIdf_{term,document1}), (document2, tfIdf_{term,document2}), (document4, tfIdf_{term,document4}), ...],
term_id_2:[(document1, tfIdf_{term,document1}), (document3, tfIdf_{term,document3}), (document5, tfIdf_{term,document5}), (document6, tfIdf_{term,document6}), ...],
...}
```

Practically, for each word you want the list of documents in which it is contained in, and the relative *tfIdf* score.

__Tip__: *tfIdf* values are invariant with respect to the query, for this reason you can precalculate and store them accordingly.

#### 2.2.2) Execute the query

In this new setting, given a query you get the right set of documents (i.e., those containing all the words in the query) and sort them according to their similairty to the query. For this purpose, as scoring function we will use the Cosine Similarity with respect to the *tfIdf* representations of the documents.

Given a query, that you let the user enter:
```
saiyan race
```
the search engine is supposed to return a list of documents, __ranked__ by their Cosine Similarity with respect to the query entered in input.

More precisely, the output must contain:
* `animeTitle`
* `animeDescription`
* `Url`
* The similarity score of the documents with respect to the query (float value between 0 and 1)


__Example Output__:

| animeTitle | animeDescription | Url | Similarity |
|:-------------------------------------:|:-----:|:---------------------------------------------------------------------:|------------|
| Fullmetal Alchemist: Brotherhood | ... | https://myanimelist.net/anime/5114/Fullmetal_Alchemist__Brotherhood | 0.96 |
| Gintama | ... | https://myanimelist.net/anime/28977/Gintama%C2%B0 | 0.92 |
| Shingeki no Kyojin Season 3 Part 2 | ... | https://myanimelist.net/anime/38524/Shingeki_no_Kyojin_Season_3_Part_2 | 0.87 |


## 3. Define a new score!

Now it's your turn. Build a new metric to rank animes based on the queries of their users.

In this scenario, a single user can give in input more information than the single textual query, so you need to take into account all this information, and think a creative and logical way on how to answer at user's requests.

Practically:

1. The user will enter you a text query. As a starting point, get the query-related documents by exploiting the search engine of Step 3.1.
2. Once you have the documents, you need to sort them according to your new score. In this step you won't have anymore to take into account just the `plot` of the documents, you __must__ use the remaining variables in your dataset (or new possible variables that you can create from the existing ones...). You __must__ use a heap data structure (you can use Python libraries) for maintaining the *top-k* documents.

    > __Q:__ How to sort them?
    __A:__ Allow the user to specify more information, that you find in the documents, and define a new metric that ranks the results based on the new request. You can also use other information  regarding the anime to score some animes above others.
   
__N.B.:__ You have to define a __scoring function__, not a filter! 

The output, must contain:

* `animeTitle`
* `animeDescription`
* `Url`
* The  __new__ similarity score of the documents with respect to the query

Are the results you obtain better than with the previous scoring function. **Explain and compare results**.



## 4. BONUS: Understanding the anime's reviews

__IMPORTANT:__ This is a bonus step, so it's not mandatory. You can get the maximum score also without doing this. We will take this into account, **only if** the rest of the homework has been completed.

For the bonus question, you will be performing a simple sentiment analysis on the anime website. To do the latter, you will need the following instructions:
- You need to extract one additional feature taken from the *Reviews* section. It will be composed of the 3 first lines of each review (approximately 500 characters). Besides, you should take into account only the first 5 reviews for each anime. For example, for "Fullmetal Alchemist: Brotherhood", you are expected to retrieve the information highlighted in the next figure:

![Example Anime](img/reviews.PNG)

- Given the previous string of words, execute a sentiment analysis on them. Explain how you performed this analysis in detail, including any preprocessing, the type of model/models used, etc. (please bear in mind that you can use pre-trained models for this task).
- Report the results of your sentiment analysis, for example:
	- What Anime Type are the most popular based on your analysis?
	- Does the number of episodes has any impact on the sentiment of the users?
	- Is your sentiment analysis in line with the scores of the animes? Explain your conclusions.
	- Any further analysis of your choice.

## 5. Algorithmic question
You consult for a personal trainer who has a *back-to-back sequence* of requests for appointments. A sequence of requests is of the form
    > 30, 40, 25, 50, 30, 20
where each number is the time that the person who makes the appointment wants to spend.
You need to accept some requests, however you need a break between them, so you cannot accept two consecutive requests. For example, `[30, 50, 20]` is an acceptable solution (of duration *100*), but `[30, 40, 50, 20]` is not, because *30* and *40* are two consecutive appointments. Your goal is to provide to the personal trainer a schedule that maximizes the total length of the accepted appointments. For example, in the previous instance, the optimal solution is `[40, 50, 20]`, of total duration *110*.
1. Write an algorithm that computes the acceptable solution with the longest possible duration.
2. Implement a program that given in input an instance in the form given above, gives the optimal solution.

**Have fun!**
