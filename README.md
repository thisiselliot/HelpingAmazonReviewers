<p>
  <img src="images/christian-wiediger-rymh7EZPqRs-unsplash.jpg">
  Photo by <a href="https://unsplash.com/@christianw">Christian Wiediger</a> on <a href="https://unsplash.com/">Unsplash</a>
</p>

# Helping Amazon Reviewers Write More Helpfully
**Author**: Elliot Macy

<br>

## Overview
Amazon, the world’s largest online shopping platform, depends on user generated product reviews for building consumer trust. Amazon promotes helpful reviews by inviting users to tag reviews that they find are helpful (or not helpful). Furthermore, every review lists the number of users who tagged it as ‘helpful’ and, by default, Amazon sorts product reviews by the number of ‘helpful’ tags they receive.

Amazon maintains a [publicly accessible database](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt) with twenty years of product reviews, by product category, ranging from 1996 through 2015. The dataset includes review texts as well as metadata (star rating, product id, review date, helpful votes, etc.).

The goal of this project is to predict a review's likely helpfulness rating relative to the median (posed as a binary classification: un/helpful). Lexical features are tf-idf vectorised to reduce sparcity and augmented by textual and contextual feature extraction. Supervised learning models, incluing random forests and XGBoost, are implemented as binary classifiers and evaluated for accuracy, recall, and f1-scores.

<br>

## Process
1. Data preperation*
    1. Drop junk data, set review date to datetime object, and define target label as helpful/unhelpful ratio
    2. Tokenize text, drop stopwords, and normalize vocabulary for TF-IDF
    3. Extract textual and con-textual features

2. EDA
    1. \[Step 1]
    2. \[Step 2]
    3. \[Step 3]

3. Modelling
    1. Combine TF-IDF vectors with extracted features and split train and test sets
    2. Optimize random forest and XGBoost classifiers with gridsearch
    3. Fit and predict on classifiers

*\*download zipped files and expand into "data" subdirectory (needs to be created) and replace "filename" variable with filename (sans extension)*
<br>

## Results
**RANDOM FOREST**
Training         | Testing
---------------- | -------------
Accuracy: 0.6013 | Accuracy: 0.6040
Recall: 0.7055   | Recall: 0.6951
F1: 0.6365       | F1: 0.6383

**XGBOOST**
Training         | Testing
---------------- | -------------
Accuracy: 0.8370 | Accuracy: 0.6135
Recall: 0.8415   | Recall: 0.6049
F1: 0.8363       | F1: 0.6114

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
