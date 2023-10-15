# Homework 2 - The Best Books of All Time

Books are essential to human life, offering knowledge, escapism, and lifelong companionship. They hold the collective wisdom of humanity, providing insight, inspiration, and an enduring connection to our shared human experience. In this engaging data analysis homework, you'll be (deep) diving into a rich dataset focused on books. Your objective is to extract valuable insights and patterns, exploring genres, authors, publication dates, ratings, and more. You aim to uncover trends and correlations through rigorous analysis and visualization, shedding light on the diverse literature landscape. Join us in this analytical journey as we decode the fascinating world of books using the power of data!

Assume you and your team work for a company that is interested in analyzing all this book data to understand better the evolution of the market of readers and authors throughout history. They want to understand it to make decisions that might affect the success of the so-called company.

Your **goal** is to answer the Research Questions (RQs) that may help discover and interpret meaningful data patterns and eventually understand how readers and authors behave.

![overflowing-bookcases](https://github.com/Sapienza-University-Rome/ADM-TA/blob/master/2023/Homework_2/img/books_pict.jpg)

____

## Before Starting

Among all the numerous things and good practices a Data Scientist needs to do before running any analysis, there is one of uttermost importance: **get the data and understand it**! 

Here, you find the list of tasks you must perform before getting your hands on the actual data and into this world of literature.

* **Get your data!** You must use the files [lighter_authors.json](https://sapienza2023adm.s3.eu-south-1.amazonaws.com/lighter_authors.json) and [lighter_books.json](https://sapienza2023adm.s3.eu-south-1.amazonaws.com/lighter_books.json), which are random samples we draw for you to work with. Notice that the mentioned data is based on [this website](https://www.kaggle.com/datasets/opalskies/large-books-metadata-dataset-50-mill-entries).
* **Understand your data.** Read the name of each file to understand what it refers to, dig into its structure, and read the description on the page where the data is available. Please be sure that you've understood the data before starting coding.
* **Handling the data.** The data are provided in many '.json' files. To answer the RQs, we kindly suggest you look for ways to handle this type of data and then perform the necessary operations based on what you want to analyze.
  
Friendly reminder: **Internet** is your friend, and it may be the source of the answer you may have along this and many other projects!

----

# VERY VERY IMPORTANT
1. **!!! Read the entire homework before coding anything!!!**
2. *My solution is not better than yours, and yours is not better than mine*. In any data analysis task, there **is no** unique way to answer RQs. For this reason, it is crucial (**necessary and mandatory**) that you describe any single decision you take and all your steps.
3. Once solving an exercise, comments about the obtained results are **mandatory**. We are not always explicit about where to focus your comments, but we will always want brief sentences about your discoveries.
4. We encourage using chatGPT (Bard, Bing, or any other Large Language Models (LLM) chatbot tool) as allies to help you solve your homework, and we were hoping you could learn how to use them properly. However, **using such tools when not explicitly allowed will be considered plagiarism and strictly prohibited**. 

____

# Research questions [RQs]

1. [__RQ1__] *Exploratory Data Analysis (EDA)* - Before working on your research questions, you should provide meaningful statistical summaries through visualizations and tabular tools to understand your data.


2. [__RQ2__] *Let’s finally dig into this vast dataset, retrieving some vital information:*
    - Plot the number of books for each author in descending order.
    - Which book has the highest number of reviews?
    - Which are the top ten and ten worst books concerning the average score?
    - Explore the different languages in the book’s dataset, providing a proper chart summarizing how these languages are distributed throughout our virtual library.
    - How many books have more than 250 pages?
    - Plot the distribution of the fans count for the 50 most prolific authors (the ones who have written more books).
3. [__RQ3__] *Let’s have a historical look at the dataset!*

    - Write a function that takes as input a year and returns as output the following information:

       - The number of books published that year.
   
       - The total number of pages written that year.
   
       - The most prolific month of that year.
   
       - The longest book written that year.
   
    - Use this function to build your data frame: the primary key will be a year, and the required information will be the attributes within the row. Finally, show the head and the tail of this new data frame considering the first ten years registered and the last ten years.
   
    - Ask **ChatGPT** or any other LLM chatbot tool to implement this function and compare your work with the one the bot gave you as an answer. Does the chatbot implementation work? Please test it out and verify the correctness of the implementation, explaining the process you followed to prove it. 

4. [__RQ4__] *Quirks questions about consistency*. In most cases, we will not have a consistent dataset, and the one we are dealing with is no exception. So, let's enhance our analysis.
     - You should be sure there are no **eponymous** (different authors who have precisely the same name) in the author's dataset. Is it true?
     -  Write a function that, given a list of author_id, outputs a dictionary where each author_id is a key, and the related value is a list with the names of all the books the author has written.
     -  What is the **longest book title** among the books of the top 20 authors regarding their average rating? Is it the longest book title overall?
     -  What is the shortest overall book title in the dataset? If you find something strange, provide a comment on what happened and an alternative answer.
       
5. [__RQ5__] *We can consider the authors with the most fans to be influential. Let’s have a deeper look.*
   - Plot the top 10 most influential authors regarding their fan count and number of books. Who is the most influential author?
   - Have they published any series of books? If any, extract the longest series name among these authors.
   - How many of these authors have been published in different formats? Provide a meaningful chart on the distribution of the formats and comment on it. 
   - Provide information about the general response from readers (number of fans, average rating, number of reviews, etc.), divide the authors by gender, and comment about anything eventually related to “structural bias.” You may want to have a look at the following recommended readings:
     
         - https://bhm.scholasticahq.com/article/38021
     
         - https://priyanka-ddit.medium.com/how-to-deal-with-imbalanced-dataset-86de86c49
     
         - https://compass.onlinelibrary.wiley.com/doi/10.1111/soc4.12962
     You can even ask ChatGPT or any other LLM chatbot tool: try to formulate a prompt that provides helpful information about it. Put that information in your notebook and provide comments on what you found.
     
6. [__RQ6__] *For this question, consider the top 10 authors concerning the number of fans again.*
   - Provide the average time gap between two subsequent publications for a series of books and those not belonging to a series. What do you expect to see, and what is the actual answer to this question?
   - For each of the authors, give a convenient plot showing how many books has the given author published **UP TO** a given year. Are these authors contemporary with each other? Can you notice a range of years where their production rate was higher?

7. [__RQ7__] *Estimating probabilities is a core skill for a data scientist: show us your best!*
   - Estimate the probability that a book has over 30% of the ratings above 4.
   - Estimate the probability that an author publishes a new book within two years from its last work.
   - In the file [*list.json*](https://www.kaggle.com/datasets/opalskies/large-books-metadata-dataset-50-mill-entries?select=list.json), you will find a peculiar list named **"The Worst Books of All Time."** Estimate the probability of a book being included in this list, knowing it has more than 700 pages.
   - Are the events *X=’Being Included in The Worst Books of All Time list’* and *Y=’Having more than 700 pages’* independent? Explain how you have obtained your answer.

8. [__RQ8__] *Charts, statistical tests, and analysis methods are splendid tools to illustrate your data-driven decisions to check whether a hypothesis is correct.*
   - Can you demonstrate that readers usually rate the longest books as the worst?
   - Compare the average rate distribution for English and non-English books with a proper statistical procedure. What can you conclude about those two groups?
   - About the two groups in the previous question, extract helpful statistics like mode, mean, median, and quartiles, explaining their role in a box plot.
   - It seems reasonable to assume that authors with more fans should have more reviews, but maybe their fans are a bit *lazy*. Confirm or reject this with a convenient statistical test or a predictive model.
   - Provide a short survey about helpful statistical tests in data analysis and mining: focus on hypothesis design and the difference between parametric and nonparametric tests, explaining the reasons behind the choice of one of these two tests.

### Bonus points

**1.**

- Select one alternative library to Pandas (i.e., Dask, Polar, Vaex, Datatable, etc.), upload [authors.json](https://www.kaggle.com/datasets/opalskies/large-books-metadata-dataset-50-mill-entries) dataset, and filter authors with at least 100 reviews. Do the same using Pandas and compare performance in terms of milliseconds.

- Select one alternative library to Pandas (i.e., Dask, Polar, Vaex, Datatable, etc.), upload [books.json](https://www.kaggle.com/datasets/opalskies/large-books-metadata-dataset-50-mill-entries), and join them with [authors.json](https://www.kaggle.com/datasets/opalskies/large-books-metadata-dataset-50-mill-entries) based on author_id. How many books don’t have a match for the author?

**2.** *Every book should have a field named description, and any author should have a field named description. Choose one of the two and perform a text-mining analysis:*

- If you choose to text-mine [**books.json**](https://www.kaggle.com/datasets/opalskies/large-books-metadata-dataset-50-mill-entries) **’ descriptions**, try to find a way to group books in genres using whatever procedure you want, highlighting words that are triggers for these choices.

- If you choose to text-mine [**authors.json**](https://www.kaggle.com/datasets/opalskies/large-books-metadata-dataset-50-mill-entries)**’ about-field**, try to find a way to group authors in genres using whatever procedure you want, highlighting words that are triggers for these choices.

- If you feel comfortable and did **both** tasks, analyze the matching of the two procedures. You grouped books and authors in genres. Do these two procedures show correspondence?
  
# Command Line Question
Using the command line is a feature that Data Scientists must master. It is relevant since the operations there require less memory to use in comparison to other interfaces. It also uses less CPU processing time than other interfaces. In addition, it can be faster and more efficient and handle repetitive tasks quickly.

__Note:__ To answer the question in this section, you must strictly use command line tools. We will reject any other method of response. 

Looking through the files, you can find [series.json](https://www.kaggle.com/datasets/opalskies/large-books-metadata-dataset-50-mill-entries), which contains a list of book series. In each series's <ins>'works'</ins> field, you'll find a list of books that are part of that series. Report the title of the __top 5__ series with the <ins>highest total 'books_count'</ins> among all of their associated books using command line tools. 

1. Write a script to provide this report. Put your script in a shell script file with the appropriate extension, then run it from the command line. The file should be called commandline_original.[put_the_proper extension]
2. Try interacting with ChatGPT or any other LLM chatbot tool to implement a <ins>more robust</ins> script implementation. Your final script should be __at most three lines__. Put your script in a shell script file with the appropriate extension, then run it from the command line. The file should be called commandline_LLM.[put_the_proper_ extension]. Add in your homework how you employed the LLM chatbot tools, validate if it is correct, and explain how you check its correctness.
   
The expected result is as follows: 

|id|title|total_books_count|
|---|---|---|
|302380|Extraordinary Voyages|20138|
|94209|Alice's Adventures in Wonderland|14280|
|311348|Kolekcja Arcydzieł Literatury Światowe|13774|
|41459|Oz|11519|
|51138|Hercule Poirot|11305|


# AWS Question
AWS offers access to many cloud-based tools and services that simplify data processing, storage, and analysis. Thanks to AWS's scalable and affordable solutions, data scientists can work effectively with large datasets and carry out advanced analytics. A data scientist must, therefore, perform the essential task of learning how to use AWS. To complete a straightforward data analysis task in this question, you must set up an environment on Amazon Web Services. 

In this question, you are asked to provide the most commonly used tags for book lists. Going through the [__list.json__](https://www.kaggle.com/datasets/opalskies/large-books-metadata-dataset-50-mill-entries) file, you'll notice that each list has a list of tags attached, and we want to see what are the <ins>most popular tags</ins> across all of the lists. Please report the __top 5__ most frequently used tags and the number of times they appear in the lists.

You have to follow the following (recommended) steps:  
- Download the *list.json* file to your local system. 
- Write a Python script that generates the report and the system's time to generate it.
- Set up an EC2 instance on your AWS account and upload the list.json file together with your script to the instance
- Compare the running times of your script on your local system and the EC2 instances.

__Important note__: Please run the __same script__ on both your local system and your EC2 instance to compare the results. e.g., keep the parameters the same if you are processing the data by loading it partially and aggregating the results. Comment about the differences you find.

Please provide a report as follows: 
- The information about the config of the EC2 instance 
- The command used to connect to the EC2 
- The commands used to upload the files and run the script on the EC2 instance through your local system 
- A table containing the most popular tags and their number of usage
- A table containing the running time of the script on your local system and EC2 instance
  
The following is the expected outcome for the most popular tags:
|tag|#usage|
|---|---|
|romance|6001|
|fiction|5291|
|young-adult|5016|
|fantasy|3666|
|science-fiction|2779|


# Algorithmic Question
Assume you are working as a librarian at a public library in Rome. Some new books have arrived, and you are in charge of putting them on a shelf. Your supervisor will give you some instructions, and you will follow his. Each book has a unique ID, and your boss's instructions can be of the following types: 

- **L N** - place the book with ID = N on the shelf to the left of the leftmost existing book
- **R N** - place the book with ID = N on the shelf to the right of the rightmost existing book
- **? N** - Calculate the minimum number of books you must pop from the left or right to have the book with ID = N as the leftmost or rightmost book on the shelf.
  
You must follow your boss's instructions and report the answers to type 3 instructions to him. He guarantees that if he has a type 3 instruction for a book with a specific ID, the book has already been placed on the shelf. 

Remember that once you've answered a type 3 instruction, the order of the books <ins>does not change</ins>. 

**Input:**

The first line contains a single number, n, representing the number of your boss's instructions. The ith instruction the boss gives can be found at each of the following n lines. 

**Output:**

Print your boss's type 3 instructions in the order they appear in the input. 

**Examples:**

__Input 1__
```
L 75
R 20
R 30
L 11
? 75
L 12
L 15
? 20
```
__Output 1__
```
1
1
```
---
__Input 2__
```
R 1
L 2
L 3
L 4
? 3
R 5
R 6
L 7
L 8
? 4
L 9
R 10
R 11
L 12
L 13
? 11
? 3
```
__Output 2:__
```
1
2
0
6
```

1. Implement a code to answer the problem above. 

2. Ask ChatGPT or any other LLM chatbot tool to check your code's time complexity (the Big O notation). Do you believe this is correct? How can you double-check it? Elaborate about your answer.

3. Is the algorithm proposed in (1.) the __optimal__ one to produce the required output? If not, can you suggest a <ins>better algorithm</ins> to perform the same task?
   

