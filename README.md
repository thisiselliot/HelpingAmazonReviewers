<p>
<img src="images/christian-wiediger-rymh7EZPqRs-unsplash.jpg">
Photo by <a href="https://unsplash.com/@christianw">Christian Wiediger</a> on <a href="https://unsplash.com/">Unsplash</a>
</p>

# Helping Amazon Reviewers Write More Helpfully
**Author**: Elliot Macy


Amazon maintains a [publicly accessible database](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt) with twenty years of product reviews, by product category, ranging from 1996 through 2015. The dataset includes review texts as well as metadata (star rating, product id, review date, helpful votes, etc.).

The goal of this project is to predict a review's likely helpfulness rating relative to the median (posed as a binary classification: un/helpful). Lexical features are tf-idf vectorised to reduce sparcity and augmented by textual and contextual feature extraction. Supervised learning models, incluing random forests and XGBoost, are implemented as binary classifiers and evaluated for accuracy, recall, and f1-scores.

## Business Understanding

Amazon, the world’s largest online shopping platform, depends on user generated product reviews for building consumer trust. Amazon promotes helpful reviews by inviting users to tag reviews that they find are helpful (or not helpful). Furthermore, every review lists the number of users who tagged it as ‘helpful’ and, by default, Amazon sorts product reviews by the number of ‘helpful’ tags they receive.

## For More Information
For any additional questions, please contact **Elliot Macy (elimacy@gmail.com)**.

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
