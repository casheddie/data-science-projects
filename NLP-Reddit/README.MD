Web Scraping and Using NLP to Evaluate Machine Learning Models
---
## Executive Summary 
In this project, we are asked to perform web scraping to collect subreddit posts data of two different subreddits to be used to train a machine learning model to be able to predict the origin of subreddit the posts came from.  I selected the Apple and Samsung subreddits to compare.  This problem can be classified as a binary claissification problem.  The success of the model would be determined by how accurate it performs predicting if a post came from the Apple or the Samsung subreddit by analyzing the text collected from each posts.  A high accuracy score when the model processes data it has not seen be a good indicator if the model is performing well.

## Table of Contents

| Item | Description | Link |
| --- | --- | --- |
| Project Code |  Technical Notebook of Code (Jupyter Notebook)| [Link](https://git.generalassemb.ly/eddie-reed/Submissions/blob/master/project_3/Project-3-NLP-Reddit-Eddie-Reed.ipynb)|
| Data | Collected Data from subreddits of Apple and Samsung | [Link](https://git.generalassemb.ly/eddie-reed/Submissions/blob/master/project_3/data/apple_samsung_posts.csv)|
| Data| Comparison of Actual vs Perdicted posts from Apple and Samsung subreddits| [Link](https://git.generalassemb.ly/eddie-reed/Submissions/blob/master/project_3/data/results_bn.xls)|
|Power Point| NLP Machine Learning Deck|[Link](https://git.generalassemb.ly/eddie-reed/Submissions/blob/master/project_3/Project%203%20NLP.pdf)
---
## Data Collection and EDA
I used the [**`praw`**](https://praw.readthedocs.io/en/latest/index.html) python wrapper to interact with the reddit API to collect the subreddit posts and saved them to a csv file.  I collected a total of 1853 posts between the Apple and Samsung subreddits. The initial thought was to use the title and body sections of the reddit posts to train the models, however, during the EDA phase it was quickly discovered that the in a number of cases, the body section of s post contained images, links to other websites and when that data was brought into a dataframe, there would be large sections of blank space and no text data.  Doing an initial pass of the data through a model yielded that the 'body' section of the reddit submissions would not be very useful for training our model due a large set of the data was blank.  

After futher evaluation of the data, it was determined that the 'title' section of the subreddits would be the best data to use because each row the dataframe contained text data.  

## Preprocessing and Modeling
We were asked to evalute at least two machine learning models to process the text data we collected and determine which one performs the best in predicting the origin of a subreddit post.  We were required to use at least one model from the Naive Bayes model family and we could select any other classification model of our choosing (e.g. logistical regression, Support Vector Machines (SVM), KNN, etc).

Since we are analyzing text data, we had to use Natural Language Processing (NLP) techniques to convert the data into some vectorized format our classifications could understand and process.  We learned about two NLP transformers called CounterVectorize and Term Frequency-Inverse Document Frequency(TFIDF) vectorizer.  Both models will analyzie text data and transform it into sparse vectors that our classification estimators can prcess.  

As in all cases in preparing to model, once cleaning and EDA of the data is completed, it is now ready to be fit into our model.  We split our data into a training and data set using `train_test_split`, fit and score our model on the testing data.  We have several hyperparameters we can tune based on the model we are using to validte and improve our models.  

## Evaluation of the Models
In this project, I selected to use the folling machine learning classification models:

1. `LogisticRegressiom`
2. `BernoulliNB` 
3. `MultinomialNB`
4. `Support Vector Machines`

The two vectoritors I selected where:

1. `CountVectorizer`
2. `TFIDFVectorizer`

Please reference the jupyter notebook linked above for detailed code and comparison of each model  I selected.  The model I determined that had the best overall performance was the `BernoullNB` with using the `CountVectorizer`.  Below are the parameters and scores:

`{'cvec__max_features': 1000,
 'cvec__ngram_range': (1, 2),
 'cvec__stop_words': None}`
 
The accuarcy score using this model was 95% which means the model will be correct 95% of the time in determing the source of s reddit post that either came from Apple or Samsung.

## Conclusion 
I discovered that just the data from the 'title' in each submission was enough to learn how to predeict the correct posts.  The model used was the Bernoulli and the transformer was Countvector.  
