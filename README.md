<p>
  <img src="images/christian-wiediger-rymh7EZPqRs-unsplash.jpg">
</p>

# Helping Amazon Reviewers Write More Helpfully
**Author**: Elliot Macy

<br>

## Overview
Online retailers like Amazon solicit product reviews from users and rank the reviews according to helpfulness. It is up to users to manually asses review helpfulness, however, by voting whether they find a review helpful or unhelpful. Newly written reviews cannot, therefore, be ranked immediately, and low-traffic reviews may never be ranked if users do not vote on them.

This project asks what if, instead, Amazon could assess review helpfulness automatically. To answer that question, I investigate automatic product review helpfulness prediction using machine learning methods, including random forest, XGBoost, and support vector machine classification models.

## Task definition
Given a set of reviews for a particular product category, classify the reviews according to their helpfulness, with helpfulness defined as whether a review’s ratio of helpful to unhelpful votes is above or below the median ratio for all of that product category’s reviews.

## Data
Amazon maintains a [publicly accessible database](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt) with twenty years of product reviews, by product category, ranging from 1996 through 2015. The dataset includes review texts as well as metadata (star rating, product id, review date, helpful votes, etc.). The figures and results shown here use reviews for products in the "luggage" category. Changing product categories has a negligible impact. Due to volume restrictions, the dataset is not included within the github repo.

## Process
To analyze the data from vantages, I extract 20 lexical, syntactic, structural, and contextual features.

The lexical features consist of unigrams (single words) and bigrams (pairs of words) taken from the text. I filter these using a list of common English words and further cull them by dropping the top 10% most frequently found terms across the review texts (frequently used terms contain less information to distinguish two classes of texts). I normalize the text using lemmatization, meaning to reduce words to their root lemmas, although there is not much benefit as opposed to stemming (simply reducing words to their stems). Finally, I quantify the text using TF-IDF vectorization, meaning the frequency of each term multiplied by the log of the inverse document frequency (the number of documents that include the term divided by the total number of documents), in order to compute the data.

The syntactic features include noun, verb, adjective, and adverb frequencies, which I determine through POS tagging, and the structural features include the quantities and frequencies of characters, words, sentences, exclamations, and questions.

I also augment these textual features with contextual features extracted from review metadata. After vectorizing the unigrams and bigrams, I concatenate the resulting sparse matrix with the syntactic, structural, and contextual features, and pass the combined featureset to three classification models: random forest, XGBoost, and support vector machines. My pipeline includes gridsearches to optimize each model's hyperparameters.

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

## Next Steps
Words depend on other words for meaning. Bigrams (or n-grams) allow machine learning models to partially capture this dependence for pairs (or larger sets) of adjoining words, but words at one end of a sentence can depend just as much on words at the other end for meaning as those in closer proximity.

Bidirectional LSTM recurrent neural networks with self attention are promising options for next steps better suited to the task of classifying language in order to predict a review's helpfulness.

## For More Information
Please contact **Elliot Macy (elimacy@gmail.com)**.

## Repository Structure
Description of the structure of the repository and its contents:
```
├── pickles                             <- (folder) gridsearch hyperparameters
├── images                              <- (folder) graphs, figures, and stock images
├── data_processing.ipynb               <- cleaning and feature extraction
├── eda.ipynb                           <- visualization and analysis
├── modelling.ipynb                     <- tf-idf classification models
├── presentation.pdf                    <- presentation deck
└── README.md                           <- repo overview (what you are reading!)👀
```

<br>

*Photo credit: <a href="https://unsplash.com/@christianw">Christian Wiediger</a> via <a href="https://unsplash.com/">Unsplash</a>*
