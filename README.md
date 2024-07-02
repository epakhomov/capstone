# A machine learning model for phishing websites detection.

## Introduction

This README file provides a summary of findings for a Capstone project: A machine learning model for phishing websites detection.

The accompanying Jupyter notebook can be [found here](https://github.com/epakhomov/capstone/blob/main/scr/DataSet1_3.ipynb). 

## The objective and the data

The objective of this assignment is to compare the performance of the classifiers (dummy classifier, k-nearest neighbors, logistic regression, decision trees, and support vector machines). The dataset for this assignment could be found [here](https://archive.ics.uci.edu/dataset/222/bank+marketing).


## The business objective 

The business objective is to find a machine learning model that would predict whether a customer would open a long term deposit or not. The model will help improve the efficiency of marketing campaigns by adjusting the campaign's parameters according to the model.

## The methods

The methodology for this assignment was based on CRISP_DM framework and included standard ML stages like Business and Data understanding, Data preparation, etc. 

## Models evaluation metrics

The dataset is highly imbalanced, so the standard accuracy score is not a good metric for this case. Given the business problem, the **precision score** seems to be more appropriate. The precision is intuitively the ability of the classifier not to label as positive a sample that is negative. In this context, it means the customer does not open long term deposit, but the model predicts the opposite. This type of error would impact revenue forecast negatively and everybody hates when it happens.


## Data quality and data preparation highlights

The data had no missing values. The categorical variables were target encoded. Standard scaled was applied.

## Models performance with the default parameters.

The precision scores and train times for each model can be found in Table 1.

|  Model  | Train score | Test score| Train times, s| 
|---------|-------------|-----------|---------------|
| Dummy   | 0.0         | 0.0       | 0.004         |
| Logistic| 0.664	    | 0.667     | 0.0990        |       
| KNN     | 0.745       | 0.575     | 0.0151        |       
| D. Tree | 1.0         | 0.49      | 0.1478        |  
| SVM     | 0.749       | 0.664     | 5.0280        |

Table 1. The precision score for models with default hyperparameters.

## Hyperparameters tuning

GridSearchCV was applied to each model to find the best hyperparameters. The comparison of precision scores for the **test data** for models with default hyperparameters and best hyperparameters can be found in Table 2.

|  Model  | Default     | Best      | 
|---------|-------------|-----------|
| Logistic| 0.667       | 0.665     |
| KNN     | 0.575	    | 0.602     | 
| D. Tree | 0.49        | 0.593     | 
| SVM     | 0.664       | 0.691     |

Table 2. Precision scores for test data for default and tuned models.

Best parameters for the SVM were: C=0.1, gamma='scale', kernel='poly'

## Feature selection 

To further improve the performance, Sequential Feature Selector was used to remove (backward selection) features to form a feature subset for SVM with the best parameters found earlier with GridSearchCV.


## Results and discussion

### Precision score interpretation

Precision is a metric used in machine learning to measure how often a model's positive predictions are correct. The higher the score, the better model performed. According to various sources, precision needs to be at minimum 70-80% (0.7-0.8) for a model to be useful. 

As we can see from Table 1, no model with default parameters scored above 0.7 on the test data, although logistic regression and SVM models got really close.

After finding best parameters with GridSearchCV, the scores improved for all models (except for logistic regression), however, the improvement was insignificant and no model scored above 0.7. However, the SVM scored better than others, therefore it was decided to improve the SVM model performance by removing features with Sequential Feature Selector. The results can be seen on Fig.2.

<img src="/images/2.png" alt="Fig.2" class="center" style="width:600px;height:auto;">

As we can see from the plot, the model trained with 10 features yielded the highest precision score on the test data - **0.725**. 

With Sequential Feature Selector, we could also rank features, i.e., we were able to count instances of features selected in all iteration that were performed. The results can be found in Table 3.

| Feature     | Rank | 
|-------------|------|
| duration    | 8    |
| nr.employed | 8    |
| poutcome    | 7    |
| campaign    | 6    |
| day_of_week | 5    |
| job         | 4    |
| education   | 4    |
| pdays       | 4    |
| loan        | 3    |
| cons.price  | 3    |
| housing     | 1    |

Table 3. Ranking of the features based on the output from Sequential Feature Selector.

As we can see the most impactful features are "duration", "nr.employed", "poutcome" and campaign. However, as we know from the data, the duration variable should be discarded if the intention is to have a realistic predictive model. With that said, one should consider number of contacts in the campaign, outcome of the previous campaign and number of employers as an important predictors.  

## Next steps

There are additional strategies that we can use to improve the model:
- Using different model like neural networks as SVM is not a good fit for a large dataset like this.
- Different encoding of categorical variables.
- Dropping the "duration" variable and repeat the modeling process.