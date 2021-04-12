![](https://techcrunch.com/wp-content/uploads/2019/02/Reddit-Header.png?w=1390&crop=1)
## Web APIs & Classification - Subreddit

## Contents

- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Contents of Notebooks](#Contents-of-Notebooks)
- [Data Dictionary](#Data-Dictionary)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)
- [Further Exploration](#Further-Exploration)


## Problem Statement
Travelling has been long considered essential to living in modern society. When wanderlust kicks in, the urge to scour the internet for possible travel destination is insatiable. With resources like blogs, websites, travel guides and videos, there lies a plethora of travel information easily accessible with just a click away. However with so much information available, are we able to quickly segregate these information so that users are able to obtain the relevant information that they require?

One such source is Reddit. Reddit is an American social news aggregation, web content rating, and discussion website. Basically it works like a forum where users can source for information by searching a certain subreddit(also known as threads) topic of interest. Users can also post, comment, and like threads and posts in a forum like content

Therefore to provide travellers with quick access to information, we will try to create a model predict and classify posts of 2 subreddits. This will aid travel companies dessminate travel information quickly to its users for greater customer satisfaction. This could also free up capacity of employees to focus on other productive work at hand. 

The 2 subreddit posts that we have chosen is [r/JapanTravel](https://www.reddit.com/r/JapanTravel/) and [r/SoloTravel](https://www.reddit.com/r/solotravel). These 2 were chosen for its similarities and we will see if our model can successfully classify them sperately. 

## Executive Summary

We will first used the Reddit API to pull data from both the r/Japan Travel and r/SoloTravel subreddits and put it into a dataframe for easier analysis. Next will then perform feature selection where we only select the features of the pulled data that is relevant to us, followed by data cleaning such as checking for nulls and duplicates.

Before we embark on data exploration, we will perfom some functions to the posts which is also known as Natural Language Processesing(NLP) which allows computers to understand the human language like we do. Some of the funtions are:
 * Remove links using regex
 * Remove non-letters using regex
 * Convert text to lower case
 * Lemmatize words which gives us the base words
 * Remove Stopwords which are common words in the english sentence structure like 'the", "them".

Next we will perform some exploratory data analysis on the processed posts to identify interesting trends and relationships between the words of each subreddit.

We will then perform our modelling where we will perform a train test split to fit and compare 2 models: Logistic Regression and Navie Bayes model(Mulinomial). Both of which we will run 2 vectorizers: CountVectorizer and TFIDF Vectorizer to help improve the accuracy. 

Our goal is to achieve at least **85%** accuracy given that both topics are very similar in nature. We will choose the best model that is closest to  goal.

We will then evaluate the model based on metrics such as confusion matrix, ROC AUC and F1 to analyze our chosen model better.

Lastly, we will present our recommendations and findings from our model that we have generated.

## Contents of Notebooks

- [Web Scrapping and Cleaning](code/01_web_scrapping_and_cleaning.ipynb)
- [EDA Preprocessing and Modelling](code/02_eda_preprocess_model.ipynb)


## Data Dictionary

| Feature       | Type | Dataset      | Description                                                                           |
|:---------------|:------|:--------------|:---------------------------------------------------------------------------------------|
| author        | Str  | subreddit_df | Identification name of user that posted                                               |
| title         | Str  | subreddit_df | Title of each post                                                                    |
| cleaned_posts | Str  | subreddit_df | String of words of each post after preprocessing                                      |
| label         | Str  | subreddit_df | Identifies subreddit categories by number. '0' for JapanTravel and '1' for SoloTravel |                                                               |


## Conclusions and Recommendations

* Using Logistic Regression with TFIDF Vectorizer on our subreddit posts, the model was able to classify both posts at an accuracy rate of **96%**

* This was partially due to the Japan specific nature of some terms like Japanese Cities and Japanese infrastructure that would often appear in a JapanTravel Subreddit. 

* From the similar nature of travel, I would have expected that many posts would have been misclassfied. But having 20 misclassfied posts is still an acceptable range of error.

* From the EDA performed on the most common and influential words, we do understand that the fundamental difference between the 2 posts came from which SoloTravel was more of sharing "personal experiences", whereas JapanTravel shares different itinearies within Japan itself, providing information on buses and trains and tourist locations.

* Thus this can help travel companies segregate the market, and be more efficient to cater to the different needs of each travel requests.  


## Further Exploration

* Perhaps we could inlclude all the comments from reddit users reacting to each post. It could provide some interesting words that might be harder for the model to achieve such high accuracy scores. However we will require another API for us to scrap it from reddit.

* We could have more than 1000 posts as well. Currently our API only allows us to obtain a maximum of 1000 posts. Having more posts, again, could come up with more vocablulary for our model.

* Perhaps we could also adopt other models like Random Forest or KNN with boosting that could yield a higher accuracy score for this classification model. 