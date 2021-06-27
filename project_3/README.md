# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & NLP

## Project 3: Web APIs & NLP

### Details
Name: Wenna Loo Yan Ying

Class: DSIF-SG-1

## Problem Statement
Reddit is a massive collection of forums where registered members can share news and content or comment on other member’s posts. Posts are organised by subject into user-created boards called "communities" or "subreddits", which cover a variety of topics such as news, politics, religion, science, movies, video games, music, books, sports, fitness, cooking, pets, and image-sharing. As aspiring data scientists who have just completed a lesson on natural language processing (NLP), we are interested to find out if we can use NLP to classify posts from two different subreddits based on their title and text content. Such a classification model may be useful for Reddit as a company or even the subreddit moderators to make sure that the posts shown on the subreddit are relevant to the community.

## Executive Summary
For this project, we'll be classifying posts from two subreddits that are similar:
- r/GME: A subreddit channel where Reddit users share and discuss content related to Gamestop ($GME) Stock
- r/dodgecoin: A subreddit channel where Reddit users share and discuss content related to Dogecoins

Reddit has made various headlines, most notably when its community helped pump GameStop’s share price to triple-digit growth in late January. This mania later spread to dogecoin which saw massive price run-ups *([source](https://www.coindesk.com/investors-pump-250m-into-reddit-following-social-media-sites-prominent-role-in-gamestop-mania))*. Using NLP to analyse the posts from the two subreddits may help to shed some insight on the GameStop and Dogecoin mania.

Starting with data acquisition, we collected posts from r/GME and r/dodgecoin by connecting to Pushshift Reddit API. This Web API allows us to access the Reddit comment and submission database to extract their data. We have collected posts from r/GME between 21st Jan 2021 to 2nd Feb 2021 because that was the timeline whereby GameStop shares have surged due to its popularity. We limited the collection of posts from r/dodgecoin to 5th May 2021 due to the long waiting time required for the initial period selected. There are about 6,805 posts from r/GME and 10,750 posts from r/dodgecoin. The posts collected were then cleaned, pre-processed for exploratory data analysis (EDA) and classification modelling. Based on the insights from our EDA, we zoomed in on the characteristics (i.e the words usage/type of posts) of each subreddit and were able to learn more about the GameStop and Dogecoin mania.

Following the EDA process, we tested and evaluated three classification models - Logistic Regression, Naive Bayes & Random Forest Classifier with two different NLP vectorizers - Count Vectorizer & TF-IDF Vectorizer to select the best parameters which produce the best model performance. The Naive Bayes model using CountVectorizer was then selected as our production model. Our production model is able to classify posts from the two subreddits with an F1-Score score of 96%. We consider our production model to be performing relatively well given that the two subreddits are quite similar. This simple classifier will be beneficial for Reddit as a company or even the subreddit moderators to keep the contents of each subreddit relevant to the community.

## Recommendations

We would recommend the subreddit moderators of r/GME and r/dogecoin to use our model as it can correctly classify 93.61% of GME posts and 97.37% of dogecoin posts. The model hence eliminates the need for manual screening currently performed by the subreddit moderators and will free up their time to focus their expertise on more productive tasks. The subreddit moderators can also use the insights from the model to understand the overall direction of their subreddit.

Alternatively, this model can be deployed to be used by the subreddit community instead. The model can be integrated into the Reddit platform/ enabled as a browser extension, to help suggest the correct subreddit for the users to publish their post.
