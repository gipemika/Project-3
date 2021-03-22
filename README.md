 
# DSI Project 3: Classifying Reddit Posts


## Problem Statement

My startup has created an application that allows consumers to view more information about alcoholic beverage by hovering their phone camera over the bottle. To further improve our application, we wanted to expand the use of our machine learning algorithm and find a way to classify human-generated content, so we can provide suggestions about the drink consumers were referring to. Given that we can gather data from Reddit, our objective now is to find which classification model is best at differentiating beer subreddit posts from wine subreddit posts as these are our targeted alcohol categories.

The two classifier model that will be constructed are Multinomial Naive Bayes model and Logistic Regression model. The evaluation metric that will be used is Accuracy as both models need to correctly classify posts into the respective subreddits.

## Executive Summary

I started off the project by gathering the two subreddit posts: beer and wine. Once I gathered enough dataset (minimum 1,000 posts per each subreddit) I concatenated the two columns that I will evaluate (title and selftext) and started looking at size and general information of the datasets. I began cleaning the dataset by dropping the null values and duplicate values as these are small percentages of the total data. I explored the data visualization in terms of length of title, posting time, and common words. The visualization provided the insights between beer subreddit and wine subreddit.

Then, I preprocessed the data by removing HTML, http, https, commonly used domains, non-letter characters, stopwords, and other special characters. I also converted the data into lowercase and later lemmatized the text. After I merged and saved the cleaned data into one CSV file, I started working on modeling section. I used train/test split to fit both datasets to one another. Then, I used CountVectorizer to transform text and calculated baseline accuracy as a benchmark since accuracy is the evaluation metric for my models. I created two classifier models: Logistic Regression and Multinomial Naive Bayes model as well as confusion matrix for each model. Although using the default hyperparameters give me a good results (more than 90% accuracy), I tried fine-tuning the models by adjusting other hyperparameters and using TFIDF vectorizer as well. However, compared the accuracy score between all of the tuned models, I found that the original Multinomial Naive Bayes model still gives the best accuracy score of 94.3%. Therefore, I concluded that the best model for my Startup to proceed for further development would be Multinomial Naive Bayes model with default hyperparameters.

## Conclusion and Recommendations

### Conclusion:

| Dataset | Type of vectorizer | Type of model | Accuracy Score |
|-|-|-|-|
| Train | Count Vectorizer (default) | Logistic Regresion | 0.993 |
| Test | Count Vectorizer (default) | Logistic Regresion | 0.901 |
| Train | Count Vectorizer (default) | Multinomial Naive Bayes | 0.976 |
| **Test** | **Count Vectorizer (default)** | **Multinomial Naive Bayes** | **0.943** |
| Train | Count Vectorizer (tuned) | Logistic Regresion | 0.966 |
| Test | Count Vectorizer (tuned) | Logistic Regresion | 0.914 |
| Train | Count Vectorizer (tuned) | Multinomial Naive Bayes | 0.979 |
| Test | Count Vectorizer (tuned) | Multinomial Naive Bayes | 0.941 |
| Train | TFIDF Vectorizer (tuned) | Logistic Regresion | 0.987 |
| Test | TFIDF Vectorizer (tuned) | Logistic Regresion | 0.911 |
| Train | TFIDF Vectorizer (tuned) | Multinomial Naive Bayes | 0.972 |
| Test | TFIDF Vectorizer (tuned) | Multinomial Naive Bayes | 0.931 |

With our objective of finding the best classification model to differentiate wine subreddit posts to beer subreddit posts, we found that our default Multinomial Naive Bayes model with count vectorizer gives the best accuracy score of 94.3%. I concluded that the best model for my Startup to proceed for further development would be Multinomial Naive Bayes model with default hyperparameters and count vectorizer.


### Key Findings:
- While both subreddits have heavy right-skewed graph, titles in wine subreddit seems to be shorter than those of beer subreddit. With not significant difference in number of words in titles, both subreddits are similarly verbose.
- The most popular time for posting on wine subreddit is 8pm, which is a lot earlier than the most popular time for posting on beer subreddit of 2am. Wine subreddit appears to be less active compared to beer subreddit as number of posts are under 20 posts per hour majority of the time while Beer subreddit has more 20 posts per hour majority of the time.
- As this beer subreddit is created to "discuss your favorite beers and breweries, and share beer related articles", it is not surprising to see the word 'beer' as the most common word, followed by 'like' being the second most common word here. Then, there is a drop after the word 'like' as other common words such as 'know', 'would', 'one', and 'anyone' occuring in range of 200. From these top common words, it is likely that majority of posts ask questions on what/where to find good brewery/drink.
- While 'wine' is the most common word in wine subreddit, the second most common word found in wine subreddit is 'bottle', which makes sense as wine is often packaged in bottle. The word 'like' is found as the top common word in wine subreddit as well. Other similar common words to beer subreddits include 'would', 'one', 'know', indicating how both subreddits share enough similarity to be used in classification model. At the same time, words such as 'red' and 'year' can be used to specifically identified that the post may be discussing about wine.


### Recommendations:
Moving forward, steps that I can take to tune and tweak my model for better accuracy score would be to:
- Feature engineer more features such as characters or word lengths
- Explore other features that could play significant role in predicting outcome such as post comments
- Try using other models such as Decision Trees, Random Forests
- Hypertune my classifier again to reduce overfitting 
- Try adding the keyword "wine" and "beer" to the list of stopwords to see how well the model can classify without these key predictors
- Create my own list of stop words such as "bottle", "anyone"
- Explore more evaluation metrics apart from accuracy score such as ROC AUC score
- Try collecting more data
