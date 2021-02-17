<p>
  <img src="images/christian-wiediger-rymh7EZPqRs-unsplash.jpg">
  <br>
</p>

# Helping Amazon Reviewers Write More Helpfully
**Author**: Elliot Macy


## Overview
Online retailers like Amazon solicit product reviews from users and rank the reviews according to helpfulness. It is up to users to manually asses review helpfulness, however, by voting whether they find a review helpful or unhelpful. Newly written reviews cannot, therefore, be ranked immediately, and low-traffic reviews may never be ranked if users do not vote on them.

This project asks what if, instead, Amazon could assess review helpfulness automatically. To answer that question, I investigate automatic product review helpfulness prediction using machine learning methods, including random forest, XGBoost, and support vector machine classification models.

## Task definition
Given a set of reviews for a particular product category, classify the reviews according to their helpfulness, with helpfulness defined as whether a review’s ratio of helpful to unhelpful votes is above or below the median ratio for all of that product category’s reviews.

<br>

## Data
Amazon maintains a [publicly accessible database](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt) with twenty years of product reviews, by product category, ranging from 1996 through 2015. The dataset includes review texts as well as metadata (star rating, product id, review date, helpful votes, etc.). The figures and results shown here use reviews for products in the "luggage" category. Changing product categories has a negligible impact.

<br>

## Process
1. Data preparation*
    1. Drop junk data, set review date to datetime object, and define target label as helpful/unhelpful ratio
    2. Tokenize text, drop stopwords, and normalize vocabulary for TF-IDF
    3. Extract textual and con-textual features

2. EDA
    1. Visualize helpful/unhelpful vocabularies' word frequencies

3. Modelling
    1. Combine TF-IDF vectors with extracted features and split train and test sets
    2. Optimize random forest and XGBoost classifiers with gridsearch
    3. Fit and predict on classifiers

*\*[download](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt) and expand zipped datasets into "data" subdirectory (**not** included with repo) and replace "filename" variable with dataset filename*

<br>

## Results
**RANDOM FOREST**
Training          | Testing
----------------- | -------------
Accuracy:  0.6306 | Accuracy:  0.6294
Precision: 0.5933 | Precision: 0.5958
Recall:    0.7688 | Recall:    0.7714
F1:        0.6697 | F1:        0.6723

**XGBOOST**
Training          | Testing
----------------- | -------------
Accuracy:  0.7048 | Accuracy:  0.6337
Precision: 0.6845 | Precision: 0.6168
Recall:    0.7309 | Recall:    0.6777
F1:        0.7070 | F1:        0.6458

**SVM**
Training          | Testing
----------------- | -------------
Accuracy:  0.6727 | Accuracy:  0.6491
Precision: 0.6389 | Precision: 0.6223
Recall:    0.7549 | Recall:    0.7327
F1:        0.6921 | F1:        0.6730

<br>

## Next Steps
Words depend on other words for meaning. Bigrams (or n-grams) allow random forests and XGBoost to partially capture this dependence for pairs (or larger sets) of adjoining words, but words at one end of a sentence can depend just as much on words at the other end for meaning as those in closer proximity.

Bidirectional LSTM recurrent neural networks with self attention are promising options for next steps better suited to the task of classifying language in order to predict a review's helpfulness.

<br>

## For More Information
Please contact **Elliot Macy (elimacy@gmail.com)**.

<br>

## Repository Structure
Description of the structure of the repository and its contents:
```
├── pickles                             <- (folder) gridsearch hyperparameters
├── images                              <- (folder) graphs, figures, and stock images
├── data_processing.ipynb               <- cleaning and feature extraction
├── eda.ipynb                           <- visualization and analysis
├── modelling.ipynb                     <- tf-idf classification models
└── README.md                           <- repo overview (what you are reading!)👀
```

<br>

*Photo credit: <a href="https://unsplash.com/@christianw">Christian Wiediger</a> via <a href="https://unsplash.com/">Unsplash</a>*
